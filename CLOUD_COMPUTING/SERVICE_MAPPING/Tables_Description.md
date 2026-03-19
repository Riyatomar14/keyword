# Cloud Computing — Tables Study Guide

A complete keyword-based guide to understand all the cloud service classification tables.

---

## Table 1 — PaaS Classification (PaaS-I, PaaS-II, PaaS-III)

### What is PaaS?
**Platform as a Service (PaaS)** — A cloud model where the provider delivers a platform (middleware + sometimes infrastructure) so developers can build and deploy applications without managing the underlying hardware or OS.

### Key Keywords

| Keyword | Meaning |
|---------|---------|
| **PaaS** | Platform as a Service — cloud-hosted development and deployment environment |
| **Middleware** | Software layer between the OS and the application (handles communication, data management, APIs) |
| **Infrastructure** | Physical or virtual hardware — servers, storage, networking |
| **Runtime Environment** | The execution environment where an application runs (e.g. Java, Python runtimes) |
| **Scalability** | Ability of a system to handle growing workloads automatically |
| **Web-hosted IDE** | A browser-based code editor — no local installation needed |
| **Rapid Prototyping** | Quickly building and testing early versions of an application |
| **API (Application Programming Interface)** | A set of rules that allows software components to communicate |
| **Middleware + Infrastructure** | Full-stack PaaS — provides both the software layer AND the hardware layer |
| **Middleware only** | Partial PaaS — provides the software layer but requires separate infrastructure |

### PaaS Categories — Quick Reference

| Category | Core Idea | Example Products |
|----------|-----------|-----------------|
| **PaaS-I** | Browser-based IDE + full stack (Middleware + Infra). Build, design, deploy entirely in the cloud | Force.com, Longjump |
| **PaaS-II** | Scalable runtime for web apps. Developers use provider APIs on top of industrial runtimes | Google AppEngine, Heroku, Engine Yard, Joyent, AppScale |
| **PaaS-III** | Full Cloud programming platform for ANY type of app, not just web apps | Microsoft Azure, Manjrasoft Aneka, Apprenda SaaSGrid, DataSynapse |

### How to Remember PaaS-I vs II vs III

```
PaaS-I   → Narrowest scope  → Browser IDE → Only web/app dev in the Cloud
PaaS-II  → Medium scope     → Scalable web runtime → Websites and web apps
PaaS-III → Widest scope     → Any distributed app → ML, enterprise, microservices
```

---

## Table 2 — PaaS-I, II, III mapped to AWS, GCP, Azure, OpenStack

### Key Keywords

| Keyword | Meaning |
|---------|---------|
| **AWS** | Amazon Web Services — the largest public cloud provider |
| **GCP** | Google Cloud Platform — Google's public cloud |
| **Azure** | Microsoft Azure — Microsoft's public cloud |
| **OpenStack** | Open-source cloud software — used to build private or community clouds |
| **Serverless** | Code runs without managing servers — provider auto-scales (e.g. Lambda, Cloud Functions) |
| **Container** | Lightweight, portable package of an application and its dependencies |
| **Kubernetes** | Open-source system for automating deployment and scaling of containers |
| **Orchestration** | Automated coordination and management of cloud workloads |
| **No-code / Low-code** | Building apps with minimal or no programming (e.g. AppSheet, Power Apps) |
| **Horizon** | OpenStack's web-based dashboard — closest OpenStack equivalent to PaaS-I |
| **Solum** | OpenStack's PaaS layer for application lifecycle management |
| **Murano** | OpenStack's application catalog — deploy pre-packaged apps |
| **Zun** | OpenStack's container service — runs Docker containers |
| **Heat** | OpenStack's orchestration engine — like AWS CloudFormation |
| **Magnum** | OpenStack's service to provision Kubernetes/Swarm clusters |
| **Mistral** | OpenStack's workflow engine — automates multi-step tasks |
| **Sahara** | OpenStack's big data service — runs Hadoop/Spark clusters |

### PaaS mapped to Clouds — Quick Reference

| PaaS Level | AWS | GCP | Azure | OpenStack |
|------------|-----|-----|-------|-----------|
| **PaaS-I** | Amplify Studio, Cloud9, CodeStar | Firebase Studio, AppSheet | Power Apps, Logic Apps | Horizon, Solum, Murano |
| **PaaS-II** | Elastic Beanstalk, Lambda, App Runner | App Engine, Cloud Run, Cloud Functions | App Service, Azure Functions | Zun, Heat, Solum Workflows |
| **PaaS-III** | EKS, ECS, SageMaker | GKE, Vertex AI, Cloud Composer | AKS, Azure ML, Service Fabric | Magnum, Mistral, Sahara |

