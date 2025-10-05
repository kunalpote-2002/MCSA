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
<img width="871" height="513" alt="image" src="https://github.com/user-attachments/assets/fae6de1d-a25a-4d25-8ffb-95bfaba46f27" />
<img width="872" height="512" alt="image" src="https://github.com/user-attachments/assets/76947457-fe51-4247-a94b-1544b1f08fad" />

### 🔹 Step 5: Add Namespace Folder & Targets

In DFS Management:
1. Right-click `\\Microsoft.com\Company` → **New Folder**.

2. Folder Name:  
<img width="871" height="516" alt="image" src="https://github.com/user-attachments/assets/34670a46-9a76-4f5a-b934-0fece530c2aa" />


4. Add Folder Targets:
- `\\Server1\\Nextgen_data`
- `\\Server2\\Nextgen_data`
- <img width="866" height="512" alt="image" src="https://github.com/user-attachments/assets/c532a647-14b8-4f69-94eb-957275d8af05" />


---

### 🔹 Step 6: Configure DFS Replication (DFSR)

When adding the second target, choose **Yes** to create a replication group.

| Setting | Value |
|----------|--------|
| **Replication Group Name** | Auto-generated |
<img width="871" height="519" alt="image" src="https://github.com/user-attachments/assets/5b032602-3300-4760-bfb8-f901d2b8519a" />

| **Primary Member** | Server1 |
<img width="867" height="509" alt="image" src="https://github.com/user-attachments/assets/0d97138e-cba8-43be-b4d6-41eecce775bb" />

<img width="873" height="445" alt="image" src="https://github.com/user-attachments/assets/7ba63cd4-14c1-4abf-beba-d66d4962a9db" />
<img width="874" height="446" alt="image" src="https://github.com/user-attachments/assets/73640709-719f-46e7-aa48-49a381331d03" />

| **Topology** | Full Mesh |
<img width="861" height="509" alt="image" src="https://github.com/user-attachments/assets/29bc63c0-f0fe-4c06-b77a-7c00215d050a" />

| **Schedule** | Replicate Continuously |
<img width="867" height="508" alt="image" src="https://github.com/user-attachments/assets/a9bc8822-c541-4a07-8d7b-4252208249d8" />

<img width="870" height="514" alt="image" src="https://github.com/user-attachments/assets/aa344956-ca0b-455b-b9b2-04adb768f2f5" />

![17](https://github.com/user-attachments/assets/6f8cff50-5d0e-4a5a-bbb8-ff74555d3911)

![18](https://github.com/user-attachments/assets/a0f6eb92-f124-4e62-ab53-8395915f50a6)

<img width="869" height="508" alt="image" src="https://github.com/user-attachments/assets/2483661d-8ef0-4fae-aebe-4563c2d47e5a" />


![20](https://github.com/user-attachments/assets/fad3a101-8e6b-43a0-a1fa-0a8514a5366e)

![21](https://github.com/user-attachments/assets/481daa95-8272-4097-be72-d65112a810bc)


![22](https://github.com/user-attachments/assets/24a5c506-2529-4c5d-8db2-4ca382bd1d58)


![23](https://github.com/user-attachments/assets/e468008e-0d6d-46ba-a32d-11e8a466c985)


Wait for replication status to show **“Converged”** in DFS Management.


![24](https://github.com/user-attachments/assets/ee0c3dd4-b2ea-4c11-8965-e379260bd60a)


---

## 💾 Project Phase 3: Backup Implementation (WSB)

### 🔹 Step 7: Install Windows Server Backup (WSB)

On both servers:
1. Open **Server Manager** → **Add Roles and Features**.
2. Go to **Features**.
3. Check **Windows Server Backup** → Install.

   <img width="866" height="470" alt="image" src="https://github.com/user-attachments/assets/999dd301-420a-4e4c-ad7d-5773a91df5e3" />


---

### 🔹 Step 8: Configure a Scheduled Backup (Server 2)

1. Open **Windows Server Backup** → **Backup Schedule**.

<img width="864" height="513" alt="image" src="https://github.com/user-attachments/assets/b017321f-9eff-46d8-b41c-f63909df7795" />
2. Configuration Type: **Custom** → **Add Items** → Select `C:\Nextgen_data`.


<img width="867" height="515" alt="image" src="https://github.com/user-attachments/assets/d8ad088a-2dbe-44cb-8766-b701eacb9519" />

<img width="869" height="516" alt="image" src="https://github.com/user-attachments/assets/727cc2b8-b2e8-4022-bd8d-76b05d6bc64b" />


3. Schedule: **Daily at 1:00 PM**.

![35](https://github.com/user-attachments/assets/aa2a3fcc-2b10-49bc-8f7b-d68bc9073839)

4. Destination: Dedicated local disk or network share.

![36](https://github.com/user-attachments/assets/eedd65b6-c487-4062-b1bf-a8dc3e3e09f3)

5. Review → Finish setup.

![37](https://github.com/user-attachments/assets/cefeeba0-b7e5-4d77-9a5e-fa649e2002ed)

![39](https://github.com/user-attachments/assets/1880a43f-3c24-4195-a58e-90e1594fb550)


---






