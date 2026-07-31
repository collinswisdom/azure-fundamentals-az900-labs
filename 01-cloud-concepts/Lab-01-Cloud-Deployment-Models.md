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


### Characteristics

### Real-World Example

---

## Hybrid Cloud

### Definition

### Characteristics

### Real-World Example

---

## Multicloud

### Definition

### Characteristics

### Real-World Example

---

# Comparison Table

| Model | Infrastructure Owner | Best For | Example |
|--------|----------------------|----------|----------|
| Public Cloud | | | |
| Private Cloud | | | |
| Hybrid Cloud | | | |
| Multicloud | | | |

---

# Key Takeaways

-

-

-

---

# AZ-900 Exam Notes

-

-

-

---

# Conclusion

This lab introduced the four cloud deployment models used in cloud computing and explained how organizations choose between them based on cost, scalability, compliance, and business requirements.
