# Network Flow: Physical NIC → Virtual NIC →  Container
---

## 🎯 What We're Learning

**How does a network packet travel from a physical cable all the way into a container?**

Let me show you with clear diagrams and simple explanations.

---

## 📊 THE COMPLETE PICTURE

```                 
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  1. PHYSICAL WORLD                                      │
│     [Ethernet Cable] ──> [Physical NIC Card]           │
│                                                         │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ IRQ (Interrupt Request)
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  2. LINUX KERNEL                                        │
│     Driver reads packet → creates sk_buff              │
│     Packet is now "inside" the operating system        │
│                                                         │
└────────────────────┬────────────────────────────────────┘
                     │
                     │ Now packet must choose a path...
                     │
        ┌────────────┼────────────┐
        │            │            │
        ▼            ▼            ▼
    ┌─────┐     ┌─────┐     ┌─────┐
    │ PP  │     │ PB  │     │ PF  │
    │OVS  │     │DPDK │     │eBPF │
    └──┬──┘     └──┬──┘     └──┬──┘
       │           │            │
       └───────────┼────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  3. VIRTUAL NIC (veth pair)                             │
│     Host Side ←──cable──→ Container Side                │
│     [veth0]   ←─linked─→  [veth1 = eth0]                │
│                                                         │
└────────────────────┬────────────────────────────────────┘
                     │
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  4. SOFTWARE SWITCH (Bridge or OVS)                     │
│     Decides: which veth should get this packet?         │
│     Like a traffic cop directing cars                   │
│                                                         │
└────────────────────┬────────────────────────────────────┘
                     │
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  5. CNI PLUGIN (Cilium/Calico/Flannel)                │
│     This is WHO set everything up in the first place   │
│     Created the veth, assigned IPs, configured routing │
│                                                         │
└────────────────────┬────────────────────────────────────┘
                     │
                     │
                     ▼
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  6. CONTAINER / POD                                     │
│     Packet arrives! Container sees it on "eth0"        │
│     Application receives the data                      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 🔍 DETAILED EXPLANATION OF EACH LAYER

---

## 1️⃣ PHYSICAL NIC - The Hardware Gateway

```
     Real World Network
            |
            | (Ethernet cable)
            |
            ▼
    ┌───────────────┐
    │  Physical NIC │  ← Real hardware chip
    │   (eth0)      │
    └───────┬───────┘
            │
            │ (writes to RAM via DMA)
            │
            ▼
    ┌───────────────┐
    │  DMA Buffer   │  ← Special memory area
    │   in RAM      │
    └───────┬───────┘
            │
            │ (fires IRQ - interrupt signal)
            │
            ▼
```

### **What is happening here:**

**Physical NIC** = A real hardware card plugged into your server
- Has a MAC address (like `00:1A:2B:3C:4D:5E`)
- Connected to actual cables
- Receives electrical signals or light pulses

**What it does:**
1. Frame arrives on the wire
2. NIC writes it directly to RAM (DMA = Direct Memory Access, no CPU needed)
3. NIC sends an **interrupt** to the CPU: "Hey! New packet arrived!"

**Why this matters:**
- This is the ONLY real hardware in the entire chain
- Everything else is software pretending to be hardware
- All virtual NICs ultimately share THIS one physical card

---

## 2️⃣ LINUX KERNEL - Packet Enters Software

```
            IRQ fires
               |
               ▼
    ┌─────────────────────┐
    │   Interrupt Handler │
    │   (CPU wakes up)    │
    └──────────┬──────────┘
               │
               ▼
    ┌─────────────────────┐
    │   NIC Driver        │  ← Software that talks to hardware
    │   (e1000, ixgbe)    │
    └──────────┬──────────┘
               │
               │ Reads from DMA buffer
               │
               ▼
    ┌─────────────────────┐
    │   Creates sk_buff   │  ← The kernel's packet container
    │   (socket buffer)   │
    └──────────┬──────────┘
               │
               │
               ▼
    ┌─────────────────────┐
    │ netif_receive_skb() │  ← Entry to network stack
    │                     │
    └──────────┬──────────┘
               │
               ▼
      Packet is now in the kernel!
