# Lab 05: Azure Landing Zone Architecture

## Module

Module 2 — Azure Architecture


## Lab Overview

This lab introduces the concept of an Azure Landing Zone and explains how organizations design a scalable, secure, and governed Azure environment before deploying production workloads.

An Azure Landing Zone provides a foundation that enables organizations to establish:

- Identity management
- Governance controls
- Network architecture
- Security practices
- Subscription organization
- Operational processes

A Landing Zone is not a single Azure service. It is an architectural approach that combines multiple Azure capabilities into a structured enterprise environment.


## Learning Objectives

By completing this lab, you will understand:

- What an Azure Landing Zone represents
- Why organizations establish landing zones
- How subscriptions are organized for enterprise environments
- How governance and security are integrated into architecture
- How networking supports enterprise workloads
- How landing zones support scalability and operational consistency


## Architecture Overview

A well-designed Azure Landing Zone creates a foundation where workloads can be deployed securely and consistently.

The architecture typically includes:

- Microsoft Entra ID for identity
- Management groups for governance structure
- Subscriptions for workload separation
- Shared services
- Centralized networking
- Security controls
- Application workload environments


The following diagram illustrates an enterprise Azure Landing Zone architecture:

![Azure Landing Zone Architecture](./diagrams/azure-landing-zone-architecture.png)


## Services Used

This conceptual architecture includes:

- Microsoft Entra ID
- Azure Management Groups
- Azure Subscriptions
- Azure Virtual Network
- Azure Firewall
- Azure Monitor
- Azure Policy
- Azure RBAC
- Azure Security services


## Landing Zone Architecture Components


## Identity Foundation

Microsoft Entra ID provides the identity foundation for Azure environments.

Organizations manage:

- Users
- Groups
- Applications
- Access control


Identity should follow:

- Least privilege
- Separation of duties
- Strong authentication practices


---

## Management Group Structure

Management groups provide an organizational structure for subscriptions.

Example:
Tenant

|
|
Management Groups

├── Platform
│
├── Landing Zones
│
├── Sandbox
│
└── Decommissioned


Management groups allow organizations to apply governance consistently.


---

## Subscription Design

Subscriptions provide boundaries for:

- Billing
- Access
- Governance
- Workload separation


Example:
Production Subscription

Development Subscription

Security Subscription

Connectivity Subscription


Different subscriptions can have different ownership and security requirements.


---

## Network Foundation

Enterprise environments commonly use centralized networking.

Example:
          Hub Network

   Firewall
   VPN Gateway
   Shared Services

          |
  -----------------

  |       |       |
  Spoke1 Spoke2 Spoke3

Apps Apps Apps



The hub provides shared connectivity and security services.

The spokes contain application workloads.


---

## Governance Foundation

Governance controls ensure Azure resources follow organizational standards.

Common controls include:

- Azure Policy
- RBAC
- Resource Tags
- Resource Locks


Examples:

- Restrict approved Azure regions
- Require resource tags
- Control administrative access
- Protect critical resources


---

## Security Foundation

Security is integrated into the landing zone design.

Security considerations include:

- Identity protection
- Network security
- Monitoring
- Threat detection
- Compliance requirements


Security should be designed before workload deployment.


---

## Implementation Steps


### Step 1 — Understand Business Requirements

Identify:

- Workload requirements
- Compliance requirements
- Security requirements
- Operational responsibilities


Architecture decisions should align with business objectives.


---

### Step 2 — Design Azure Organization Structure

Define:

- Management groups
- Subscription strategy
- Ownership boundaries


The structure should support future growth.


---

### Step 3 — Establish Governance Controls

Define:

- Azure Policies
- RBAC model
- Naming standards
- Tagging strategy


Governance should provide guardrails without preventing productivity.


---

### Step 4 — Design Network Architecture

Define:

- Hub-spoke design
- Connectivity requirements
- Security inspection points
- Network segmentation


Network architecture should support both security and scalability.


---

### Step 5 — Prepare Operational Management

Define:

- Monitoring strategy
- Backup approach
- Security monitoring
- Incident response processes


A landing zone should support ongoing operations after deployment.


---

## Verification

Confirm understanding by explaining:

- Why organizations use Azure Landing Zones
- How landing zones combine governance and architecture
- Why subscription design matters
- How networking supports enterprise workloads
- Why security should be designed from the beginning


## Security Considerations

A landing zone applies security principles before workloads are deployed.

Important considerations:

- Identity-first security
- Least privilege access
- Network segmentation
- Policy enforcement
- Security monitoring
- Compliance management


Security should be integrated into architecture rather than added later.


## Cost Considerations

Landing zone design influences cost management.

Organizations should consider:

- Subscription structure
- Resource ownership
- Monitoring costs
- Security service costs
- Network service costs


Good architecture improves cost visibility and prevents uncontrolled resource growth.


## Key Takeaways

An Azure Landing Zone provides an enterprise-ready foundation for cloud adoption.

It combines:

- Identity
- Governance
- Security
- Networking
- Operations

A well-designed landing zone allows organizations to scale Azure environments while maintaining control, security, and consistency.


## References

Azure Landing Zone Documentation:

https://learn.microsoft.com/azure/cloud-adoption-framework/ready/landing-zone/

Azure Well-Architected Framework:

https://learn.microsoft.com/azure/well-architected/
