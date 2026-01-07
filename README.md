<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket – Prerequisites & Installation Guide

This repository documents the prerequisites and step-by-step installation of **osTicket**, an open-source help desk ticketing system, on a **Windows-based Azure Virtual Machine using IIS**.

---

## 📌 Overview

osTicket is a PHP-based ticketing system that relies on IIS, PHP, and MySQL to function correctly on Windows environments. This guide is intended for lab, learning, or entry-level production setups.

---

## 🛠️ Environments & Technologies Used

* Microsoft Azure (Virtual Machines)
* Remote Desktop Protocol (RDP)
* Internet Information Services (IIS)
* PHP Manager for IIS
* MySQL

---

## 💻 Operating Systems Used

* Windows 10
* Windows Server (Azure VM)

---

## ✅ Prerequisites

Ensure the following components are available before starting:

* Internet Information Services (IIS)
* CGI Module (IIS Feature)
* PHP Manager for IIS
* PHP 7.3.8 (NTS, x86)
* VC_redist.x86
* MySQL Server 5.5.62
* Rewrite Module (IIS)
* HeidiSQL (optional – database management)

---

## 🚀 Installation Steps

---

### 1. Connect to the VM



1. Locate the **Public IP Address** of the VM
2. Connect using **Remote Desktop**
3. Log in with the credentials created earlier
   
<img width="1001" height="1114" alt="09-screenshot" src="https://github.com/user-attachments/assets/32407cd1-8414-438d-8c02-8d492e27b09a" />

---

### 2. Download osTicket Installation Files




* Download the [osTicket installation package](https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0)
* Extract the files to the **Desktop** for easy access
<img width="2259" height="1185" alt="11-screenshot" src="https://github.com/user-attachments/assets/cc61f21f-cfce-4a8e-ac4e-97c86f336d0b" />
---

### 3. Enable IIS with CGI

<!-- Screenshot 04: Windows Features – IIS and CGI Enabled (images/04-enable-iis-cgi.png) -->

1. Open **Control Panel**
2. Navigate to **Programs → Turn Windows features on or off**
3. Enable:

   * **Internet Information Services (IIS)**
   * **CGI** (under *World Wide Web Services → Application Development Features*)

---

### 4. Install PHP Manager

<!-- Screenshot 05: PHP Manager Installer (images/05-php-manager-install.png) -->

* Run the **PHP Manager for IIS** installer
* Complete the installation using default settings

PHP Manager is required to configure PHP versions and extensions used by osTicket.

---

### 5. Install IIS Rewrite Module

<!-- Screenshot 06: IIS Rewrite Module Installer (images/06-rewrite-module.png) -->

* Run the **Rewrite Module** installer
* This enables friendly URLs and proper request routing in IIS

---

### 6. Configure PHP

<!-- Screenshot 07: PHP Folder and Extracted Files (images/07-php-folder.png) -->

1. Navigate to `C:\`
2. Create a folder named **PHP**
3. Extract `php-7.3.8-nts-Win32-VC15-x86.zip` into the `C:\PHP` directory

---

### 7. Install VC++ Redistributable

<!-- Screenshot 08: VC_redist.x86 Installer (images/08-vc-redist.png) -->

* Run `VC_redist.x86.exe`
* Complete the basic installation

This is required for PHP to run correctly on Windows.

---

### 8. Install MySQL

<!-- Screenshot 09: MySQL Installer – Typical / Standard Configuration (images/09-mysql-install.png) -->

1. Run the MySQL installer
2. Choose **Typical Setup**
3. Select **Standard Configuration**
4. Set the MySQL root credentials

MySQL is used to store:

* Tickets
* Users and agents
* Emails
* Attachments (metadata)
* Help topics
* Configuration data

---

### 9. Configure IIS for PHP

<!-- Screenshot 10: IIS PHP Manager – Register New PHP Version (images/10-register-php.png) -->

1. Open **IIS Manager** as Administrator
2. Select the server node
3. Open **PHP Manager**
4. Click **Register new PHP version**
5. Browse to `C:\PHP\php-cgi.exe`

---

### 10. Restart IIS

<!-- Screenshot 11: IIS Stop and Start (images/11-restart-iis.png) -->

* In IIS Manager:

  * Right-click the server
  * Click **Stop**
  * Wait for full shutdown
  * Click **Start**

---

### 11. Deploy osTicket Files

<!-- Screenshot 12: osTicket Files in wwwroot (images/12-osticket-wwwroot.png) -->

1. Extract `osTicket-v1.15.8.zip`
2. Copy the **upload** folder to:

   ```
   C:\inetpub\wwwroot
   ```
3. Rename the folder from `upload` to `osTicket`

---

### 12. Restart IIS Again

<!-- Screenshot 13: IIS Restart After osTicket Deployment (images/13-final-restart.png) -->

Restart IIS once more to apply all changes.

---

## 🎉 Final Step

Open a browser inside the VM and navigate to:

```
http://localhost/osTicket
```

You should now see the osTicket web installer.

---

## 📚 Notes

* This guide is intended for educational and lab environments
* Additional hardening is recommended for production deployments
* Database and email configuration are completed during the web installer

---

## 🧩 Troubleshooting Tips

* Ensure required PHP extensions are enabled in PHP Manager
* Confirm MySQL service is running
* Verify folder permissions for `C:\inetpub\wwwroot\osTicket`

---