---

## Table 3 — IaaS and SaaS from Private Cloud and OpenStack

### What is IaaS?
**Infrastructure as a Service (IaaS)** — Provider delivers raw compute, storage, and networking. You manage everything above: OS, middleware, runtime, and apps.

### What is SaaS?
**Software as a Service (SaaS)** — Provider delivers a fully managed, ready-to-use application. You manage nothing — just use the software.

### Key Keywords

| Keyword | Meaning |
|---------|---------|
| **IaaS** | Infrastructure as a Service — raw compute, storage, networking on demand |
| **SaaS** | Software as a Service — fully managed app, just log in and use |
| **Private Cloud** | Cloud infrastructure operated solely for one organization, on-premises or hosted |
| **VMware vSphere / vCenter** | Leading private cloud virtualization platform for compute |
| **VMware NSX** | Software-defined networking for private cloud |
| **Cisco ACI** | Cisco's SDN solution for private datacenters |
| **NetApp / Dell EMC SAN** | Enterprise block/file storage hardware for private clouds |
| **Microsoft Active Directory** | Identity and access management system for private networks |
| **SDN (Software-Defined Networking)** | Networking managed via software rather than physical hardware |
| **SAN (Storage Area Network)** | High-speed network providing block-level storage access |
| **NAS (Network Attached Storage)** | File-level storage accessible over a network |
| **Nova** | OpenStack compute service — provisions and manages VMs |
| **Neutron** | OpenStack networking service — virtual networks, subnets, routers |
| **Cinder** | OpenStack block storage service (like a virtual hard drive) |
| **Swift** | OpenStack object storage service (like AWS S3) |
| **Manila** | OpenStack shared file system service |
| **Keystone** | OpenStack identity service — authentication and authorization |
| **Octavia** | OpenStack load balancer service |
| **Nextcloud** | Open-source file sharing and collaboration platform (like Google Drive) |
| **Zabbix / Nagios** | Open-source monitoring tools for private infrastructure |
| **GitLab CE** | Self-hosted open-source DevOps and CI/CD platform |
| **Ceilometer** | OpenStack telemetry service — collects usage metrics |
| **Gnocchi** | OpenStack metric storage — stores time-series data from Ceilometer |
| **Jenkins** | Open-source CI/CD automation server |
| **Apache Superset** | Open-source BI and data visualization tool |

### IaaS Private Cloud vs OpenStack — Quick Reference

| Component | Private Cloud | OpenStack |
|-----------|--------------|-----------|
| **Compute** | VMware vSphere / vCenter | Nova |
| **Storage** | NetApp / Dell EMC SAN | Cinder + Swift + Manila |
| **Networking** | Cisco ACI / VMware NSX | Neutron + Octavia |
| **Identity** | Microsoft Active Directory | Keystone |

### SaaS Private Cloud vs OpenStack — Quick Reference

| Component | Private Cloud | OpenStack |
|-----------|--------------|-----------|
| **Collaboration** | Microsoft Exchange + SharePoint | Nextcloud on OpenStack |
| **Monitoring** | Zabbix / Nagios | Ceilometer + Gnocchi |
| **CI/CD** | GitLab CE (self-hosted) | Jenkins on Nova VMs |
| **Analytics / BI** | Tableau Server (on-prem) | Apache Superset on Sahara |

---

## Table 4 — IaaS and SaaS from Public Cloud (AWS, GCP, Azure)

### Key Keywords

