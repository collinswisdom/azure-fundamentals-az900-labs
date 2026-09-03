# Lab 04 — Azure Container Instances (ACI)

## Overview

This lab demonstrates how to deploy and run a containerized application using **Azure Container Instances (ACI)**.

Azure Container Instances provides a simple way to run containers in Azure without having to provision or manage virtual machines.

The lab covers container deployment, networking, application access, container inspection, logging, lifecycle management, Azure CLI validation, and resource cleanup.

---

## Objectives

By completing this lab, I will:

* Understand the purpose of Azure Container Instances
* Understand the difference between containers and virtual machines
* Create an Azure Container Instance
* Deploy a containerized application
* Configure container networking
* Expose a container application through a public endpoint
* Configure a DNS name label
* Access the application from a web browser
* Inspect container properties and configuration
* View container logs
* Manage the container lifecycle
* Validate the deployment using Azure CLI
* Inspect resources within an Azure resource group
* Clean up Azure resources after completing the lab

---

# Architecture

The following diagram represents the architecture implemented in this lab:

![Azure Container Instances Architecture](diagrams/01-aci-architecture.png)

### Architecture Flow

```text
Internet
   │
   │ HTTP :80
   ▼
Public IP / DNS FQDN
   │
   ▼
Azure Container Instance
   │
   ▼
Container
   │
   ▼
Containerized Web Application
```

The application was exposed through a public endpoint using HTTP over TCP port 80.

---

# Prerequisites

* An active Azure subscription
* Access to the Azure Portal
* Basic understanding of Azure resources
* Basic understanding of networking concepts
* Azure CLI access for validation

---

# Step 1 — Create the Resource Group

A dedicated resource group was created to contain the resources used during the lab.

### Configuration

| Setting        | Value              |
| -------------- | ------------------ |
| Resource Group | `rg-aci-lab`       |
| Region         | South Africa North |

### Screenshot

![Resource Group](diagrams/02-resource-group.png)

---

# Step 2 — Create the Azure Container Instance

An Azure Container Instance was created to host the containerized web application.

Navigate to:

**Azure Portal → Container Instances → Create**

### Configuration

| Setting          | Value                                               |
| ---------------- | --------------------------------------------------- |
| Resource Group   | `rg-aci-lab`                                        |
| Container Name   | `aci-app-lab`                                       |
| Region           | South Africa North                                  |
| Operating System | Linux                                               |
| Image Source     | Quickstart image                                    |
| Image            | `mcr.microsoft.com/azuredocs/aci-helloworld:latest` |

### Screenshot

![Container Instance Configuration](diagrams/03-container-instance-configuration.png)

---

# Step 3 — Configure Container Networking

The container was configured with a public endpoint so that the web application could be accessed from the Internet.

### Configuration

| Setting         | Value            |
| --------------- | ---------------- |
| DNS Name Label  | Unique DNS label |
| Port            | `80`             |
| Protocol        | TCP              |
| IP Address Type | Public           |

### Traffic Flow

```text
Internet
   │
   │ HTTP :80
   ▼
Public IP / FQDN
   │
   ▼
Azure Container Instance
   │
   ▼
Web Application
```

### Screenshot

![Container Networking](diagrams/04-container-networking.png)

---

# Step 4 — Deploy the Container

The configured Azure Container Instance was submitted for deployment.

Azure provisioned the container instance and started the container using the specified image.

### Screenshot

![Container Deployment](diagrams/05-container-deployment.png)

---

# Step 5 — Verify the Container Instance

After deployment, the container instance was inspected from the Azure Portal.

The following information was verified:

* Container status
* Public IP address
* FQDN
* Port configuration
* Container image
* Operating system

### Screenshot

![Container Instance Overview](diagrams/06-container-instance-overview.png)

---

# Step 6 — Test the Application

The public FQDN of the container instance was opened in a web browser.

### Expected Result

The Azure Container Instances sample application displayed:

> **Welcome to Azure Container Instances!**

This confirmed that the container was running and that the application was reachable through the configured public endpoint.

### Screenshot

![Application Test](diagrams/07-application-test.png)

---

# Step 7 — Inspect Container Logs

The container logs were accessed through the Azure Portal.

Logs provide application output that can be useful when monitoring and troubleshooting containerized workloads.

### Screenshot

![Container Logs](diagrams/08-container-logs.png)

---

# Step 8 — Inspect Container Configuration

The deployed container configuration was inspected to understand the compute and runtime settings assigned to the container.

### Observed Configuration

| Setting               | Value                                               |
| --------------------- | --------------------------------------------------- |
| Container Name        | `aci-app-lab`                                       |
| Image                 | `mcr.microsoft.com/azuredocs/aci-helloworld:latest` |
| Port                  | `80`                                                |
| CPU                   | `0.5 cores`                                         |
| Memory                | `1 GiB`                                             |
| GPU SKU               | None                                                |
| GPU Count             | `0`                                                 |
| Commands              | None                                                |
| Environment Variables | None                                                |
| Volumes               | None                                                |

This demonstrates that a container has its own resource allocation and runtime configuration.

### Screenshot

![Container Configuration](diagrams/09-container-configuration.png)

---

# Step 9 — Manage the Container Lifecycle

The lifecycle of the Azure Container Instance was tested by stopping and starting the container.

### Lifecycle Tested

```text
Running
   │
   ▼
Stopped
   │
   ▼
Started
   │
   ▼
Running
```

