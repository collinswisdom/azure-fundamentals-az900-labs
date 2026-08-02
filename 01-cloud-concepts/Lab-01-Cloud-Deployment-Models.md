# Lab 01 – Cloud Deployment Models

## Lab Information

| Item | Details |
|------|---------|
| Module | Cloud Concepts |
| Lab | 01 |
| Topic | Cloud Deployment Models |
| Azure Service | Azure Fundamentals |
| Status | Completed |

---

# Objective

Understand the four cloud deployment models and identify when each model should be used.

---

# Learning Outcomes

By completing this lab, I can:

- Explain Public Cloud
- Explain Private Cloud
- Explain Hybrid Cloud
- Explain Multicloud
- Identify business scenarios for each model

---

# Cloud Deployment Models

## Public Cloud

### Definition

A Public Cloud is a cloud computing environment where the cloud provider owns, operates, and maintains the infrastructure. Customers access computing resources such as virtual machines, storage, databases, and networking services over the internet on a pay-as-you-go basis.

Microsoft Azure is an example of a public cloud platform.

### Characteristics


- Infrastructure is owned and managed by the cloud provider.
- Resources are accessed over the internet.
- Multiple customers (tenants) share the same physical infrastructure while remaining logically isolated.
- Highly scalable and elastic.
- Pay only for the resources you use.


### Real-World Example

KollraX wants to host its website and customer portal without purchasing physical servers.

Instead of building a data center, KollraX deploys an Azure App Service and an Azure SQL Database in Microsoft Azure.

Microsoft manages the hardware, networking, power, cooling, and physical security, while KollraX manages its application and data.

### Architecture Diagram

```text
                 Internet
                      │
                      ▼
             Microsoft Azure
     ┌──────────────────────────┐
     │      Azure Services      │
     │  • Virtual Machines      │
     │  • App Service           │
     │  • Storage               │
     │  • SQL Database          │
     └──────────────────────────┘
          ▲        ▲        ▲
          │        │        │
     KollraX   School   Bank
```

## Private Cloud

### Definition

A Private Cloud is a cloud computing environment that is dedicated to a single organization. Unlike a Public Cloud, the infrastructure is not shared with other customers. The organization may host the infrastructure in its own data center or have it hosted by a third-party provider, but the resources are exclusively reserved for that organization.


### Characteristics

- Dedicated to a single organization.
- Greater control over infrastructure and security.
- Supports strict compliance and regulatory requirements.
- Higher operational and maintenance costs.
- Can be hosted on-premises or by a third-party provider.

### Real-World Example

A financial institution processes highly sensitive customer data and must comply with strict regulatory requirements. To maintain full control over its infrastructure, networking, and security policies, it deploys its workloads in a Private Cloud environment that is dedicated exclusively to the organization.

### Advantages

- Full control over infrastructure.
- Enhanced security and privacy.
- Easier to meet regulatory and compliance requirements.
- Customizable hardware and software configurations.
- Predictable performance because resources are not shared.

## Hybrid Cloud

### Definition

A Hybrid Cloud is a cloud computing model that combines an organization's on-premises infrastructure (or private cloud) with a public cloud such as Microsoft Azure. This allows applications, data, and workloads to move between both environments based on business, security, compliance, and performance requirements.


### Characteristics

- Combines on-premises infrastructure with a public cloud.
- Enables workloads to run in the most appropriate environment.
- Supports gradual cloud adoption.
- Provides flexibility for disaster recovery and backup.
- Helps organizations meet security and compliance requirements.


## Multicloud

### Definition
Multicloud is a cloud computing strategy in which an organization uses services from two or more cloud providers instead of relying on just one.

### Characteristics

Uses services from two or more cloud providers (e.g., AWS, Azure, Google Cloud).
Each provider is selected based on its strengths or business needs.
Applications and services are spread across different clouds.
For example, one cloud hosts web applications while another handles analytics.
Reduces dependence on a single cloud provider.
Makes it easier to switch providers or add new ones without disrupting the entire environment.


# Conclusion

This lab introduced the four cloud deployment models used in cloud computing and explained how organizations choose between them based on cost, scalability, compliance, and business requirements.