```

### **What is happening here:**

**sk_buff** = The kernel's way of storing a network packet
- Contains the raw packet bytes
- Plus metadata: which interface it came from, timestamp, etc.

**Where in the kernel:**
- Driver code: `/drivers/net/ethernet/`
- Network stack: `/net/core/dev.c`

**Key point:**
From this moment on, the packet exists as a **software object** inside Linux kernel memory.

---

## 3️⃣ THREE POSSIBLE PATHS (PP, PB, PF)

```
                  Packet is in kernel
                         |
                         |
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
   ┌────────┐       ┌────────┐      ┌────────┐
   │   PP   │       │   PB   │      │   PF   │
   │ Packet │       │ Packet │      │ Packet │
   │Process │       │ Bypass │      │ Filter │
   └────────┘       └────────┘      └────────┘
       │                │                │
       │                │                │
       ▼                ▼                ▼
   Full kernel     Skip kernel      eBPF programs
   network stack   (DPDK)           (fast filtering)
```

### **Path 1: PP (Packet Processing) - The Normal Route**

```
sk_buff
  │
  ├─> netfilter (iptables rules)
  │
  ├─> routing decision
  │
  ├─> bridge forwarding
  │
  └─> socket or output interface
```

**What it is:**
The default, normal path through the entire Linux network stack.

**When used:**
- Regular Linux networking
- Basic Docker setups
- Simple container clusters

**Speed:** Good, but not the fastest

---

### **Path 2: PB (Packet Bypass - DPDK) - The Fast Lane**

```
Physical NIC
     │
     │ (skip the kernel entirely!)
     │
     └──> DPDK driver
            │
            └──> User-space application
                 (no kernel involvement)
```

**What it is:**
The application reads packets DIRECTLY from the NIC's memory.
No kernel. No interrupts. No sk_buff.

**When used:**
- High-frequency trading
- Telecom / 5G
- When you need 10+ million packets/second

**Speed:** FASTEST possible

**Trade-off:** You must write your own network stack

---

### **Path 3: PF (Packet Filter - eBPF) - The Smart Path**

```
Packet arrives
     │
     ├─> eBPF program at XDP (earliest point)
     │   │
     │   └─> Can drop, modify, or redirect immediately
     │
     ├─> eBPF program at TC (traffic control)
     │   │
     │   └─> Can enforce policies, do NAT
     │
     └─> Continue to destination
```

**What it is:**
Small programs that run INSIDE the kernel at specific hook points.

**When used:**
- **Cilium** (modern CNI plugin)
- High-performance firewalling
- When you need both speed AND flexibility

**Speed:** Nearly as fast as DPDK, but stays in kernel

---

## 4️⃣ VIRTUAL NIC (veth pair) - The Magic Cable

```
┌──────────────────────────┐      ┌──────────────────────────┐
│   HOST NAMESPACE         │      │   CONTAINER NAMESPACE    │
│   (root network stack)   │      │   (isolated network)     │
│                          │      │                          │
│         veth0            │      │          veth1           │
│           │              │      │            │             │
│    (host side of         │      │     (container side)     │
│     virtual cable)       │      │                          │
│           │              │      │     Renamed to: eth0     │
│           │              │      │                          │
│  Attached to bridge/OVS  │      │     Has Pod IP           │
│           │              │      │     10.244.1.5/24        │
└───────────┼──────────────┘      └────────────┼─────────────┘
            │                                   │
            │    Virtual "cable" connection     │
            └───────────────┬───────────────────┘
                            │
                      (anything in veth0 
                       comes out veth1)
```

### **What is a veth pair:**

Think of it as a **virtual Ethernet cable** with two ends:
- **veth0** stays on the host
- **veth1** goes into the container

**Key concept:**
When you send a packet into `veth0`, it **magically appears** at `veth1`.

### **Why we need it:**

Containers run in isolated **network namespaces**:
- Each namespace = separate network stack
- Separate interfaces, IPs, routing tables
- Totally isolated from each other

The veth pair is the **bridge** between host and container namespaces.

---

### **What is a Network Namespace:**

```
┌─────────────────────────────────────────────────────────┐
│                     HOST MACHINE                        │
│                                                         │
│  ┌─────────────────┐         ┌─────────────────┐      │
│  │  Namespace 1    │         │  Namespace 2    │      │
│  │  (Container A)  │         │  (Container B)  │      │
│  │                 │         │                 │      │
│  │  eth0: 10.1.1.2 │         │  eth0: 10.1.1.3 │      │
│  │  routing table  │         │  routing table  │      │
│  │  iptables       │         │  iptables       │      │
│  └─────────────────┘         └─────────────────┘      │
│                                                         │
│  ┌─────────────────────────────────────────────┐       │
│  │        Root Namespace (Host)                │       │
│  │        eth0: physical NIC                   │       │
│  │        br0: bridge                          │       │
│  └─────────────────────────────────────────────┘       │
└─────────────────────────────────────────────────────────┘
```

**Network Namespace** = A completely isolated copy of the network stack.

Each container gets its own namespace:
- Can't see other containers' interfaces
- Can't conflict on IP addresses
- Total isolation

---

## 5️⃣ BRIDGE / OVS - The Software Switch

```
                    Linux Bridge (br0)
                           │
           ┌───────────────┼───────────────┐
           │               │               │
           ▼               ▼               ▼
        veth0           veth2           veth4
           │               │               │
           │               │               │
      (to Pod A)      (to Pod B)      (to Pod C)
