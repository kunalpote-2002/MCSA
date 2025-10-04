# 🖥️ Windows Server Project: DFS Namespace & Replication with Backup (MCSA Project)

## 📘 Project Overview
This project demonstrates a **high-availability file sharing and backup solution** using:
- **Active Directory Domain Services (AD DS)**
- **Distributed File System (DFS Namespace & Replication)**
- **Windows Server Backup (WSB)**

It covers full configuration from domain setup to replication, testing, and disaster recovery.

---

## 🏗️ Project Phase 1: Preparation & Role Installation

### 🔹 Step 1: Configure Initial Servers

#### Server 1 (Domain Controller)
- Install **Active Directory Domain Services (AD DS)**.
- Create a new domain:  
- Optionally, host the DFS Namespace root for high availability.

#### Server 2 (Member Server)
- Join Server 2 to the domain (`Microsoft.com`).

### 🔹 Step 2: Create Shared Folders

| Server | Folder Path | Network Share |
|---------|--------------|---------------|
| Server 1 | `c:\Nextgen_data` | `\\Server1\\Nextgen_data` |
| Server 2 |  `c:\Nextgen_data` | `\\Server2\\Nextgen_data` |

**Permissions Configuration**
- **NTFS Permissions**: Assign domain groups Modify/Read rights as needed.  
- **Share Permissions**: Give `Authenticated Users` or `Everyone` **Full Control**.
-<img width="870" height="487" alt="image" src="https://github.com/user-attachments/assets/93461e68-be30-4d90-8807-9c0a0ecc7fed" />
 - SAME FOR SERVER 2
-<img width="745" height="456" alt="image" src="https://github.com/user-attachments/assets/2a75e119-87f5-4a34-8b3e-09943af4fab8" />



---

## ⚙️ Project Phase 2: DFS Namespace (DFSN) & Replication (DFSR)

### 🔹 Step 3: Install DFS Roles
On both servers:
1. Open **Server Manager** → **Manage** → **Add Roles and Features**.
2. Under **Server Roles**, expand:


3. Check both:
- DFS Namespaces  
- DFS Replication  
4. Complete the installation.

---

### 🔹 Step 4: Create Domain-Based Namespace

1. Open **DFS Management** (`Start → Administrative Tools`).
  <img width="871" height="511" alt="image" src="https://github.com/user-attachments/assets/3622cac5-6e31-44e4-88e9-d30d399068a2" />
2. Right-click **Namespaces** → **New Namespace**.

   <img width="869" height="515" alt="image" src="https://github.com/user-attachments/assets/7b519077-b927-4962-a929-8d5c6ded1e26" />


3. Enter:
- **Namespace Server**: `Server1`
- <img width="873" height="510" alt="image" src="https://github.com/user-attachments/assets/58e19814-29a7-4391-87d5-8c0ede70e85a" />

- **Namespace Name**: `Company`
- <img width="862" height="510" alt="image" src="https://github.com/user-attachments/assets/b683955b-441a-4f96-abb7-78944da0baa2" />

4. Choose **Domain-based Namespace**.  
- Resulting Path:  \\Microsoft.com\Company
- <img width="869" height="517" alt="image" src="https://github.com/user-attachments/assets/b7561579-fe9c-44cc-a42e-2a4f2ff5106b" />

  ```

---

### 🔹 Step 5: Add Namespace Folder & Targets

In DFS Management:
1. Right-click `\\Microsoft.com\Company` → **New Folder**.
2. Folder Name:  


3. Add Folder Targets:
- `\\Server1\\Nextgen_data`
- `\\Server2\\Nextgen_data`

---

### 🔹 Step 6: Configure DFS Replication (DFSR)

When adding the second target, choose **Yes** to create a replication group.

| Setting | Value |
|----------|--------|
| **Replication Group Name** | Auto-generated |
| **Primary Member** | Server1 |
| **Topology** | Full Mesh |
| **Schedule** | Replicate Continuously |

Wait for replication status to show **“Converged”** in DFS Management.

---

## 💾 Project Phase 3: Backup Implementation (WSB)

### 🔹 Step 7: Install Windows Server Backup (WSB)

On both servers:
1. Open **Server Manager** → **Add Roles and Features**.
2. Go to **Features**.
3. Check **Windows Server Backup** → Install.

---

### 🔹 Step 8: Configure a Scheduled Backup (Server 2)

1. Open **Windows Server Backup** → **Backup Schedule**.
2. Configuration Type: **Custom** → **Add Items** → Select `C:\BACKUP_NEXTGEN`.
3. Schedule: **Daily at 1:00 PM**.
4. Destination: Dedicated local disk or network share.
5. Review → Finish setup.

---