| Keyword | Meaning |
|---------|---------|
| **EC2** | Elastic Compute Cloud — AWS's virtual machine service |
| **Compute Engine (GCE)** | GCP's virtual machine service |
| **Azure VMs** | Azure's virtual machine service |
| **S3** | Simple Storage Service — AWS object storage |
| **EBS** | Elastic Block Store — AWS block storage (virtual hard disk for EC2) |
| **EFS** | Elastic File System — AWS managed shared file storage |
| **GCS** | Google Cloud Storage — GCP object storage |
| **Persistent Disk** | GCP's block storage service |
| **Blob Storage** | Azure object storage |
| **VPC** | Virtual Private Cloud — isolated virtual network in the cloud |
| **VNet** | Azure's Virtual Network |
| **Route 53** | AWS DNS service |
| **CloudFront** | AWS Content Delivery Network (CDN) |
| **ELB** | Elastic Load Balancer — AWS load balancing service |
| **Front Door** | Azure CDN and global load balancer |
| **AWS IAM** | Identity and Access Management — controls who can do what in AWS |
| **Cloud IAM** | GCP's resource-level access control |
| **Entra ID / Azure AD** | Azure's identity and SSO platform (formerly Active Directory) |
| **RDS** | Relational Database Service — AWS managed SQL database |
| **DynamoDB** | AWS managed NoSQL database |
| **Cloud SQL** | GCP managed relational database |
| **Firestore** | GCP managed NoSQL document database |
| **Cosmos DB** | Azure globally distributed multi-model database |
| **Amazon WorkMail** | AWS managed email and calendar service |
| **SES** | Simple Email Service — AWS transactional email delivery |
| **Google Workspace** | GCP SaaS suite — Gmail, Meet, Drive, Docs |
| **Microsoft 365** | Azure SaaS suite — Outlook, Teams, OneDrive, Word |
| **QuickSight** | AWS managed BI and dashboard service |
| **Looker** | GCP enterprise BI platform |
| **Power BI** | Microsoft managed BI and reporting tool |
| **Rekognition** | AWS AI service for image and video analysis |
| **Cloud Vision API** | GCP AI service for image recognition |
| **Azure AI Services** | Azure suite of cognitive and OpenAI-powered APIs |
| **CloudWatch** | AWS monitoring service — metrics, logs, and alerts |
| **Cloud Monitoring** | GCP observability and monitoring service |
| **Azure Monitor** | Azure monitoring — logs, alerts, dashboards |

### IaaS Public Cloud — Quick Reference

| Component | AWS | GCP | Azure |
|-----------|-----|-----|-------|
| **Compute** | EC2 | Compute Engine | Azure VMs |
| **Object Storage** | S3 | Cloud Storage | Blob Storage |
| **Block Storage** | EBS | Persistent Disk | Managed Disk |
| **File Storage** | EFS | Filestore | Azure Files |
| **Networking** | VPC + Route53 + CloudFront + ELB | VPC + Cloud DNS + Cloud CDN + LB | VNet + DNS + Front Door + LB |
| **Identity** | AWS IAM | Cloud IAM | Azure AD / Entra ID |

### SaaS Public Cloud — Quick Reference

| Component | AWS | GCP | Azure |
|-----------|-----|-----|-------|
| **Managed DB** | RDS + DynamoDB | Cloud SQL + Firestore | Azure SQL + Cosmos DB |
| **Email / Comms** | WorkMail + SES | Google Workspace | Microsoft 365 |
| **Analytics / BI** | QuickSight | Looker | Power BI |
| **AI / ML APIs** | Rekognition | Cloud Vision + NL API | Azure AI Services |
| **Monitoring** | CloudWatch | Cloud Monitoring | Azure Monitor |

---

## Master Comparison — IaaS vs PaaS vs SaaS

```
┌──────────┬────────────────────────────────────────────────────────┐
│  Model   │  What YOU manage                                       │
├──────────┼────────────────────────────────────────────────────────┤
│  IaaS    │  OS → Middleware → Runtime → App → Data               │
│  PaaS    │  App → Data  (provider manages OS + Middleware)        │
│  SaaS    │  Nothing  (provider manages everything)                │
└──────────┴────────────────────────────────────────────────────────┘
```

### Private Cloud vs Public Cloud vs OpenStack

| Aspect | Private Cloud | Public Cloud (AWS/GCP/Azure) | OpenStack |
|--------|--------------|------------------------------|-----------|
| **Ownership** | Organization owns hardware | Provider owns hardware | Organization owns hardware |
| **Cost model** | CapEx (upfront) | OpEx (pay-as-you-go) | CapEx + setup cost |
| **Scalability** | Limited by own hardware | Virtually unlimited | Limited by own hardware |
| **Control** | Full control | Limited control | Full control |
| **Software** | Proprietary (VMware, Cisco) | Proprietary (AWS, GCP, Azure) | Open-source |
| **Best for** | Security-sensitive workloads | Scalable, global apps | Custom cloud on open-source |

---

*Study Tip: Remember the progression — IaaS gives you bricks, PaaS gives you a workshop, SaaS gives you a finished product.*
