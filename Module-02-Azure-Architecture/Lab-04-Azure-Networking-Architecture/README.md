# Lab 04: Azure Networking Architecture

## Module

Module 2 — Azure Architecture


## Lab Overview

This lab introduces the architectural principles used to design networking environments in Microsoft Azure.

Azure networking provides the connectivity layer that allows applications, users, services, and on-premises environments to communicate securely.

A well-designed Azure network should consider:

- Network segmentation
- Address planning
- Connectivity
- Security boundaries
- Routing
- Availability
- Scalability

This lab focuses on architectural decisions rather than detailed service configuration.


## Learning Objectives

By completing this lab, you will understand:

- The purpose of an Azure Virtual Network
- How subnets provide network segmentation
- How network security controls protect workloads
- The difference between public and private connectivity
- Why IP address planning matters
- How hub-and-spoke architecture can support enterprise environments


## Architecture Overview

An Azure Virtual Network (VNet) provides a logical network boundary for Azure resources.

Subnets divide the VNet into smaller network segments.

A typical enterprise architecture may separate:

- Application workloads
- Databases
- Shared services
- Network infrastructure

Network security controls can then be applied to control traffic between these segments.

The following diagram illustrates a conceptual Azure enterprise network:

![Azure Networking Architecture](./diagrams/azure-networking-architecture.png)


## Services Used

This conceptual architecture discusses:

- Azure Virtual Network
- Azure Subnets
- Network Security Groups
- Azure Firewall
- Azure VPN Gateway
- Azure ExpressRoute
- Azure Load Balancer


## Implementation Steps

### Step 1 — Define the Network Boundary

Create an Azure Virtual Network to provide the logical network boundary for workloads.

The VNet should use an appropriately planned private IP address range.

Example:

```text
10.10.0.0/16
