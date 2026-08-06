# Lab 02: Cloud Computing Overview

## Module

Module 1 — Cloud Concepts


## Lab Overview

This lab explores the fundamentals of cloud computing and how organizations consume cloud services.

The objective is to understand the cloud computing operating model, including how cloud providers deliver computing resources, how customers consume services, and how responsibilities are shared between the cloud provider and the customer.

Cloud computing has transformed traditional IT by allowing organizations to access scalable computing resources without owning and maintaining physical infrastructure.


## Learning Objectives

By completing this lab, you will understand:

- What cloud computing is
- How cloud service providers deliver resources
- The benefits of cloud computing
- Cloud service models:
  - Infrastructure as a Service (IaaS)
  - Platform as a Service (PaaS)
  - Software as a Service (SaaS)

- The shared responsibility model between Microsoft Azure and customers


## Architecture Overview

Traditional IT requires organizations to purchase, maintain, and manage physical infrastructure.

Cloud computing introduces a consumption-based model where organizations consume computing resources from cloud providers.

In Microsoft Azure:

- Microsoft manages the physical datacenters
- Microsoft manages the underlying cloud infrastructure
- Customers manage their applications, configurations, and data

The level of responsibility depends on the service model being used.

The following diagram illustrates the relationship between cloud consumers, Microsoft Azure infrastructure, and the shared responsibility model:

[Cloud Computing Overview](./diagram/cloud-computing-overview1.png)

## Implementation Steps

### Step 1 — Understand Cloud Computing

Cloud computing provides on-demand access to computing resources through the internet.

These resources include:

- Compute power
- Storage
- Networking
- Databases
- Applications


### Step 2 — Understand Cloud Service Models

## Infrastructure as a Service (IaaS)

The customer manages:

- Operating system
- Applications
- Data
- Configuration

Examples:

- Azure Virtual Machines


## Platform as a Service (PaaS)

The cloud provider manages:

- Infrastructure
- Operating system
- Runtime environment

Customers focus on:

- Applications
- Data

Examples:

- Azure App Service


## Software as a Service (SaaS)

The provider manages the entire application platform.

Customers consume the finished service.

Examples:

- Microsoft 365


### Step 3 — Understand Shared Responsibility

Cloud security is a partnership between Microsoft and customers.

Microsoft is responsible for:

- Physical datacenters
- Hardware
- Azure infrastructure
- Global network


Customers are responsible for:

- Identity management
- Data protection
- Access control
- Application security


## Verification

The concepts in this lab can be verified by explaining:

- The difference between IaaS, PaaS, and SaaS
- Which responsibilities belong to Microsoft
- Which responsibilities belong to customers


## Security Considerations

Cloud adoption does not remove security responsibilities.

Organizations must implement:

- Identity protection
- Strong authentication
- Least privilege access
- Data protection controls
- Security monitoring


## Cost Considerations

Cloud computing follows a consumption-based pricing model.

Organizations should consider:

- Resource utilization
- Right-sizing workloads
- Removing unused resources
- Selecting appropriate service models


## Key Takeaways

Cloud computing provides organizations with scalable and flexible IT services.

Understanding cloud service models and shared responsibility is essential for designing secure Azure environments.

These concepts form the foundation for Azure administration, security engineering, and cloud architecture.


## References

Microsoft Azure Cloud Concepts Documentation:

https://learn.microsoft.com/azure/cloud-adoption-framework/
