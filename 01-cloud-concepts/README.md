# Lab 01: Cloud Deployment Models

## Microsoft Azure Fundamentals (AZ-900)

## Module 1: Cloud Concepts

---

# 1. Overview

Cloud deployment models define how cloud infrastructure is hosted, managed, and accessed by organizations.

Organizations choose different deployment models based on:

- Security requirements
- Compliance needs
- Cost considerations
- Scalability requirements
- Business objectives

The four main cloud deployment models are:

1. Public Cloud
2. Private Cloud
3. Hybrid Cloud
4. Multicloud

---

# 2. Lab Objective

By completing this lab, I will understand:

- The differences between cloud deployment models
- The advantages and disadvantages of each model
- When organizations should choose each deployment approach
- How Microsoft Azure supports different deployment strategies

---

# 3. Cloud Deployment Models Overview

| Deployment Model | Description | Example |
|---|---|---|
| Public Cloud | Cloud resources owned and operated by a third-party provider and shared among customers | Microsoft Azure |
| Private Cloud | Dedicated cloud infrastructure used by a single organization | Azure Stack Hub |
| Hybrid Cloud | Combination of private infrastructure and public cloud services | On-premises + Azure |
| Multicloud | Using services from multiple cloud providers | Azure + AWS + Google Cloud |

---

# 4. Public Cloud

## Definition

Public Cloud is a cloud environment where computing resources are owned and managed by a cloud service provider.

Customers share the provider's infrastructure while maintaining isolated environments.

Examples:

- Microsoft Azure
- Amazon Web Services (AWS)
- Google Cloud Platform (GCP)

---

## Characteristics

- Provider-managed infrastructure
- Pay-as-you-go pricing
- High scalability
- Global availability
- No hardware maintenance

---

## Advantages

✅ Lower upfront cost

✅ Rapid deployment

✅ Unlimited scalability

✅ Access to advanced cloud services

---

## Disadvantages

❌ Less physical infrastructure control

❌ Compliance limitations for some industries

---

## Business Scenario

A startup wants to launch a web application globally without purchasing servers.

Solution:

Use Microsoft Azure Virtual Machines, Azure App Service, and Azure Storage.

---

# Public Cloud Architecture

Diagram:

![Public Cloud Architecture](./diagrams/public-cloud.png)

---

# 5. Private Cloud

## Definition

Private Cloud is a cloud environment dedicated to a single organization.

The organization has complete control over infrastructure, security, and management.

Examples:

- Azure Stack Hub
- VMware Private Cloud
- Enterprise Data Centers

---

## Characteristics

- Dedicated infrastructure
- Higher customization
- Greater control
- Suitable for strict compliance requirements

---

## Advantages

✅ Maximum control

✅ Strong security customization

✅ Supports regulatory requirements

---

## Disadvantages

❌ Higher operational cost

❌ Requires skilled IT teams

❌ Limited scalability compared with public cloud

---

## Business Scenario

A government organization needs to store sensitive information while maintaining strict control.

Solution:

Deploy a private cloud environment using Azure Stack Hub.

---

# Private Cloud Architecture

Diagram:

![Private Cloud Architecture](./diagrams/private-cloud.png)

---

# 6. Hybrid Cloud

## Definition

Hybrid Cloud combines private cloud infrastructure with public cloud services.

Organizations can keep sensitive workloads privately while using public cloud resources for scalability.

---

## Characteristics

- Private + Public cloud integration
- Data movement between environments
- Flexible workload placement

---

## Advantages

✅ Balance between security and scalability

✅ Gradual cloud migration

✅ Better workload optimization

---

## Disadvantages

❌ More complex management

❌ Requires integration skills

---

## Business Scenario

A financial company keeps customer databases on-premises but uses Azure for application hosting.

Solution:

Use:

- Azure Virtual Network
- Azure ExpressRoute
- Azure Hybrid Services

---

# Hybrid Cloud Architecture

Diagram:

![Hybrid Cloud Architecture](./diagrams/hybrid-cloud.png)

---

# 7. Multicloud

## Definition

Multicloud is an approach where an organization uses services from multiple cloud providers.

Example:

- Microsoft Azure for identity services
- AWS for application hosting
- Google Cloud for analytics

---

## Characteristics

- Multiple cloud providers
- Workload distribution
- Vendor flexibility

---

## Advantages

✅ Avoids vendor lock-in

✅ Uses best services from different providers

✅ Improves resilience

---

## Disadvantages

❌ Increased complexity

❌ Requires multiple skill sets

❌ More difficult security management

---

## Business Scenario

A global enterprise uses:

- Azure for Microsoft 365 integration
- AWS for customer applications
- Google Cloud for AI workloads

---

# Multicloud Architecture

Diagram:

![Multicloud Architecture](./diagrams/multicloud.png)

---

# 8. Deployment Model Comparison

| Feature | Public Cloud | Private Cloud | Hybrid Cloud | Multicloud |
|-|-|-|-|-|
| Ownership | Cloud Provider | Organization | Shared | Multiple Providers |
| Cost | Low | High | Medium | Variable |
| Scalability | Very High | Limited | High | Very High |
| Control | Medium | High | High | Medium |
| Management Complexity | Low | High | High | Very High |
| Example | Azure | Azure Stack | Azure + On-Prem | Azure + AWS |

---

# 9. Microsoft Azure Perspective

Microsoft Azure supports different deployment strategies:

## Public Cloud

Examples:

- Azure Virtual Machines
- Azure App Service
- Azure Storage


## Private Cloud

Example:

- Azure Stack Hub


## Hybrid Cloud

Examples:

- Azure Arc
- Azure ExpressRoute
- Azure Hybrid Benefit


## Multicloud

Examples:

- Azure Arc-enabled servers
- Azure Lighthouse

---

# 10. Lab Challenge

## Scenario

A healthcare company wants to modernize its infrastructure.

Requirements:

- Patient records must remain controlled
- Applications need global availability
- Company wants to reduce hardware costs

### Challenge:

Which deployment model would you recommend?

Explain your answer.

---

## Answer

Recommended Model:

Hybrid Cloud

Reason:

The organization can keep sensitive patient data in a controlled environment while using Azure public cloud services for application scalability and availability.

---

# 11. Key Learning Points

After completing this lab, I understand:

✔ Public Cloud provides scalable cloud services through providers like Azure.

✔ Private Cloud provides dedicated infrastructure and greater control.

✔ Hybrid Cloud combines private infrastructure with public cloud benefits.

✔ Multicloud allows organizations to use multiple cloud providers.

✔ Azure supports all deployment strategies depending on business requirements.

---

# 12. Lab Status

Completed:

☐ Documentation

☐ Architecture Diagrams

☐ Comparison Analysis

☐ Business Scenario Evaluation


Author:

Collins Ukpe Wisdom

Azure Fundamentals Portfolio
