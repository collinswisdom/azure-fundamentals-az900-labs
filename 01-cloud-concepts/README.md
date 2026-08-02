# ☁️ Module 01: Cloud Concepts & Engineering Trade-Offs

Welcome to **Module 01: Cloud Concepts** of my Azure Fundamentals portfolio. This module moves beyond basic theory to examine how core cloud principles—deployment architectures, service models, financial structures, and SLAs—are evaluated and implemented in real-world enterprise environments.

---

## 🎯 Engineering Objectives

In this module, I demonstrate and evaluate:
* 🌐 **Architectural Selection:** Evaluating Public, Private, Hybrid, and Multicloud architectures based on data residency, network latency, and compliance constraints.
* 📦 **Service Model Mapping:** Deciding between IaaS, PaaS, and SaaS to balance administrative overhead with operational control.
* 🛡️ **Shared Responsibility Governance:** Mapping security boundaries between Microsoft Azure and customer operations.
* 💰 **Financial Optimization:** Analyzing CapEx vs. OpEx models and conducting cost estimations using the Azure Pricing Calculator.
* ⏱️ **Reliability Engineering:** Calculating composite SLAs and designing high-availability strategies for critical workloads.

---

## 📚 Module Labs & Progress

| Lab | Title | Focused Engineering Scenario | Status |
| :---: | :--- | :--- | :---: |
| **Lab 01** | [Cloud Deployment Models](./Lab-01-Cloud-Deployment-Models.md) | Architectural evaluation and hybrid migration planning for legal client data. | 🟢 Completed |
| **Lab 02** | [Cloud Service Models](./Lab-02-Cloud-Service-Models.md) | Mapping workload tiers (IaaS vs PaaS vs SaaS) for enterprise M365 & Azure environments. | ⬜ Pending |
| **Lab 03** | [Shared Responsibility Model](./Lab-03-Shared-Responsibility-Model.md) | Security auditing and boundary mapping between Microsoft and enterprise operations. | ⬜ Pending |
| **Lab 04** | [Azure Pricing and Consumption](./Lab-04-Azure-Pricing-and-Consumption.md) | Cost estimation, resource tagging, and budget guardrails via Azure Calculator. | ⬜ Pending |
| **Lab 05** | [Azure Service Level Agreements](./Lab-05-Azure-Service-Level-Agreements.md) | Calculating composite uptime guarantees for multi-tier Azure solutions. | ⬜ Pending |

---

## 🔑 Architectural Reference

```text
Enterprise Cloud Framework
├── Deployment Models
│   ├── Public Cloud (Pay-as-you-go elasticity, shared hypervisor isolation)
│   ├── Private Cloud (Single-tenant dedicated infrastructure, high compliance)
│   ├── Hybrid Cloud (On-premises Active Directory/Data linked via IPsec VPN or ExpressRoute)
│   └── Multicloud (Azure Entra ID identity backbone extended to multi-cloud platforms)
└── Service Models
    ├── IaaS (Azure VMs, VNets - Full OS & network control)
    ├── PaaS (Azure App Service, Azure SQL - Reduced management overhead)
    └── SaaS (Microsoft 365, Entra ID - Pure service consumption)
