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

* Creating a VM to Use osTicket: [Here](https://github.com/jamessimon31/ConfigueVM)

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

<img width="2289" height="1275" alt="27-screenshot" src="https://github.com/user-attachments/assets/0865f6ed-9db2-4696-99ca-676bcc12502d" />


Restart IIS once more to apply all changes.

---


### 13. In the IIS go to Sites > Default > osTicket

In the IIS go to Sites > Default > osTicket

<img width="344" height="196" alt="image" src="https://github.com/user-attachments/assets/de9c3752-8021-4c58-b78e-0ce43a96d538" />

   a. It should look like this

<img width="195" height="222" alt="image" src="https://github.com/user-attachments/assets/1f708ebd-6bd6-4121-adc2-d00908aecbd1" />



> **Note:** that some extensions are not enabled. We will fix a couple of those before we finish the lab.

---

### 13. In the IIS go to Sites > Default > osTicket

- Go back to IIS, Site > Default > osTicket
  <img width="1454" height="1152" alt="image" src="https://github.com/user-attachments/assets/a01e310f-b127-4ed2-a525-e66b36baf973" />

- Double-click PHP Manager
- Click 'Enable or Disable an extension'

<img width="468" height="126" alt="image" src="https://github.com/user-attachments/assets/85294e91-a154-4b17-a8f5-29476d98ce81" />

- Enable: ```php_imap.dll```
- Enable: ```php_intl.dll```
- Enable: ```php_opcache.dll```

<img width="282" height="237" alt="image" src="https://github.com/user-attachments/assets/4736e377-d15b-4931-8e98-50b97cb791f1" />

> Before you go forward make sure all of them show enabled. Once they show enable, Refresh the osTicket site in the Browser. 

<img width="349" height="313" alt="image" src="https://github.com/user-attachments/assets/6a7feaa8-7e78-4004-946c-070ffa0a67bc" />

---

### 14. Rename the Config files

- Go to ```C:\inetpub\wwwroot\osTicket\include```
- Change the File ```ost-sampleconfig.php```
- To ```ost-config.php```
  
  <img width="345" height="309" alt="image" src="https://github.com/user-attachments/assets/b99d97c2-e7e4-4b05-91fe-2a80d616b5b9" />

- We then are going to change the permission to that file, so osTicket can change/edit that file

  <img width="254" height="217" alt="image" src="https://github.com/user-attachments/assets/d8d3ba37-b622-4c21-aa6d-1d4a880e1080" />

#### Set Permissions

1.  Right-click `ost-config.php` → **Properties → Security → Advanced**
   
    <img width="116" height="154" alt="image" src="https://github.com/user-attachments/assets/3f69c02f-9f20-4d9d-a406-9ee539efe1c8" />

2.  Disable inheritance → Remove all
   
    <img width="304" height="190" alt="image" src="https://github.com/user-attachments/assets/82ae260d-4a40-4cd0-99c1-6732e5ee949f" />

3.  Add **Everyone** with **Full Control**
   
    <img width="298" height="178" alt="image" src="https://github.com/user-attachments/assets/e591d071-7d08-4ca1-9f25-640cb06963d5" />


> ⚠️ This is insecure for production but acceptable for lab use.



### 14. Create the Database (HeidiSQL)

<img width="332" height="201" alt="image" src="https://github.com/user-attachments/assets/0fcfdf48-19ac-4413-acc5-7b123e5a6ac7" />

1.  Install **HeidiSQL** from the installation files
    
2.  Open HeidiSQL and connect to the MySQL server
   
      - Username: `root`
      - Password: `root`
        
        <img width="468" height="267" alt="image" src="https://github.com/user-attachments/assets/492e793e-0234-48c0-a90e-e64f520ee251" />

3.  Create a database named: `osTicket`

      <img width="345" height="215" alt="image" src="https://github.com/user-attachments/assets/be4369bf-487c-40d0-b5af-c2e127eebe50" />

---

### 15. Complete osTicket Web Installer

In the browser setup page:

-   Helpdesk Name
    
-   Default Email
    
-   Admin Name, Email, Username, Password


<img width="266" height="275" alt="image" src="https://github.com/user-attachments/assets/d57d0c42-07fd-40d8-9c7a-52863171be1c" />


**Database Settings:**

-   MySQL Database: `osTicket`
    
-   Username: `root`
    
-   Password: `root`
    

Click **Install Now!**


<img width="468" height="207" alt="image" src="https://github.com/user-attachments/assets/3166537e-2dd0-4170-a853-7ae904195361" />

----------

## 🎉 Final Step

Open a browser inside the VM and navigate to:

-   End User Portal:
    
    ```
    http://localhost/osTicket/
    ```
    
-   Admin Panel:
    
    ```
    http://localhost/osTicket/scp/login.php
    ```
    
You should now see the osTicket web installer.


<img width="363" height="285" alt="image" src="https://github.com/user-attachments/assets/c30257c9-4b67-4831-bf77-98b742a65970" />

---

## 🧹 Cleanup (Important)

After installation:

1.  Delete: `C:\inetpub\wwwroot\osTicket\setup`
    
2.  Set permissions on: `C:\inetpub\wwwroot\osTicket\include\ost-config.php` 
    to **Read-only**

---

## 📚 Notes

* This guide is intended for educational and lab environments
* Additional hardening is recommended for production deployments
* Database and email configuration are completed during the web installer

---
