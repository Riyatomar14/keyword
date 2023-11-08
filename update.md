## computer is divided into three parts-

# 1.computation 

 **CPU,GPU,TPU**

**OPERATING SYSTEM**
a.Windows
b.MacOS

**KERNEL**--that manages operations between computer and hardware.

**host**-basically a bare metal(server with no operating system)

**VM(virtual machine)**-virtualization

  type-1 (server with no operating system) ex:XEN,KVM

  type-2 (server with operating system) EX: VM WARE,ORACLE

**CONTAINER**
  -Docker container
  -linux container(LXC)

  ORCHESTRATION CONTAINERS(manage service with container)
  
  -KUBERNETES(K8S)
  
  -DOCKER SWARM
  
  -MESOS
  
  -EKS(Amazon Elastic Kubernetes Service)
  
  -ECS(Elastic container service)  
  
  **user space and kernel space**

  **eBPF** 

  **DUAL BOOT**

   **IAAS**

  **KAAS**

  **RANCHER**

  **MESOS**

  **FPGA**

# 2.networking

**SWICH**-hardware

**open Vswitch OR OVS**-software

**LOAD BALANCER**-help to overcome the traffic

**SMART NICS**-

  DPDK-transfer TCP packets from operating system kernel to processing running space in user space.
  
  SR-IOV-allows a device, such as a network adapter, to separate access to its resources among various PCIe hardware functionsand help in optimization gives efficiency.
  
**proxy and reverse proxy**

**NAT**

**routing**

**ROUTE 53(DNS)**

**DNS**

**LAYER 4** (TCP AND UDP)
 
**CNI**-EX:FUNNEL,CALICO

**DHCP (Dynamic Host Configuration Protocol)**- a network management protocol used to dynamically assign an IP address to any device, or node, on a network so it can communicate using IP.

**HASHING**

**LAYER 7** (PRESENTATION AND DATA LINK)-it is best for load balancing of HTTP and HTPPS.

**SWITCH**

**TUN**

**OSI LAYER**

 L7 PHYSICAL

 L6 DATA LINK
 
 L5 NETWORK 
 
 L4 TRANSPORT
 
 L3 SESSION
 
 L2 PRESENTATION

 L1 APPLICATION 

**IP ADDRESS** -INTERNET PROTOCOL(IPv4,IPv6)

  Public IP- ex:starts with 11..
 
  Private IP-10. ,172. ,192. . 

  Local IP-ex:starts with 127.0.00[a specific number]

**PORT NUMBER**-

eg:HTTP-80

HTTPS-443

FTP-20,21

SMTP-25

TELMET-23

SSH[secure shell]-22

**DNS** (turns domain name into IP address)

> # CDN(content delievery network)
A content delivery network (CDN) is a group of geographically distributed servers that speed up the delivery of web content by bringing it closer to where users are.

> SNOWBALL
  it is a way of trransferring the data physically.

**ping**

**NIC**

**ethernet**

**tap(temporary applicant pool)**

**API**

**rest api**

# 3.storage 
 
**block storage** ex:EBS

**OBJECT STORAGE** ex:S3

 **db**-HELP TO MANAGE SERVICES

 **caching** ex:redish

**RAM**

**ROM**

**OPTICAL DISK**

**HDD(hard disk drive)**

**SSD(Solid State Drive)**-new generation of storage device 

**SHARDING**- process of storing a large database across multiple machines. a type of database partitioning that separates large databases into smaller, faster, more easily managed parts.

**CEPH**

**ETCD**-etcd stores data in a multiversion persistent key-value store.

## architecture

**api gateway**- act as mediator between server and client.

**ELK STACK**-it is a open source and combination of elasticsearch,logstack and kiibana . it is alog management platform that provide centralized logging to identity the problems with users.

**prometheus and grafana** opensource tools for application monitoring and analysis. 

**Von Neumann architecture**

**harvard architecture**

**ISA(INSTRUCTION SET ARCHITECURE)**-defines how the CPU is controlled by the software.

**CISC**- COMPLEX INSTRUCTION SET COMPUTER - CLOSED SOURCE-INTEL,AMD

**RISC**- REDUCED INSTRUCTION SET COMPUTER - CLOSED SOURCE -ARM

  RISC V 
  
## SYSTEM DESIGN 

**MQTT(MESSAGE QUEING TELEMETRY TRANSPORT)**- SMART SENSORS AND OTHER INTERNET OF THINGS(IOT).it is basicallly a messaging protocol.

**PUB-SUB (PUBLISH/SUBSCRIBER)**- USED TO DISTRIBUTE SERVICE

**SQL**-manage the permission on server.it is structured database and having predifed schema.

**NOSQL(NOT ONLY SQL)**- it is unstructured and having dynamic schema.

**CAP THEOREM**-it gave guarantee of only two characterstics: availabity,consistencyand partition tolerance.

## PROPERTIES
**AUTO SCALING**

**reliability**

**HA(HIGH AVAILABILITY)**

**REDUDANCY**

**SECURITY**
  **ZERO TRUST SECURITY** (ZTS) 
  
  **ZERO TOUCH PROVISIONING** (ZTP)

  **HTTPS**

  **SSL(SECURE SOCKET LAYER)**- STANDARD FORM-X.509 
                                ex: caddy

  **BGP(BORDER GATEWAY PROTOCOL)**-USE TO EXCHANGE ROUTING INFORMATION BETWEEN AUTONOMOUS SYSTEM(AS)

## CONCEPT
**RABBIT MQ**(message-queueing software)-OPENSTACK

**RAFT** AND **ROUND-ROBIN**-LOAD BALANCER


