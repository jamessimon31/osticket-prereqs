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

<img width="1072" height="801" alt="12-screenshot" src="https://github.com/user-attachments/assets/06b52fed-34f9-4e92-aa62-f8677b21c3cf" />
<img width="958" height="784" alt="13-screenshot" src="https://github.com/user-attachments/assets/ab79fe74-4925-41b7-aeb9-72751f31780a" />

---

### 4. Install PHP Manager

<img width="1024" height="861" alt="15-screenshot" src="https://github.com/user-attachments/assets/81da830d-7553-46c1-9b7e-24ab5e2f2b7c" />

* Run the **PHP Manager for IIS** installer
* Complete the installation using default settings

PHP Manager is required to configure PHP versions and extensions used by osTicket.

---

### 5. Install IIS Rewrite Module

<img width="1022" height="811" alt="16-screenshot" src="https://github.com/user-attachments/assets/9d0cf9f5-4b1c-4db1-a82a-f4ca0f1fb604" />


* Run the **Rewrite Module** installer
* This enables friendly URLs and proper request routing in IIS

---

### 6. Configure PHP

<img width="1726" height="1478" alt="17-screenshot" src="https://github.com/user-attachments/assets/b364367c-3462-4d8b-89f8-4b11bef815cc" />

1. Navigate to `C:\`
2. Create a folder named **PHP**
3. Extract `php-7.3.8-nts-Win32-VC15-x86.zip` into the `C:\PHP` directory

<img width="935" height="468" alt="18-screenshot" src="https://github.com/user-attachments/assets/5c2b2879-e68d-44ec-8c87-52ada4fe2ec6" />


---

### 7. Install VC++ Redistributable

<img width="505" height="313" alt="20-screenshot" src="https://github.com/user-attachments/assets/0ba65f14-8857-4e0a-aaba-61608be1dfa2" />


* Run `VC_redist.x86.exe`
* Complete the basic installation

This is required for PHP to run correctly on Windows.

---

### 8. Install MySQL

<img width="525" height="410" alt="21-screenshot" src="https://github.com/user-attachments/assets/c7b0b759-0b61-4443-adc0-3a88f610fe22" />

1. Run the MySQL installer
2. Choose **Typical Setup**
3. Select **Standard Configuration**
4. Set the MySQL root credentials
<img width="1078" height="875" alt="22-screenshot" src="https://github.com/user-attachments/assets/48253de6-48f9-47e9-8405-a61a40112504" />
<img width="1136" height="831" alt="23-screenshot" src="https://github.com/user-attachments/assets/3c89268a-81e2-48d3-8323-7d8bc2ad0a60" />
<img width="1812" height="1164" alt="24-screenshot" src="https://github.com/user-attachments/assets/71504b77-3f9d-4ed8-9288-53ef223f2ff1" />


MySQL is used to store:

* Tickets
* Users and agents
* Emails
* Attachments (metadata)
* Help topics
* Configuration data

---

### 9. Configure IIS for PHP

<img width="1778" height="1398" alt="25-screenshot" src="https://github.com/user-attachments/assets/b7d5eb96-1d57-4301-926f-e594329d5469" />

1. Open **IIS Manager** as Administrator
2. Select the server node
3. Open **PHP Manager**
4. Click **Register new PHP version**
5. Browse to `C:\PHP\php-cgi.exe`
<img width="2397" height="1319" alt="26-screenshot" src="https://github.com/user-attachments/assets/a6b84201-9820-41e3-aec1-2986f951c0eb" />

---

### 10. Restart IIS

<img width="2289" height="1275" alt="27-screenshot" src="https://github.com/user-attachments/assets/42820d00-bc4f-44b7-8ce8-a6370f82d241" />


* In IIS Manager:

  * Right-click the server
  * Click **Stop**
  * Wait for full shutdown
  * Click **Start**

---

### 11. Deploy osTicket Files

<img width="804" height="613" alt="28-screenshot" src="https://github.com/user-attachments/assets/65dfab18-b7d9-45b3-b676-ff828aea4768" />


1. Extract `osTicket-v1.15.8.zip`
2. Copy the **upload** folder to: `osTicket`
<img width="805" height="240" alt="29-screenshot" src="https://github.com/user-attachments/assets/653822a0-d0bd-4df3-a520-63ef48d4632a" />

   ```
   C:\inetpub\wwwroot
   ```
4. Rename the folder from `upload` to `osTicket`

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
