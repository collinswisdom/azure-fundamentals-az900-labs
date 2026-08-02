# Lab 01: Enterprise Cloud Deployment Models & Architecture Trade-offs

## 1. Executive Summary & Objective
As part of designing cloud architecture strategies for client workloads at KollraX Ltd, I evaluated the strategic, operational, and security trade-offs between **Public**, **Private**, **Hybrid**, and **Multicloud** deployment models. The objective of this lab is to establish a clear decision framework for workload migration based on data sovereignty, network latency, and financial expenditure models (CapEx vs. OpEx).

---

## 2. Technical Framework & Azure Concepts
* **Public Cloud (Microsoft Azure):** Shared multi-tenant physical hardware abstracted by the Hyper-V hypervisor. Operates on a pure Operational Expenditure (OpEx) model with high elasticity.
* **Private Cloud:** Dedicated single-tenant infrastructure (on-premises datacenter or Azure Dedicated Host). Requires Capital Expenditure (CapEx) for physical hardware procurement and lifecycle management.
* **Hybrid Cloud Architecture:** Connection of local on-premises infrastructure with Azure using secure IPsec VPN tunnels or private **Azure ExpressRoute** circuits, managed centrally via **Azure Arc**.
* **Multicloud Strategy:** Distributing workloads across distinct cloud vendors to isolate blast radiuses and meet specific client compliance demands.

---

## 3. Real-World Engineering Scenario (KollraX MSP Case Study)

### The Challenge
A corporate legal client required a public-facing web portal for client document intake during peak litigation audit cycles. However, strict legal compliance mandates required that sensitive client records remain hosted on local encrypted storage arrays with zero direct internet exposure.

### My Architectural Solution: Hybrid Infrastructure
1. **Frontend Tier:** Deployed an auto-scaling **Azure App Service** instance in the public cloud to absorb traffic spikes without local server investments.
2. **Database & Storage Tier:** Maintained on-premises behind physical firewalls on local storage arrays.
3. **Secure Connectivity:** Configured an encrypted Site-to-Site IPsec VPN tunnel connecting the Azure Virtual Network (VNet) directly to the internal gateway, ensuring frontend queries access backend storage over a private IP space.

---

## 4. Workload Mapping Matrix

| Workload Scenario | Recommended Model | Primary Engineering Rationale |
| :--- | :--- | :--- |
| Customer Web Portal | **Public Cloud** | Instant elasticity during traffic spikes; zero hardware overhead. |
| Core Financial Ledger | **Private Cloud** | Strict regulatory isolation and full physical hardware control. |
| Hybrid Identity Sync | **Hybrid Cloud** | Entra Connect syncing local Active Directory to Entra ID for M365 SSO. |
| Disaster Recovery Site | **Multicloud / Hybrid** | Geographical failover across independent cloud environments. |

---

## 5. Security & Financial Assessment

### Security Audit Notes
* Public management endpoints require enforcement of **Conditional Access Policies** and **MFA** via Microsoft Entra ID.
* For hybrid connectivity, all data in transit across the public network must be encrypted using AES-256 via IKEv2 IPsec protocols.

### Financial Analysis (CapEx vs. OpEx)
* Shifting web tiers to Azure reduced the client's upfront hardware procurement cost (**CapEx**) to zero, moving costs into dynamic **OpEx** driven purely by consumption during active audit months.

---

## 6. Personal Takeaways & Verification

```bash
# Verifying Azure VNet Gateway status via Azure CLI
az network vnet-gateway show --resource-group rg-kollrax-hybrid --name gw-hybrid-hub
