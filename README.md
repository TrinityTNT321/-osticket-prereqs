 <p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo" width="300"/>
</p>

<h1 align="center">osTicket – Prerequisites and Installation</h1>

This documentation outlines the prerequisites, environment configuration, and step-by-step installation process of the open-source help desk ticketing system **osTicket v1.15.8**, deployed on a Windows IIS server using Microsoft Azure Virtual Machines, PHP, and MySQL.

---

## 🧰 Environments and Technologies Used
- **Microsoft Azure** – Virtual Machines / Compute  
- **Remote Desktop (RDP)**  
- **Internet Information Services (IIS)**  
- **PHP v7.3.8**  
- **MySQL / HeidiSQL**

---

## 💻 Operating System Used
- **Windows 10 (21H2)**  

---

## 🧾 Project Overview
This project demonstrates the end-to-end process of setting up a cloud-hosted help desk system.  
You will:
- Deploy a **Virtual Machine** in **Microsoft Azure**
- Configure **IIS**, **PHP**, and **MySQL**
- Install and secure **osTicket v1.15.8**

---

## ⚙️ Installation Steps

### 1️⃣ Create and Configure the Virtual Machine
In **Microsoft Azure**, create a new **Virtual Machine (VM)** named `osTicket-VM`.  
Select the appropriate **resource group**, region, and use **Windows 11 Pro** as the image.  
Choose a size compatible with your lab requirements (e.g., 2 vCPUs and 8 GB RAM).  
Create a **username** and **password** (record these for RDP access).  

Under **Networking**, create a new Virtual Network, then click **Review + Create**.  
Once deployed, connect to your VM via **Remote Desktop (RDP)** using its public IP and credentials.

<p align="center">
  <img src="https://imgur.com/13tUFgP.png" width="25%" alt="Azure VM Setup 1"/>
  <img src="https://imgur.com/briGOzl.png" width="25%" alt="Azure VM Setup 2"/>
  <img src="https://imgur.com/5Iu6mBj.png" width="25%" alt="Azure VM Setup 3"/>
  <img src="https://imgur.com/vrYWmcw.png" width="25%" alt="Azure VM Setup 4"/>
</p>

---

### 2️⃣ Enable IIS and Required Components
Inside your VM:
1. Open **Control Panel → Programs → Turn Windows features on or off**
2. Enable **Internet Information Services (IIS)**
3. Under **World Wide Web Services → Application Development Features**, check **CGI**
4. Install:
   - **PHP Manager for IIS**
   - **URL Rewrite Module**
   - **VC_redist.x86**
   - **MySQL** (set username/password as `root`)

Then create a directory:
Extract `php-7.3.8-nts-Win32-VC15-x86` into that folder.
<p align="center">
  <img src="https://imgur.com/oDH5VKd.png" width="25%" alt="Azure VM Setup 1"/>
  <img src="https://imgur.com/CTN4Wl7.png" width="25%" alt="Azure VM Setup 2"/>
  <img src="https://imgur.com/gZohraa.png" width="25%" alt="Azure VM Setup 3"/>
  <img src="https://imgur.com/JetImEH.png" width="25%" alt="Azure VM Setup 4"/>
</p>


---

### 3️⃣ Register PHP in IIS
In IIS:
1. Click your **computer name** on the left panel  
2. Open **PHP Manager**
3. Select **Register new PHP version**  
4. Browse to:
Restart IIS (Stop → Start) to apply changes.
<p align="center">
  <img src="https://imgur.com/1QSIiRO.png" width="25%" alt="Azure VM Setup 1"/>
 </p>

---

## 🧩 Installing osTicket v1.15.8

### 1️⃣ Prepare the osTicket Files
Extract `osTicket-v1.15.8.zip` from the installation package.  
Copy the **upload** folder to:
Rename it to:
This opens the osTicket setup page in your browser.  
If PHP extensions are missing, proceed to enable them.
<p align="center">
  <img src="https://imgur.com/Rsdrgrw.png" width="25%" alt="Azure VM Setup 1"/>
 </p>


---

### 3️⃣ Enable Required PHP Extensions
From IIS → **PHP Manager** → **Enable or disable an extension**, enable:
- `php_imap.dll`
- `php_intl.dll`
- `php_opcache.dll`

Refresh the osTicket setup page to verify that all extensions are enabled.

---

### 4️⃣ Configure `ost-config.php`
Rename:
Adjust permissions:
1. Right-click → **Properties → Security**
2. Disable inheritance → Remove all entries
3. Add new permission: **Everyone → Full Control**

---

### 5️⃣ Web-Based Configuration
In your browser, click **Continue** and configure:
- **Helpdesk Name:** Any desired name  
- **Default Email:** Address that receives user tickets

---

## 🗄️ Database Setup Using HeidiSQL

Install **HeidiSQL** and open a new session:
Connect and create a new database named:

In the osTicket setup form, enter:
- **MySQL Database:** osTicket  
- **MySQL Username:** root  
- **MySQL Password:** root  
Click **Install Now!** to complete setup.

---

## 🌐 Accessing osTicket

After installation:
- **Admin Panel:**  
  [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
- **End-User Portal:**  
  [http://localhost/osTicket/](http://localhost/osTicket/)

---

→ Set to **Read-only**

Your osTicket environment is now fully installed and secured.

---

## 🧠 System Architecture Overview

Below is a simplified architecture showing how osTicket components interact within the environment.

```plaintext
+---------------------------------------------------+
|                    End Users                      |
|      (Submit tickets via Web Portal / Email)      |
+-----------------------------+---------------------+
                           |
                           v
+---------------------------------------------------+
|                  IIS Web Server                   |
|  Hosts osTicket PHP application and handles HTTP  |
+---------------------------------------------------+
                           |
                           v
+-------------------+     +-------------------------+
|     PHP Engine    | --> |     MySQL Database      |
|  Executes scripts |     | Stores ticket data,     |
|  and web logic    |     | users, and settings     |
+-------------------+     +-------------------------+
