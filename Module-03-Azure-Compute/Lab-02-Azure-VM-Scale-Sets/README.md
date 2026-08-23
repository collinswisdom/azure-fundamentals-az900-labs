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

## VMSS Configuration

The Virtual Machine Scale Set was configured to deploy multiple Ubuntu Linux instances using a common VM configuration.

| **Setting**            | **Value**               |
| ---------------------- | ----------------------- |
| VMSS Name              | `vmss-app-lab`          |
| Operating System       | Ubuntu Server 24.04 LTS |
| Image Generation       | Gen2                    |
| VM Size                | Standard DS1 v2         |
| vCPU                   | 1                       |
| Memory                 | 3.5 GiB                 |
| Initial Instance Count | 2                       |
| Minimum Instances      | 2                       |
| Maximum Instances      | 20                      |
| Autoscaling            | Enabled                 |
| Virtual Network        | `vnet-vmss-lab`         |
| Subnet                 | `snet-app`              |

The VMSS maintains multiple identical virtual machine instances. Each instance is attached to the VMSS backend pool used by the Azure Load Balancer.

The initial deployment contained two instances, providing multiple backend targets for incoming HTTP traffic.

This means the application does not depend on a single virtual machine.

If one instance becomes unavailable, the Load Balancer can stop sending traffic to that unhealthy instance and continue routing requests to healthy instances.

---

## Autoscaling Configuration

Autoscaling was configured to allow the VMSS to automatically adjust the number of instances based on workload.

The autoscaling configuration used CPU utilization as the scaling metric.

| **Setting**          | **Value**             |
| -------------------- | --------------------- |
| Autoscale Type       | Custom autoscale      |
| Metric               | CPU                   |
| Minimum Instances    | 2                     |
| Default Instances    | 2                     |
| Maximum Instances    | 20                    |
| Predictive Autoscale | Disabled              |
| Autoscale Profile    | `CPU-Based-Autoscale` |

The minimum instance count was configured as **2**, ensuring that the VMSS maintains at least two instances under normal operation.

The maximum instance count was configured as **20**, preventing the autoscale mechanism from creating an unlimited number of virtual machines.

### Autoscaling Concept

The VMSS can scale **out** when the workload increases and scale **in** when the workload decreases.

```text
                 Increased CPU Usage
                        │
                        ▼
                ┌─────────────────┐
                │ Autoscale Rules  │
                └────────┬────────┘
                         │
                    Scale Out
                         │
                         ▼
              ┌─────────────────────┐
              │ Additional VMSS     │
              │ Instances Created   │
              └─────────────────────┘


                 Reduced CPU Usage
                        │
                        ▼
                ┌─────────────────┐
                │ Autoscale Rules  │
                └────────┬────────┘
                         │
                    Scale In
                         │
                         ▼
              ┌─────────────────────┐
              │ Excess Instances   │
              │ Removed             │
              └─────────────────────┘
```

Autoscaling therefore separates the application from a fixed number of compute instances.

---

## Nginx Web Server Configuration

Nginx was installed on the VMSS instances to provide a web application endpoint on TCP port 80.

Nginx acts as the web server running inside each VMSS instance.

The basic traffic path is:

```text
Internet
   │
   │ HTTP :80
   ▼
Azure Load Balancer
   │
   │ Backend Pool
   ▼
VMSS Instance
   │
   │ TCP :80
   ▼
Nginx
   │
   ▼
HTTP Response
```

Nginx was configured to listen on port 80 so that the Load Balancer could forward incoming HTTP requests to the application instances.

Because the VMSS instances use the same configuration, each instance can provide the same web service.

---

## Load Balancer Traffic Flow

The Azure Standard Load Balancer provides the public entry point for the application.

The Load Balancer uses the following components:

1. **Frontend configuration** — receives traffic through the public IP.
2. **Load-balancing rule** — maps frontend TCP port 80 to backend TCP port 80.
3. **Backend pool** — contains the VMSS instances.
4. **Health probe** — determines whether backend instances are available.
5. **Outbound rule** — provides outbound Internet connectivity for the VMSS instances.

The resulting traffic flow is:

```text
                         INTERNET
                            │
                            │ HTTP :80
                            ▼
                 ┌─────────────────────┐
                 │ Azure Load Balancer  │
                 │     Public IP        │
                 │                      │
                 │ Frontend :80         │
                 └──────────┬──────────┘
                            │
                    Load Balancing Rule
                            │
                            ▼
                     Backend Pool
                            │
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
       ┌──────────────┐            ┌──────────────┐
       │ VMSS Instance│            │ VMSS Instance│
       │      1       │            │      2       │
       │              │            │              │
       │ Nginx :80    │            │ Nginx :80    │
       └──────────────┘            └──────────────┘
              │                           │
              └─────────────┬─────────────┘
                            │
                       HTTP Response
```

The Load Balancer does not itself run the web application.

Instead, it determines which healthy backend instance should receive each connection.

---

## Health Probe

The Load Balancer health probe was configured to use TCP port 80.

| **Setting**     | **Value**             |
| --------------- | --------------------- |
| Probe Name      | `lb-vmss-app-probe01` |
| Protocol        | TCP                   |
| Port            | 80                    |
| Backend Service | Nginx                 |

The health probe periodically checks whether the backend instance is accepting connections on TCP port 80.

Conceptually:

```text
Load Balancer
      │
      │ TCP :80 Health Probe
      ▼
VMSS Instance
      │
      ▼
Nginx :80
```

If the instance responds successfully, the Load Balancer considers the backend available.

If the probe fails according to the configured health-probe thresholds, the instance can be removed from the set of healthy backends used for load balancing.

This is important because **the Load Balancer does not simply send traffic to every VMSS instance**.

