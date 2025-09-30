Azure Windows Web App with Private MySQL on Linux VM (Terraform Automated)
<br>
Project Overview

This project demonstrates a Terraform-automated deployment of a secure Azure environment where a Windows-based Azure Web App connects privately to a Linux Virtual Machine hosting a MySQL database.
<br>
<br>
![web app domain](Learning_App_Web_App.png)

---

The solution highlights how to:

Automate infrastructure with Terraform

Connect cross-platform components (Windows Web App ↔ Linux VM)

Enforce private networking using Azure VNets and NSGs

Deploy a public-facing app that communicates securely with a backend database

---

Architecture

Terraform IaC: Automates resource creation (VM, Web App, VNet, NSG, etc.)

Linux VM (Ubuntu): Runs the MySQL server

Azure Web App (Windows App Service): Hosts the frontend web application

Virtual Network (VNet): Provides private communication between app and database

NSGs: Restrict MySQL access to only the Web App subnet (port 3306)

Public Internet Traffic: Only the Web App is exposed; the database is not directly accessible

---

Resources Created:<br>
<br>
<br>
![All Resources](All_Resources.png)<br>

<br>
---

📸 Demo & Screenshots

(Add screenshots of your portal, VNet settings, NSG, and successful database connection here.)

---

Security Highlights:

Database locked down to VNet-only traffic

Web App private tunneling via VNet integration (no public DB access)

NSGs restrict traffic (only port 3306 + SSH for admin)

Terraform automation ensures repeatability and no manual drift

---

Key Skills Demonstrated:

Terraform Infrastructure as Code (IaC)

Linux VM setup & MySQL administration

Windows-based Azure Web App deployment

Cross-platform integration (Windows App Service → Linux MySQL)

Azure Virtual Networking & NSGs

Secure cloud architecture patterns

---

📂 Repository Structure
