# Lab 02 — Azure Virtual Machine Scale Sets

## Overview

This lab demonstrates the deployment and configuration of an Azure Virtual Machine Scale Set (VMSS) running Ubuntu Linux.

The lab focuses on understanding how multiple virtual machine instances can be deployed as a scalable compute platform and placed behind an Azure Standard Load Balancer for high availability and traffic distribution.

The environment was configured with:

- Azure Virtual Machine Scale Set
- Azure Virtual Network and subnet
- Network Security Group
- Azure Standard Load Balancer
- Load Balancer frontend configuration
- Backend address pool
- Health probe
- Load-balancing rule
- Load Balancer outbound rule
- Nginx web server
- VMSS autoscaling

The lab also includes connectivity testing and troubleshooting of outbound Internet access from the VMSS instances.

## Objectives

The objectives of this lab were to:

1. Deploy an Azure Virtual Machine Scale Set.
2. Configure a dedicated virtual network and subnet.
3. Configure network security controls using an NSG.
4. Configure autoscaling for the VMSS.
5. Deploy an Azure Standard Load Balancer.
6. Configure a backend pool for the VMSS instances.
7. Configure a health probe to monitor backend availability.
8. Configure a load-balancing rule for HTTP traffic.
9. Configure outbound Internet connectivity for the VMSS instances.
10. Install and configure Nginx on the VMSS instances.
11. Validate traffic distribution across multiple VMSS instances.
12. Troubleshoot and resolve outbound connectivity issues.

## Architecture

The lab uses an Azure Virtual Machine Scale Set behind an Azure Standard Load Balancer.

Internet-facing traffic enters through the Load Balancer's public IP address. The Load Balancer uses a frontend configuration and load-balancing rule to forward traffic to healthy VMSS instances in the backend pool.

Each VMSS instance runs Nginx and listens on TCP port 80.

### Architecture Diagram

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/4fa42e62-374f-48ac-baa0-c51571395624" />

## Resource Configuration

The lab was deployed in the following Azure resource group:

| Resource | Name | Configuration / Purpose |
|---|---|---|
| Resource Group | `rg-vmss-lab` | Contains the resources used for the VMSS lab |
| Virtual Machine Scale Set | `vmss-app-lab` | Provides scalable Ubuntu Linux VM instances |
| Virtual Network | `vnet-vmss-lab` | Provides the private network for the VMSS |
| Subnet | `snet-app` | Hosts the VMSS instances |
| Network Security Group | `nsg-vmss-lab` | Controls inbound and outbound network traffic |
| Load Balancer | `lb-vmss-app` | Distributes inbound traffic across healthy VMSS instances |
| Public IP | `lb-vmss-app-publicip` | Provides the public entry point to the Load Balancer |
| Backend Pool | `bepool` | Contains the VMSS backend resources |
| Health Probe | `lb-vmss-app-probe01` | Checks backend availability on TCP port 80 |
| Load Balancing Rule | `lb-vmss-app-lbrule01` | Maps frontend TCP port 80 to backend TCP port 80 |
| Outbound Rule | `outbound-vmss-internet` | Provides outbound Internet connectivity for VMSS instances |

### Network Configuration

| Component | Value |
|---|---|
| Virtual Network | `vnet-vmss-lab` |
| Address Space | `10.10.0.0/16` |
| Subnet | `snet-app` |
| Subnet Address Range | `10.10.1.0/24` |
| Network Security Group | `nsg-vmss-lab` |
| NAT Gateway | None |

### Load Balancer Configuration

| Setting | Value |
|---|---|
| Name | `lb-vmss-app` |
| SKU | Standard |
| Frontend Configuration | `lb-vmss-app-frontendconfig01` |
| Public IP | `lb-vmss-app-publicip` |
| Backend Pool | `bepool` |
| Load Balancing Rule | `lb-vmss-app-lbrule01` |
| Frontend Port | 80 |
| Backend Port | 80 |
| Protocol | TCP |
| Health Probe | `lb-vmss-app-probe01` |
| Probe Protocol | TCP |
| Probe Port | 80 |
| Outbound Rule | `outbound-vmss-internet` |
| Outbound Protocol | All |
| Idle Timeout | 15 minutes |
| TCP Reset | Enabled |