```

### **What is a Bridge:**

A **Layer 2 switch** implemented in software.

**What it does:**
1. Receives frames from attached interfaces (veth ports, physical NICs)
2. Looks at destination MAC address
3. Forwards frame to the correct port

**It's like a traffic cop** directing packets to the right destination.

---

### **Linux Bridge vs OVS (Open vSwitch):**

```
┌──────────────────┐              ┌──────────────────┐
│  Linux Bridge    │              │       OVS        │
├──────────────────┤              ├──────────────────┤
│                  │              │                  │
│ • Simple         │              │ • Programmable   │
│ • Built-in       │              │ • OpenFlow       │
│ • Good for basic │              │ • SDN-ready      │
│   setups         │              │ • High perf      │
│                  │              │   (with DPDK)    │
│ • Used by:       │              │ • Used by:       │
│   Flannel        │              │   OpenStack      │
│   Simple Docker  │              │   Large clouds   │
└──────────────────┘              └──────────────────┘
```

**Linux Bridge:**
- Simple software switch in the kernel
- MAC learning, forwarding
- Good enough for most cases

**OVS (Open vSwitch):**
- Advanced, programmable switch
- Can write custom forwarding rules (OpenFlow)
- Can use DPDK for extreme performance
- Used in large-scale deployments

---

## 6️⃣ CNI - The Setup Worker

```
                    Kubernetes creates a Pod
                            │
                            ▼
                    kubelet calls CNI plugin
                            │
            ┌───────────────┼───────────────┐
            │               │               │
            ▼               ▼               ▼
        Flannel         Calico          Cilium
        
        Each CNI plugin's job:
        
        1. Create network namespace
        2. Create veth pair
        3. Move one end into namespace
        4. Attach other end to bridge
        5. Assign IP address (IPAM)
        6. Set up routing rules
```

### **What is CNI:**

**CNI = Container Network Interface**

It's a **standard specification** that says:

> "When you create a container, here's how you should set up its networking."

### **Why CNI exists:**

**Kubernetes does NOT do networking itself.**

Instead, it says:
> "Hey CNI plugin, set up networking for this Pod. I don't care HOW you do it, just make it work."

This is genius because:
- Different environments need different networking
- Cloud providers can write their own plugins
- You can swap networking solutions without changing Kubernetes

---

### **What does a CNI plugin actually do:**

When a Pod is created:

```
Step 1: Create network namespace
        └─> Isolated network environment for the Pod

Step 2: Create veth pair
        └─> Virtual cable with two ends

Step 3: Move veth1 into Pod's namespace
        └─> Now the Pod has its own network interface

Step 4: Attach veth0 to bridge
        └─> Connect to the host's network

Step 5: Assign IP address
        └─> Give the Pod an IP (e.g., 10.244.1.5)

Step 6: Set up routing
        └─> Make sure packets can reach the Pod
```

---

### **CNI Plugin Comparison:**

```
┌─────────────────────────────────────────────────────────┐
│                      FLANNEL                            │
├─────────────────────────────────────────────────────────┤
│ Technology:  VXLAN overlay network                      │
│ Complexity:  Low (easiest to set up)                    │
│ Performance: Good                                       │
│ Features:    Basic networking only                      │
│ Use case:    Simple clusters, getting started           │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                      CALICO                             │
├─────────────────────────────────────────────────────────┤
│ Technology:  BGP routing + eBPF/iptables                │
│ Complexity:  Medium                                     │
│ Performance: Very Good                                  │
│ Features:    Rich NetworkPolicy support                 │
│ Use case:    Production clusters, need good policies    │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                      CILIUM                             │
├─────────────────────────────────────────────────────────┤
│ Technology:  Pure eBPF (kernel-native)                  │
│ Complexity:  Medium-High                                │
│ Performance: Best (O(1) lookups, no iptables)           │
│ Features:    L7 policies, identity-based, Hubble        │
│ Use case:    Large scale, need observability & speed    │
└─────────────────────────────────────────────────────────┘
```

---

## 7️⃣ WHY eBPF? WHY CILIUM?

This is the key question from your whiteboard!

---

### **The Problem with Traditional Networking (iptables):**

```
        With 10,000 Pods in a cluster:
        
