# Lab 01 — Azure Virtual Machines

## Overview

This lab demonstrates the deployment and architectural configuration of an Azure Virtual Machine within a controlled Azure network environment.

The lab focuses on understanding how Azure Virtual Machines are designed, deployed, secured, and connected to supporting Azure resources.

The objective is not simply to deploy a virtual machine, but to demonstrate the architectural decisions involved in designing a secure and manageable compute workload in Microsoft Azure.

---

## Business Scenario

A small organization has a legacy business application that currently runs on a Windows Server.

The application requires:

* Windows Server
* Administrative control over the operating system
* Custom software installation
* Persistent storage
* Controlled network access
* Secure administrative access

The organization wants to migrate this workload to Microsoft Azure while maintaining control over the server environment.

---

## Objectives

By completing this lab, I will:

* Deploy an Azure Virtual Machine.
* Create a dedicated virtual network and subnet.
* Configure network security using a Network Security Group.
* Attach managed storage to the virtual machine.
* Configure secure administrative access.
* Validate connectivity to the virtual machine.
* Document the architectural decisions made during deployment.
* Evaluate security, availability, scalability, and cost considerations.

---

## Target Architecture

The solution will use the following logical architecture:

```text
Azure Subscription
        │
        ▼
Resource Group
        │
        ▼
Virtual Network
10.10.0.0/16
        │
        ▼
Application Subnet
10.10.1.0/24
        │
        ├── Network Security Group
        │
        ▼
Windows Virtual Machine
        │
        ▼
Managed Disk
```

---

## Azure Resources

| Resource               | Purpose                                                      |
| ---------------------- | ------------------------------------------------------------ |
| Resource Group         | Provides a logical management boundary for the lab resources |
| Virtual Network        | Provides network isolation for the workload                  |
| Subnet                 | Segments the virtual network and hosts the VM                |
| Network Security Group | Controls network traffic to and from the subnet/VM           |
| Virtual Machine        | Provides compute capacity for the legacy application         |
| Managed Disk           | Provides persistent storage for the VM                       |

---

## Architectural Considerations

The architecture will consider the following:

### Security

* Restrict unnecessary inbound network access.
* Use secure administrative access.
* Apply network security controls using an NSG.
* Avoid exposing the VM to the public internet unnecessarily.

### Networking

The virtual network will use:

* Address space: `10.10.0.0/16`
* Application subnet: `10.10.1.0/24`

### Compute

The VM will be selected based on the requirements of the workload rather than simply choosing the largest available size.

### Storage

Azure Managed Disks will provide persistent storage for the virtual machine.

### Cost

The VM size, disk configuration, and runtime duration will be considered as part of the overall cost of the solution.

---

## Implementation

The implementation will be completed in the following stages:

1. Create the resource group.
2. Create the virtual network.
3. Create the application subnet.
4. Configure the Network Security Group.
5. Deploy the Azure Virtual Machine.
6. Configure managed storage.
7. Configure secure administrative access.
8. Test connectivity.
9. Review the deployed architecture.
10. Document findings and lessons learned.

---

## Validation

The following areas will be validated after deployment:

* VM deployment status
* Network configuration
* NSG configuration
* Administrative connectivity
* Storage configuration
* Resource relationships
* Security configuration

---

## Evidence

Screenshots and architecture diagrams will be added after the implementation is completed.

Planned evidence includes:

* Azure resource group
* Virtual network and subnet
* Network Security Group
* VM configuration
* VM networking
* Managed disk
* Successful connectivity test
* Final architecture diagram

---

## Architecture Decisions

| Decision                         | Rationale                                            |
| -------------------------------- | ---------------------------------------------------- |
| Use Azure VM                     | The workload requires operating-system-level control |
| Dedicated VNet                   | Provides network isolation                           |
| Dedicated subnet                 | Provides workload segmentation                       |
| NSG                              | Provides network traffic control                     |
| Managed Disk                     | Provides persistent VM storage                       |
| Controlled administrative access | Reduces unnecessary exposure of the VM               |

---

## Lessons Learned

This section will be completed after the lab implementation.

Key areas will include:

* What was learned about Azure VM architecture.
* Security considerations discovered during deployment.
* Networking decisions and their impact.
* Operational responsibilities associated with IaaS.
* Potential improvements to the architecture.

---

## Conclusion

This lab demonstrates the deployment of an Azure Virtual Machine as an Infrastructure-as-a-Service workload.

The primary architectural lesson is that Azure Virtual Machines provide significant control over the operating system and infrastructure configuration, but that control also introduces additional operational and security responsibilities compared with more managed Azure compute services.
