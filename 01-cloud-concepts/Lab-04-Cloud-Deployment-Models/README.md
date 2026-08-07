# Lab 04: Cloud Deployment Models

## Module

Module 1 — Cloud Concepts


## Lab Overview

This lab explores the different cloud deployment models used by organizations:

- Public Cloud
- Private Cloud
- Hybrid Cloud
- Multi-Cloud

Cloud deployment models define where cloud resources are hosted, who manages the infrastructure, and how organizations consume cloud services.

Understanding deployment models is essential for designing secure and scalable enterprise cloud environments.


## Learning Objectives

By completing this lab, you will understand:

- Differences between public, private, hybrid, and multi-cloud environments
- When organizations use each deployment model
- Advantages and challenges of each model
- How Microsoft Azure supports enterprise cloud strategies


## Architecture Overview

Organizations choose cloud deployment models based on business requirements, security needs, and operational constraints.

### Public Cloud

Resources are hosted by a cloud provider and shared across multiple customers.

Example:

- Microsoft Azure

The cloud provider manages the underlying infrastructure while customers manage their workloads.


### Private Cloud

Cloud infrastructure is dedicated to a single organization.

Private cloud provides greater control and customization but requires more management responsibility.


### Hybrid Cloud

Hybrid cloud combines:

- Public cloud resources
- Private infrastructure

Organizations use hybrid models when they need to maintain existing systems while adopting cloud services.


### Multi-Cloud

Multi-cloud uses services from multiple cloud providers.

Example:

- Microsoft Azure
- Amazon Web Services
- Google Cloud Platform

Organizations may use multi-cloud strategies for flexibility, risk reduction, or specialized services.


The following diagram illustrates different cloud deployment models:

![Cloud Deployment Models](./diagrams/cloud-deployment-models.png)


## Services Used

Azure services supporting deployment models include:

- Microsoft Azure Virtual Machines
- Azure Virtual Network
- Azure VPN Gateway
- Azure ExpressRoute
- Azure Arc


## Implementation Steps


### Step 1 — Understand Public Cloud

Public cloud provides shared cloud infrastructure managed by a cloud provider.

Characteristics:

- On-demand resources
- Consumption-based pricing
- High scalability
- Minimal physical infrastructure management


Azure example:

Microsoft Azure


---

### Step 2 — Understand Private Cloud

Private cloud provides dedicated infrastructure controlled by one organization.

Characteristics:

- Greater control
- Custom security requirements
- Higher operational responsibility


Example:

Azure Stack


---

### Step 3 — Understand Hybrid Cloud

Hybrid cloud connects existing infrastructure with cloud resources.

Common use cases:

- Data center migration
- Disaster recovery
- Regulatory requirements


Azure examples:

- Azure VPN Gateway
- Azure ExpressRoute
- Azure Arc


---

### Step 4 — Understand Multi-Cloud

Multi-cloud allows organizations to use multiple cloud providers.

Benefits:

- Avoid vendor dependency
- Use specialized services
- Improve resilience


Challenges:

- Increased complexity
- Different security models
- Additional management overhead


## Verification

Confirm understanding by explaining:

- When an organization would choose hybrid cloud
- Why some companies use private cloud
- The advantages and challenges of multi-cloud strategies


## Security Considerations

Each deployment model introduces different security responsibilities.

Public Cloud:

- Identity protection
- Access control
- Data security


Private Cloud:

- Infrastructure security
- Patch management
- Physical security


Hybrid Cloud:

- Secure connectivity
- Identity synchronization
- Network segmentation


Multi-Cloud:

- Consistent security policies
- Centralized monitoring
- Access governance


## Cost Considerations

Deployment models affect cost differently.

Public Cloud:

- Lower upfront investment
- Pay-as-you-use pricing


Private Cloud:

- Higher infrastructure costs
- Increased maintenance responsibility


Hybrid Cloud:

- Balanced approach
- Requires integration investment


Multi-Cloud:

- Potential optimization
- Increased management complexity


## Key Takeaways

Cloud deployment models define how organizations adopt cloud technology.

A cloud architect must evaluate security, cost, compliance, and business requirements before selecting a deployment strategy.


## References

Microsoft Cloud Adoption Framework:

https://learn.microsoft.com/azure/cloud-adoption-framework/