┌─────────────────────────────────────────┐
│  iptables rule 1                        │
│  iptables rule 2                        │
│  iptables rule 3                        │
│  ...                                    │
│  iptables rule 9,997                    │
│  iptables rule 9,998                    │
│  iptables rule 9,999                    │  ← Must scan EVERY rule
│  iptables rule 10,000                   │     for EVERY packet!
└─────────────────────────────────────────┘

Every packet must scan ALL rules = O(n)
Slow! Gets worse with more Pods!
```

**Problem:**
- iptables uses a **linear list** of rules
- Every packet scans from top to bottom
- With thousands of Pods = thousands of rules
- Performance gets WORSE as cluster grows

---

### **The eBPF Solution:**

```
        With 10,000 Pods in a cluster:
        
┌─────────────────────────────────────────┐
│                                         │
│         eBPF Hash Map                   │
│                                         │
│    Key: Pod IP    →  Value: Rules      │
│    10.244.1.5     →  identity=1234     │
│    10.244.1.6     →  identity=5678     │
│    ...                                  │
│                                         │
└─────────────────────────────────────────┘

Packet arrives → Hash lookup → O(1) constant time!
No matter if you have 10 Pods or 10,000 Pods!
```

**eBPF advantage:**
- Uses **hash tables** for lookups
- O(1) = constant time, doesn't matter how many Pods
- Dramatically faster at scale

---

### **What is eBPF:**

```
        Traditional Linux Kernel
        
┌─────────────────────────────────────────┐
│         Kernel Code                     │
│    (written in C, compiled in)          │
│                                         │
│    To change = recompile kernel         │
│                 or                      │
│    Write kernel module (risky!)         │
└─────────────────────────────────────────┘
```

```
        With eBPF
        
┌─────────────────────────────────────────┐
│         Kernel Code                     │
│    (original kernel untouched)          │
│                                         │
│    ┌─────────────────────┐             │
│    │  eBPF Program 1     │  ← You write this!
│    │  (runs in kernel)   │  ← Safe, verified
│    └─────────────────────┘  ← Hot-loaded
│                                         │
│    ┌─────────────────────┐             │
│    │  eBPF Program 2     │             │
│    └─────────────────────┘             │
└─────────────────────────────────────────┘
```

**eBPF = Extended Berkeley Packet Filter**

A way to run custom programs **inside the Linux kernel** without:
- Recompiling the kernel
- Rebooting the system
- Risking kernel crashes

**How it works:**
1. Write a small program in C
2. Compile to eBPF bytecode
3. Load it into the kernel
4. Kernel **verifies** it's safe (no infinite loops, no bad memory access)
5. Kernel **JIT-compiles** it to native machine code
6. Runs at **near-native speed**

---

### **Where eBPF Hooks Into the Kernel:**

```
Packet Journey with eBPF:

Physical NIC
    │
    ▼
┌─────────────────────┐
│  XDP Hook           │ ← eBPF can attach here (earliest!)
│  (eXpress Data Path)│    Can drop packets instantly
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  TC Hook            │ ← eBPF can attach here
│  (Traffic Control)  │    Can modify, redirect packets
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Netfilter          │ ← eBPF can attach here
│  (iptables layer)   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Socket Layer       │ ← eBPF can attach here
│                     │    L7 inspection possible!
└─────────────────────┘
```

**eBPF can hook at MULTIPLE points** in the packet's journey:
- **XDP**: Earliest possible, before sk_buff created
- **TC**: After sk_buff, can modify packets
- **Netfilter**: Where iptables normally runs
- **Socket**: Application layer, can inspect HTTP/gRPC

---

## 8️⃣ WHY CILIUM USES eBPF - THE REAL REASON

### **Problem 1: iptables is too slow**

```
Old way (kube-proxy with iptables):

Packet arrives
   │
   ├─> Check iptables rule 1
   ├─> Check iptables rule 2
   ├─> Check iptables rule 3
   ├─> ...
   ├─> Check iptables rule 9,999
   └─> Finally found the rule!
   
Time: O(n) - gets slower with more Pods
```

```
Cilium way (eBPF):

Packet arrives
   │
   └─> eBPF program does hash lookup
       Time: O(1) - always fast!