After the container was started again, the application endpoint was verified to ensure the container was operational.

### Screenshot

![Container Lifecycle](diagrams/10-container-lifecycle.png)

---

# Step 10 — Validate Using Azure CLI

Azure CLI was used to validate the deployed container instance.

### View Container Information

```bash
az container show \
  --resource-group rg-aci-lab \
  --name aci-app-lab \
  --output table
```

### Retrieve Container State, IP Address and FQDN

```bash
az container show \
  --resource-group rg-aci-lab \
  --name aci-app-lab \
  --query "{Name:name, State:instanceView.state, IP:ipAddress.ip, FQDN:ipAddress.fqdn}" \
  --output table
```

### View Container Logs

```bash
az container logs \
  --resource-group rg-aci-lab \
  --name aci-app-lab
```

These commands provided command-line validation of the container deployment and its runtime information.

### Screenshot

![Azure CLI Validation](diagrams/11-azure-cli-validation.png)

---

# Step 11 — Verify Resource Deployment

The `rg-aci-lab` resource group was inspected to identify the resources created during the lab.

The resource group contained:

```text
rg-aci-lab
├── aci-app-lab
└── DefaultWorkspace-...-JNB
```

The `aci-app-lab` resource represents the Azure Container Instance.

The `DefaultWorkspace-...-JNB` resource represents the Log Analytics workspace associated with the Azure environment.

### Screenshot

![Resource Group Resources](diagrams/12-resource-group-resources.png)

---

# Step 12 — Cleanup

After completing the lab, the entire resource group was deleted to prevent unnecessary Azure charges.

The following Azure CLI command was used:

```bash
az group delete \
  --name rg-aci-lab \
  --yes \
  --no-wait
```

The resource group was subsequently removed.

### Verification

```bash
az group exists --name rg-aci-lab
```

Expected result:

```text
false
```

---

# Security Considerations

Although this was an introductory container lab, several security concepts were demonstrated.

### Public Exposure

The container was configured with a **public IP address and DNS endpoint**.

Public exposure should only be used when required because it makes the application reachable from the Internet.

### Port Minimization

Only **TCP port 80** was exposed for the web application.

Exposing only required ports follows the principle of reducing unnecessary attack surface.

### Container Isolation

The application ran inside a container rather than directly on a traditional virtual machine operating system.

Containers provide application-level isolation while allowing Azure to manage the underlying infrastructure.

### Secrets and Environment Variables

No environment variables or secrets were required for this demonstration.

In production environments, sensitive values should not be hard-coded into container images.

### Resource Cleanup

The temporary resources were deleted after the lab, reducing both cost and unnecessary resource exposure.

---

# Validation Checklist

| Task                              | Status |
| --------------------------------- | ------ |
| Resource group created            | ✅      |
| Container Instance created        | ✅      |
| Container image deployed          | ✅      |
| Port 80 configured                | ✅      |
| Public endpoint configured        | ✅      |
| DNS name label configured         | ✅      |
| Application accessed successfully | ✅      |
| Container logs reviewed           | ✅      |
| Container configuration inspected | ✅      |
| Container lifecycle tested        | ✅      |
| Azure CLI validation completed    | ✅      |
| Resource group inspected          | ✅      |
| Resources cleaned up              | ✅      |

---

# Key Concepts Learned

## Azure Container Instances

Azure Container Instances allows containers to run directly in Azure without requiring the user to manage the underlying virtual machines.

## Container Image

A container image contains the application and dependencies required to create and run a container.

## Container

A container is a running instance of a container image.

## Container Port

The container port is the network port used by the application running inside the container.

## Public IP

A public IP allows the containerized application to be accessed from the Internet.

## DNS Name Label

A DNS name label provides a DNS-based hostname that can be used to access the container application.

## Container Lifecycle

Containers can be started and stopped as required. Their lifecycle is different from managing a traditional virtual machine.

---

# VM vs App Service vs Azure Container Instances

| Feature                   | Virtual Machine | App Service           | Container Instances        |
| ------------------------- | --------------- | --------------------- | -------------------------- |
| Infrastructure management | High            | Low                   | Low                        |
| OS management             | Customer        | Microsoft             | Microsoft                  |
| Application deployment    | Manual/varied   | Application-focused   | Container-focused          |
| Container required        | No              | No                    | Yes                        |
| Scaling                   | Manual/VMSS     | Built-in options      | Limited/simple             |
| Best suited for           | Full OS control | Web applications/APIs | Simple container workloads |

---

# Conclusion

This lab demonstrated how to deploy, access, inspect, manage, and validate a containerized application using **Azure Container Instances**.

The lab demonstrated the progression from traditional virtual machines to managed application platforms and container-based workloads.

The key takeaway is that **ACI abstracts much of the underlying infrastructure management**, allowing administrators and developers to focus on running containerized applications without managing the underlying virtual machines.

The lab also provided practical exposure to:

* Container deployment
* Public networking
* DNS-based application access
* Container configuration
* Container logs
* Container lifecycle management
* Azure CLI
* Resource management
* Basic container security considerations

---

## Lab Status

**Status:** Completed

**Module:** Module 03 — Azure Compute

**Lab:** Lab 04 — Azure Container Instances

**Platform:** Microsoft Azure

**Region:** South Africa North

**Resource Group:** `rg-aci-lab`

**Container:** `aci-app-lab`
