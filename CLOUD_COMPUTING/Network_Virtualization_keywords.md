# Network Virtualization Dictionary

> A comprehensive reference for network virtualization keywords — covering kernel bypass, virtual interfaces, container networking, eBPF, SR-IOV, and more.

---

## Table of Contents

- [Core Networking Concepts](#core-networking-concepts)
- [Virtual Interfaces & Tunneling](#virtual-interfaces--tunneling)
- [Bridges & Switching](#bridges--switching)
- [DPDK & Kernel Bypass](#dpdk--kernel-bypass)
- [SR-IOV](#sr-iov)
- [eBPF & XDP](#ebpf--xdp)
- [DPI & Traffic Analysis](#dpi--traffic-analysis)
- [CNI Plugins & Container Networking](#cni-plugins--container-networking)
- [Quick Reference Table](#quick-reference-table)

---

## Core Networking Concepts

### Interface
A logical or physical point where two systems connect and communicate. In virtualization, interfaces are often virtual constructs mapped to physical hardware — they may exist only in software (veth, tun, tap) or represent abstracted views of physical NICs (SR-IOV VF).

### Linux Network Stack
The kernel's built-in networking subsystem handling packet processing through layers: socket → transport (TCP/UDP) → network (IP) → link layer. Virtual networking solutions either use this stack or bypass it entirely for performance. Many high-throughput NFV deployments intentionally avoid it using DPDK or XDP.

### Network Namespace
A Linux kernel feature that creates isolated copies of the network stack — each namespace has its own interfaces, routing tables, firewall rules, and sockets. This is the foundation of container networking. Every container gets its own namespace, making it believe it has a dedicated network. Pods in Kubernetes share a namespace within the pod but are isolated from other pods.

### NAT (Network Address Translation)
Rewrites source/destination IPs in packet headers. Used heavily in container networking to allow pods/containers on private IP ranges to reach the outside world. kube-proxy traditionally implements NAT via iptables rules; Cilium replaces this with eBPF for better performance.

### VLAN (Virtual LAN)
Tags ethernet frames with an 802.1Q tag to logically segment a physical network into multiple broadcast domains. A single physical switch port can carry traffic for multiple VLANs. Used in OVS to isolate tenant traffic in multi-tenant virtualized environments.

### Cgroups (Control Groups)
A Linux kernel mechanism to limit, prioritize, and account for resource usage (CPU, memory, network bandwidth) per process group. Works alongside namespaces to form the container isolation model. In eBPF, cgroups also serve as attach points for network programs — enabling per-pod policies.

---

## Virtual Interfaces & Tunneling

### Veth Pair
Virtual Ethernet Pair — two linked virtual interfaces that act like a pipe. Whatever enters one end comes out the other. The standard tool for connecting a container's network namespace to the host. One end sits inside the container namespace, the other on the host bridge or routing table.

```
[ Container NS ]       [ Host NS ]
  eth0 (veth0)  <--->  veth1 → Linux Bridge / OVS
```

### Tap (Terminal Access Point)
A layer-2 virtual interface that simulates an Ethernet device. Packets are delivered to a userspace program as raw Ethernet frames. Used heavily in VMs — QEMU/KVM uses tap devices to give VMs network access. The hypervisor reads/writes raw frames via the tap file descriptor.

### Tun (Network Tunnel)
A layer-3 virtual interface similar to Tap but operates at the IP level. Used in VPN implementations (OpenVPN, WireGuard). The kernel routes IP packets into userspace for processing, where they are typically encrypted and forwarded through a real interface.

| Feature | Tap | Tun |
|---------|-----|-----|
| Layer | L2 (Ethernet frames) | L3 (IP packets) |
| Use case | VM networking, bridges | VPNs, tunnels |
| Sees MAC headers | Yes | No |

### Vhost-net
A kernel module that accelerates virtio-net by moving the data-plane processing into the kernel, avoiding expensive userspace context switches. The guest sends packets via virtio rings, and vhost-net handles them in kernel space on the host, directly passing them to the tap interface.

### Virtio
A standardized interface for virtual devices between a hypervisor and a guest VM. Defines the protocol for efficient I/O between guest and host without emulating real hardware. Uses shared memory ring buffers (virtqueues) to pass descriptors between guest driver and host backend.

### Virtio-net
The virtual NIC implementation of Virtio. A paravirtualized network driver inside the guest that communicates with the host via virtqueues instead of emulating a real NIC. Much faster than full emulation (e.g., emulated Intel e1000) because it avoids the overhead of mimicking hardware registers.

### Virtio-user PMD
A DPDK Poll Mode Driver that speaks the virtio protocol in userspace. Allows a userspace DPDK application (like OVS-DPDK) to act as the virtio backend, enabling high-speed packet passing between containers and DPDK-based vSwitches without going through the kernel. Bridge between the virtio world and DPDK.

### Memif (Memory Interface)
A shared-memory based interface used primarily in VPP and DPDK environments. Two userspace applications share a ring buffer in memory and exchange packets at very high speed with near-zero overhead — no kernel involvement at all. Ideal for chaining NFV functions running as separate processes.

```
[ NFV App A ] <-- shared memory ring --> [ NFV App B ]
                      memif
```

### SPAN (Switched Port Analyzer)
Port mirroring — duplicates traffic from one interface and sends it to another for monitoring or analysis without interrupting the main flow. OVS supports SPAN for feeding traffic copies to monitoring tools, IDS engines, or DPI probes. Does not affect the mirrored traffic path.

---

## Bridges & Switching

### Linux Bridge
A kernel-level layer-2 software switch. It learns MAC addresses and forwards frames between attached interfaces. Simple and widely used — Docker's default networking uses a Linux bridge (`docker0`). Slower than OVS-DPDK but zero additional dependencies.

### OVS (Open vSwitch)
A production-grade, programmable virtual switch designed for virtualized environments. Supports OpenFlow for centralized SDN control, VLAN tagging, tunneling (VXLAN, GRE, Geneve), and has a userspace datapath that integrates with DPDK. The workhorse of most serious virtual networking deployments — used in OpenStack, Kubernetes (with OVN), and telco NFV platforms.

**Key OVS components:**

| Component | Role |
|-----------|------|
| `ovs-vswitchd` | Main daemon, datapath management |
| `ovsdb-server` | Configuration database |
| Kernel datapath | Fast-path forwarding in kernel |
| DPDK datapath | Userspace fast-path (OVS-DPDK) |

### OVS-DPDK Daemon
OVS running with its userspace datapath powered by DPDK instead of the kernel. The `ovs-vswitchd` process uses DPDK PMDs to receive/send packets entirely in userspace, achieving dramatically higher throughput and lower latency than kernel OVS. Requires hugepages and dedicated CPU cores for PMD threads.

### DPDK vSwitch
Any virtual switch whose dataplane is implemented using DPDK. OVS-DPDK is the most common example. Packets never touch the kernel datapath — they go straight from NIC → DPDK PMD → vSwitch logic → destination interface.

### CNI (Container Network Interface)
A standard specification and set of libraries for configuring network interfaces in Linux containers. Kubernetes calls CNI plugins at pod creation/deletion time to set up and tear down networking. CNI defines *what* a networking plugin must do (add/del interface, assign IP), not *how* — giving plugin authors freedom to use veth pairs, eBPF, SR-IOV, or any other mechanism.

### CNI Bridge
The reference CNI plugin that creates a Linux bridge on the host and connects each pod via a veth pair. Simple, widely understood, suitable for development and small clusters. Lacks features like network policy enforcement or high-performance datapaths — typically replaced by Calico, Cilium, or similar in production.

```
Pod NS: eth0 <--veth--> host: vethXXX --> cni0 (Linux Bridge) --> eth0 (host NIC)
```

---

## DPDK & Kernel Bypass

### DPDK (Data Plane Development Kit)
A set of userspace libraries and drivers that allow applications to take full control of network hardware and process packets entirely in userspace, bypassing the Linux kernel network stack. Dramatically reduces latency (sub-microsecond) and increases throughput for NFV and telecom workloads. The NIC is bound to a UIO/VFIO driver and controlled exclusively by the DPDK application.

```
Normal path:  NIC → kernel driver → kernel network stack → socket → app
DPDK path:    NIC → VFIO/UIO → DPDK PMD → userspace app   (no kernel stack)
```

### PMD (Poll Mode Driver)
DPDK's driver model. Instead of using interrupts (which cause context switches), PMDs have dedicated CPU cores that spin in a tight loop continuously polling the NIC's RX queues for new packets. Eliminates interrupt overhead at the cost of dedicating full CPU cores — those cores run at 100% even when idle.

### DPDK Mempool
A pre-allocated pool of fixed-size memory buffers (`mbuf`s) used by DPDK for packet storage. Allocated from hugepages at startup to minimize TLB misses. Applications grab buffers from the pool, fill them with packet data, process and forward them, then return them — avoiding expensive dynamic `malloc`/`free` calls in the hot path.

### Hugepages
Memory pages larger than the default 4 KB (typically 2 MB or 1 GB). DPDK requires hugepages because they reduce TLB (Translation Lookaside Buffer) misses when working with large memory regions for packet buffers and DMA. Configured in the OS before DPDK applications start (e.g., `echo 1024 > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages`).

### UIO / VFIO Driver
Kernel drivers that allow DPDK to take ownership of a NIC away from the standard kernel driver.

| Driver | Description |
|--------|-------------|
| **UIO** (Userspace I/O) | Simpler, older approach; maps NIC registers/memory to userspace |
| **VFIO** (Virtual Function I/O) | Adds IOMMU support for safe, isolated DMA from userspace — preferred for security |

After binding a NIC to `vfio-pci`, DPDK's PMD controls it directly and the kernel sees no traffic on that interface.

### DPDK PMD Controlled
Describes a NIC or virtual interface that is driven by a DPDK Poll Mode Driver rather than the Linux kernel. The NIC is invisible to the Linux network stack — only the DPDK application can send/receive on it. This includes both physical NICs (bound via VFIO) and virtual interfaces like `virtio-user` memif.

---

## SR-IOV

### SR-IOV (Single Root I/O Virtualization)
A PCIe standard that allows a single physical NIC (the **Physical Function / PF**) to present itself as multiple independent virtual devices to the OS. Each virtual device is a **Virtual Function (VF)**. Hardware-level isolation — each VF has its own queues, interrupts, and can be assigned directly to a VM or container. Enables near line-rate networking without a software vSwitch in the data path.

```
Physical NIC (PF)
  ├── VF 0  → VM / Container A
  ├── VF 1  → VM / Container B
  └── VF 2  → VM / Container C
```

### SR-IOV VF (Virtual Function)
One of the virtual NIC instances created by SR-IOV. A VF is assigned directly to a VM or container via VFIO passthrough (device passthrough), giving it near line-rate performance since packets go directly between the VF hardware and the guest — bypassing the hypervisor's software switching entirely. The trade-off is reduced flexibility: no live migration support and limited visibility into VF traffic.

---

## eBPF & XDP

### eBPF (Extended Berkeley Packet Filter)
A Linux kernel technology that allows running sandboxed, verified programs inside the kernel without changing kernel source or loading modules. In networking, eBPF programs can inspect, modify, redirect, or drop packets at various hook points (XDP, TC, sockets, cgroups). The basis of modern CNI plugins like Cilium. Programs are written in a restricted C subset, compiled to eBPF bytecode, verified by the kernel verifier, then JIT-compiled to native machine code.

```
eBPF Program Lifecycle:
  Write (C) → Compile (clang/LLVM) → Load (BPF loader) → Verify (kernel) → JIT → Attach to hook
```

### XDP Hook Point (eXpress Data Path)
The earliest possible point in the Linux kernel where an eBPF program can intercept a packet — right when the NIC driver receives it, before any memory allocation, sk_buff creation, or stack processing. Enables very high-speed packet processing (DDoS mitigation, load balancing) with near DPDK-level performance while staying in the kernel ecosystem and retaining access to kernel features.

**XDP actions:**

| Action | Meaning |
|--------|---------|
| `XDP_PASS` | Send packet up to normal kernel stack |
| `XDP_DROP` | Drop packet immediately |
| `XDP_TX` | Retransmit out the same interface |
| `XDP_REDIRECT` | Send to another interface or CPU |
| `XDP_ABORTED` | Drop with error tracing |

### BPF Loader
A userspace tool or library responsible for compiling, verifying, and loading eBPF bytecode into the kernel, and attaching it to the appropriate hook point. Common loaders include `libbpf`, `bpftool`, and `iproute2` (`tc` command). Cilium uses its own loader that manages eBPF program lifecycle for all pods dynamically.

### Connect4
An eBPF program type that hooks into the `connect()` system call at the cgroup level for IPv4 sockets. Used by Cilium to transparently redirect connections — for example, redirecting a pod's connection destined for a ClusterIP service IP directly to a backend pod IP, bypassing kube-proxy and iptables chain traversal entirely. The application is unaware of the redirection.

### Cgroups (in eBPF context)
Beyond resource limiting, cgroups serve as eBPF attach points. eBPF programs attached to a cgroup apply to all processes within it — enabling per-pod socket-level load balancing, connection tracking, and network policy enforcement without iptables. Cilium attaches programs to each pod's cgroup for fine-grained control.

---

## DPI & Traffic Analysis

### DPI (Deep Packet Inspection)
Inspecting packet payload beyond headers — examining application-layer content to identify protocols, applications, or malicious patterns. In virtual networks, DPI engines are often inserted as service functions in an NFV service chain, receiving traffic copies via SPAN or tap interfaces. Used for firewalling, QoS classification, intrusion detection, and lawful intercept.

---

## CNI Plugins & Container Networking

### Cilium
A CNI plugin built entirely on eBPF. Replaces iptables-based kube-proxy with eBPF programs for service load balancing, implements network policy at the socket and packet level, and provides deep observability via Hubble. Uses Connect4 for service redirection, XDP for load balancing and DDoS protection, and TC hooks for network policy enforcement. Zero iptables rules in the datapath.

### Calico eBPF
Calico's high-performance dataplane mode using eBPF instead of iptables. Provides similar capabilities to Cilium's eBPF mode — replacing kube-proxy, enforcing network policy, and reducing latency by eliminating iptables chain traversal. Calico also supports a standard Linux datapath (iptables) and a VPP datapath for telco-grade performance.

### Flannel
A simple, lightweight CNI plugin focused purely on giving each node a subnet and providing basic pod-to-pod connectivity. Typically uses VXLAN for cross-node tunneling. Easy to operate but lacks network policy enforcement — commonly paired with Calico (for policy) or replaced by Cilium in performance-sensitive environments.

---

## Quick Reference Table

| Category | Keywords |
|----------|----------|
| **Isolation primitives** | Network Namespace, Cgroups, SR-IOV VF |
| **Virtual interfaces** | Veth Pair, Tap, Tun, Memif, Virtio-net, Vhost-net |
| **Switching / bridging** | Linux Bridge, OVS, OVS-DPDK, CNI Bridge, DPDK vSwitch |
| **Kernel bypass** | DPDK, PMD, Hugepages, UIO/VFIO, Mempool, Virtio-user PMD |
| **Hardware offload** | SR-IOV, SR-IOV VF, DPDK PMD Controlled |
| **eBPF ecosystem** | eBPF, XDP, BPF Loader, Connect4, Cilium, Calico eBPF |
| **Container networking** | CNI, CNI Bridge, Flannel, Cilium, Calico |
| **Traffic handling** | NAT, VLAN, SPAN, DPI |
| **VM networking** | Virtio, Virtio-net, Vhost-net, Tap |
| **Observability** | SPAN, DPI, eBPF |

---