```

**Result:** Cilium can handle **10-100x more Pods** at the same speed.

---

### **Problem 2: Pod IPs keep changing**

```
Traditional iptables rules:

Rule: Allow traffic from 10.244.1.5 to 10.244.2.8

Problem:
- Pod restarts → New IP: 10.244.1.9
- Old rule still says 10.244.1.5
- Rule is BROKEN!
```

```
Cilium way (Identity-based):

Rule: Allow traffic from identity=1234 to identity=5678

Where:
- identity=1234 = Pods with label app=frontend
- identity=5678 = Pods with label app=backend

When Pod restarts:
- Gets new IP, but SAME identity (labels don't change)
- Rule STILL WORKS!
```

**Result:** Policies survive Pod restarts. No need to update rules.

---

### **Problem 3: Can't see inside HTTP/gRPC**

```
Traditional firewalls:

Can only see:
- Source IP: 10.244.1.5
- Destination IP: 10.244.2.8
- Port: 80
- Protocol: TCP

Can't see:
- Which HTTP method? (GET, POST, DELETE)
- Which URL path? (/api/users, /api/admin)
- Which gRPC method?
```

```
Cilium way (L7 policies):

eBPF can see:
- HTTP method: POST
- URL: /api/users
- Headers
- Response codes

Can enforce:
"Allow only GET /api/public/*
 Block everything else"
```

**Result:** Application-layer security without a service mesh.

---

### **Problem 4: No visibility**

```
Traditional setup:

"Why is Pod A can't reach Pod B?"
"Is the traffic being blocked?"
"Which rule is dropping it?"

Answer: ¯\_(ツ)_/¯  (no easy way to see)
```

```
Cilium way (Hubble):

eBPF records EVERY packet:
- Source: default/frontend-xyz
- Destination: default/backend-abc
- Verdict: FORWARDED
- Identity: 1234 → 5678
- L7: GET /api/users → 200 OK

Real-time flow visibility!
```

**Result:** You can SEE what's happening in your cluster.

---

## 9️⃣ THE COMPLETE FLOW - PUTTING IT ALL TOGETHER

Let me trace ONE packet's complete journey with ALL layers:

```
SENDER (outside world) wants to reach a Pod at 10.244.1.5

Step 1: Packet arrives at Physical NIC
        ├─> NIC writes to DMA buffer
        └─> NIC fires interrupt

Step 2: Kernel receives packet
        ├─> Driver creates sk_buff
        └─> Hands to netif_receive_skb()

Step 3: eBPF program runs (if Cilium installed)
        ├─> Attached at TC hook
        ├─> Checks identity-based policy
        ├─> Does NAT if needed (Service → Pod IP)
        └─> Decides: ALLOW or DROP

Step 4: Packet reaches bridge (br0 or OVS)
        ├─> Bridge looks at destination MAC
        └─> Forwards to correct veth port

Step 5: Packet enters veth0 (host side)
        └─> Magically appears at veth1 (container side)

Step 6: Packet is now in Pod's namespace
        ├─> veth1 is renamed to "eth0" inside Pod
        ├─> Pod's network stack processes it
        └─> Application receives the data!

Throughout: Cilium's eBPF records the flow for Hubble
```

---

## 🎯 SUMMARY - THE KEY POINTS

### **Physical NIC**
- Real hardware, the only actual network card
- All virtual NICs share this one card
- Uses DMA + IRQ to hand packets to kernel

### **Linux Kernel**
- Receives packet via interrupt
- Creates sk_buff (packet container)
- Entry point: `netif_receive_skb()`

### **Three Paths**
1. **PP (Packet Processing)**: Normal kernel stack - good for basic setups
2. **PB (DPDK)**: Bypass kernel - fastest, for extreme performance
3. **PF (eBPF)**: Programmable filter in kernel - modern, flexible

### **veth Pair**
- Virtual cable with two ends
- One end in host namespace, one in container namespace
- How containers get their network interface

### **Bridge / OVS**
- Software switch
- Forwards packets between veth ports
- Linux Bridge = simple, OVS = programmable

### **CNI**
- Standard for how to set up container networking
- Kubernetes calls CNI plugin to do the actual work
- Plugins: Flannel (simple), Calico (good), Cilium (best)

### **Why eBPF / Cilium**
1. **Speed**: O(1) hash lookups vs O(n) iptables
2. **Identity**: Label-based, survives Pod restarts
3. **L7**: Can see inside HTTP/gRPC traffic
4. **Observability**: Hubble shows real-time flows

---


