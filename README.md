# Windows Server 2022 Home Lab

## Overview
This repository serves as a technical portfolio documenting my hands-on implementation and administration of a Windows Server 2022 environment. It features a comprehensive documentation of the practical steps, configurations, and system deployments managed during this project.

## Tech Stack
*  **Hypervisor:** Microsoft Hyper-V
*  **OS:** Windows Server 2022

## Lab Implementation

### Phase 1: Virtual Infrastructure & Environment Setup
In this phase, the core virtualization environment was prepared using Microsoft Hyper-V to host the Windows Server instances.

1. **Networking Configuration:**
   - Created a Virtual Switch: `External-Internet-Switch` (Type: External) to provide internet connectivity to the VMs.

2. **Virtual Machine Provisioning:**
   - **VM 01 (Domain Controller):**
     - **Name:** `Home-Lab-DC1-Server_2022`
     - **Memory:** 4096 MB
     - **OS:** Windows Server 2022 Datacenter (Desktop Experience)
   - **VM 02 (Member Server):**
     - **Name:** `Home-Lab-SVR1-Server_2022`
     - **Memory:** 3072 MB
     - **OS:** Windows Server 2022 Datacenter (Desktop Experience)

3. **System Optimization:**
   - **Checkpoints Disabled:** I have intentionally disabled the checkpoint feature for both virtual machines as they are not required for the current phase of the lab. 
   - **Note:** While I am aware that checkpoints (snapshots) are a powerful tool for recovering from configuration errors.

### Visual Proof of Setup

#### 1. Networking & Hyper-V Management
| Hyper-V Manager Overview | Virtual Switch Configuration | 
|---|---|
| ![HyperV Manager](./assets/Hyper-V%20Manager.png) | ![vSwitch](./assets/virtual-Switch.png) |

#### 2. Virtual Machine Specifications
* **DC1 Configuration:**
  
  ![DC1 Settings](./assets/DC1-Settings.png)
* **SVR1 Configuration:**
  
  ![SVR1 Settings](./assets/SVR1-Settings.png)

#### 3. System Access (Live Demo)
> Below is a quick capture of the successful login process:
![Login Demo](./assets/login-demo.gif)

---

### Phase 2: Active Directory Domain Services & Network Integration
In this phase, I established the identity foundation by promoting the primary Domain Controller and integrating the member server into the `homelab.com` forest.

1. **Network Standardization:**
   - Assigned static IPv4 addresses to ensure persistent DNS resolution between the servers.
   - **KWT-DC01 (Domain Controller):**
     - **IP:** `192.168.8.100` | **Preferred DNS:** `127.0.0.1` (Loopback)
   - **KWT-SVR1 (Member Server):**
     - **IP:** `192.168.8.101` | **Preferred DNS:** `192.168.8.100` (Pointing to DC1)

2. **Domain Controller Promotion:**
   - **Role Installation:** Deployed Active Directory Domain Services (AD DS) role.
   - **Forest Creation:** Established a new forest: `homelab.com`.
   - **Identity Update:** Finalized the server hostname as `KWT-DC01`.

3. **Domain Integration (Join Process):**
   - **Server Naming:** Updated the member server hostname to `KWT-SVR01`.
   - **Domain Join:** Successfully joined `KWT-SVR01` to the `homelab.com` domain.
   - **Authentication:** Verified the join using Domain Administrator credentials.

### Visual Proof of Domain Setup

#### 1. Networking & Static IP Configuration
| KWT-DC01 Network Settings | KWT-SVR01 DNS Pointing | 
|---|---|
| ![DC Network](./assets/dc-ip-config.png) | ![SVR Network](./assets/svr-dns-setup.png) |

#### 2. Active Directory Configuration & Domain Join
* **Forest Deployment (`homelab.com`):**
  
  ![Forest Setup](./assets/forest-setup.png)

* **Initiating Domain Join & Success:**

| Initiating Join | Success Message |
|---|---|
| ![Join Step](./assets/domain-join-step.png) | ![Join Success](./assets/join-success.png) |
  
#### 3. Directory Verification & Identity (Live Demo)
* **Active Directory Users and Computers (ADUC):**
  > Verification of `KWT-SVR01` registration within the "Computers" container:
  ![ADUC Check](./assets/aduc-check.png)

* **Domain Admin Access:**
  > Below is a capture of the successful login on the member server using the Domain Administrator account (`HOMELAB\Administrator`):
  ![Domain Login](./assets/domain-login-final.gif)