It sends traffic to instances that are considered healthy.

---

## Connectivity Testing

The lab included testing of both inbound application traffic and outbound Internet connectivity.

### Inbound Application Testing

The Load Balancer public IP was used as the entry point for HTTP traffic.

A request to:

```text
http://<Load-Balancer-Public-IP>
```

is processed through the Load Balancer and forwarded to a healthy VMSS instance running Nginx.

The expected flow is:

```text
Client
  │
  │ HTTP :80
  ▼
Public Load Balancer
  │
  ▼
Healthy VMSS Instance
  │
  ▼
Nginx
  │
  ▼
HTTP Response
```

### Backend Validation

The VMSS instances were also checked individually to confirm that Nginx was running and listening on TCP port 80.

This helped separate application-level problems from Load Balancer problems.

For example:

* If Nginx is not running, the health probe can fail.
* If the NSG blocks required traffic, connectivity can fail.
* If the Load Balancer rule is incorrect, frontend requests may not reach the backend.
* If the backend is healthy but outbound connectivity is unavailable, the problem is related to the outbound path rather than inbound load balancing.

---

## Outbound Internet Connectivity

During the lab, outbound Internet connectivity from the VMSS instances required additional configuration.

This demonstrated an important Azure networking concept:

> **Inbound connectivity and outbound connectivity are separate traffic paths.**

The public Load Balancer was configured with an outbound rule:

```text
outbound-vmss-internet
```

The outbound rule provides SNAT-based Internet connectivity for the VMSS backend instances.

The resulting outbound path is conceptually:

```text
VMSS Instance
      │
      │ Outbound Connection
      ▼
Backend Pool
      │
      ▼
Load Balancer Outbound Rule
      │
      ▼
Public IP
      │
      ▼
Internet
```

This was required because the VMSS subnet did not use a NAT Gateway.

---

## Troubleshooting Outbound Connectivity

The lab demonstrated that successful inbound access through a Load Balancer does not automatically prove that the VMSS instances have working outbound Internet connectivity.

Outbound connectivity was tested from the Linux VMSS instances.

Testing included connectivity to an external Internet address.

The troubleshooting process involved checking:

1. VMSS instance network configuration.
2. Subnet configuration.
3. Network Security Group rules.
4. Load Balancer configuration.
5. Backend pool membership.
6. Outbound rule configuration.
7. Public IP association.
8. Instance-level Internet connectivity.

After the outbound configuration was corrected, the VMSS instances were able to establish outbound Internet connections.

This troubleshooting exercise was important because it demonstrated that Azure networking problems should be investigated by following the traffic path rather than assuming that one working direction means all network connectivity is working.

---

## Validation

The final environment was validated by confirming the following:

| **Validation**                   | **Expected Result** |
| -------------------------------- | ------------------- |
| VMSS deployed                    | Successful          |
| Minimum instances                | 2                   |
| VMSS instances running           | Successful          |
| VMSS attached to subnet          | Successful          |
| Backend pool populated           | Successful          |
| Health probe configured          | TCP :80             |
| Nginx installed                  | Successful          |
| Nginx listening on :80           | Successful          |
| Load Balancer frontend available | Successful          |
| HTTP load-balancing rule         | TCP :80 → TCP :80   |
| Inbound HTTP traffic             | Successful          |
| Outbound Internet connectivity   | Successful          |
| Autoscale configuration          | Enabled             |
| Maximum VMSS instances           | 20                  |

---

## Key Concepts Demonstrated

This lab demonstrated several important Azure compute and networking concepts.

### 1. Virtual Machine Scale Sets

A VMSS allows Azure to manage multiple VM instances as a single scalable compute resource.

Instead of manually creating and managing individual virtual machines, the VMSS maintains instances using a common configuration.

### 2. Load Balancing

The Azure Load Balancer distributes incoming connections across backend VMSS instances.

This reduces dependence on a single server and allows the application to continue operating when multiple healthy instances are available.

### 3. Health Probes

Health probes allow the Load Balancer to determine which backend instances are available to receive traffic.

### 4. Autoscaling

Autoscaling allows the number of VMSS instances to change according to workload conditions.

### 5. Network Security Groups

The NSG provides network-level traffic filtering for the environment.

### 6. Outbound Connectivity

The lab demonstrated that outbound Internet access must be considered independently from inbound application traffic.

### 7. Nginx

Nginx provides the HTTP service running on each VMSS instance.

### 8. Separation of Responsibilities

The architecture separates responsibilities between services:

```text
Load Balancer
    │
    ├── Public entry point
    ├── Traffic distribution
    ├── Health checking
    └── Outbound connectivity
             │
             ▼
          VMSS
             │
             ├── Compute instances
             ├── Scaling
             └── Instance management
                     │
                     ▼
                   Nginx
                     │
                     └── HTTP application service
```

---

## Lessons Learned

The lab demonstrated that deploying a scalable application environment involves more than simply creating multiple virtual machines.

The major architectural relationships were:

```text
Internet
   │
   ▼
Public IP
   │
   ▼
Azure Load Balancer
   │
   ├── Health Probe
   ├── Load-Balancing Rule
   └── Outbound Rule
   │
   ▼
VMSS Backend Pool
   │
   ├── VMSS Instance 1
   ├── VMSS Instance 2
   └── Additional Instances
          │
          ▼
        Nginx
          │
          ▼
       HTTP :80
```

The most important lesson was understanding how the individual Azure resources work together rather than viewing them as independent services.

The Load Balancer provides traffic distribution and health checking.

The VMSS provides scalable compute.

The NSG provides network traffic filtering.

Nginx provides the actual web service.

Autoscaling changes the number of available compute instances according to the configured scaling rules.

Together, these components form a basic scalable and highly available web application architecture.
