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


### 1. Networking Strategy & DNS Hierarchy
I configured static IP addressing to ensure persistent communication. The most critical part was pointing the Member Server's DNS to the Domain Controller's IP.

#### **KWT-DC01 (Domain Controller)**
* **IP Address:** `192.168.8.100`
* **Preferred DNS:** `127.0.0.1` (Loopback address)
![DC Network](./assets/dc-ip-config.png)

#### **KWT-SVR01 (Member Server)**
* **IP Address:** `192.168.8.101`
* **Preferred DNS:** `192.168.8.100` (Pointing to DC)
![SVR Network](./assets/svr-dns-setup.png)

---

### 2. Domain Controller Promotion
I initiated the new forest `homelab.com` and promoted `KWT-DC01` to the Role of Domain Controller.
![Forest Setup](./assets/forest-setup.png)

### 3. Member Server Integration
This step involved connecting the Member Server to the established domain.

| Stage | Action | Documentation |
| :--- | :--- | :--- |
| **Joining** | Connecting to `homelab.com` | ![Join Step](./assets/domain-join-step.png) |
| **Confirmation** | Welcome Message | ![Join Success](./assets/join-success.png) |

---

### 4. Final Verification
I verified the infrastructure's health through the ADUC console and a successful cross-machine domain login.

> ![ADUC Check](./assets/aduc-check.png)
> *`KWT-SVR01` correctly registered in the Computers container.*

#### 🎬 Live Demo: Domain Administrator Login
![Domain Login](./assets/domain-login-final.gif)
*Logging into the member server using the `HOMELAB\Administrator` account.*
