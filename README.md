Azure Windows Web App with Private MySQL on Linux VM (Terraform Automated)
<br>
<br>
Project Overview:

This project demonstrates a Terraform-automated deployment of a secure Azure environment where a Windows-based Azure Web App connects privately to a Linux Virtual Machine hosting a MySQL database.
<br>
<br>

![Diagram](architecture_no_public_ip.png)

---

The solution highlights:

Automate infrastructure with Terraform

Connect cross-platform components (Windows Web App ↔ Linux VM)

Enforce private networking using Azure VNets and NSGs

Deploy a public-facing app that communicates securely with a backend database

---

Architecture

Terraform IaC to provision all core Azure resources (Resource Group, VNet, Subnets, NSGs, App Service Plan, Web App, and Linux VM).

Linux VM (Ubuntu) hosting a MySQL database, bootstrapped automatically with cloud-init (launching data when the machine starts).

Azure App Service (Windows) running the frontend application, integrated directly with GitHub for source control and continuous delivery.

Private VNet + NSGs ensuring only the Web App subnet can access MySQL (port 3306) while blocking public access.

End-to-end architecture demonstrating a real-world pattern: public-facing app ↔ private database backend.

---

Resources Created:<br>
<br>
<br>
![All Resources](All_Resources.png)<br>

<br>

[Linux Overview](Linux_VM_Overview.png)

<br>


---

Database Setup (MySQL):

SQL Initialization Script (01.sql) provisions:

appdb database and Course table

Inserts seed data:

Docker & Kubernetes (⭐ 4.5)

AZ-204 Azure Developer (⭐ 4.6)

AZ-104 Administrator (⭐ 4.7)

Creates least-privilege user appusr with role-based access

Configured for both remote TCP connections and localhost access
<br>
<br>
![MySql](01_SQL.png)

---

Cloud-Init Automation (MySQL Bootstrap):
<br>
<br>

Installs and configures MySQL server on the Linux VM.

Secures the root account with a strong password.

Configures MySQL to listen only on the private VNet IP.

Restarts MySQL and automatically runs the initialization script (01.sql).

Ensures the database, tables, seed data, and least-privilege user are created on first boot.
<br>
<br>
![Cloud-Init Automation](cloudinit.png)

---

The Azure Web App is connected directly to this GitHub repository via Terraform:
<br>

![Github](Github_azure_webapp_mysql_vnet_integration.png)

This ensures that updates pushed to the main branch of the repo are automatically pulled into the App Service.

The application folder (containing the .NET frontend app) provides the code that gets deployed to the Web App. Terraform provisions the infra, while GitHub serves as the source of truth for the application code.
<br>

[Application folder](learningapp)
<br>
[Web Deployment](web_deployment_tf.png)

---

Security Highlights:

Database locked down to VNet-only traffic

Web App private tunneling via VNet integration (no public DB access)

NSGs restrict traffic 

Terraform automation ensures repeatability and no manual drift
<br>

[Web App Overview ](Webapp_Resource_Overview.png)<br>
[Web App deployment center](webapp_Deployment_center.png)<br>
[Web App deployment center logs](webapp_Deployment_Center_logs.png)<br>
[Integration](Webapp_Resource_Networking_Virtual_Network_Integration.png)<br>
[Connection String](Webapp_Resource_Environment_Variables.png)<br>

---

Key Skills Demonstrated:

Terraform Infrastructure as Code (IaC)

Linux VM setup & MySQL administration

Windows-based Azure Web App deployment

Cross-platform integration (Windows App Service → Linux MySQL)

Azure Virtual Networking & NSGs

Secure cloud architecture patterns

---
Terraform Configuration Files:
<br>
[main](main_tf.png)<br>
[locals](locals_tf.png)<br>
[Webb App Network Deployment](APP_Network_Deployment_tf.png)<br>
[Database Config](db_Config_tf.png)<br>
[Database deployment](db_deployment_tf.png)<br>
[Terraform](Terraform_tf.png)<br>
[variables](variables_tf.png)<br>
[Terraform Var](Terraform_tf_vars.png)<br>


---

Terraform Instructions:
<br>
Authenticate with Azure: (az login, az account set --subscription "your-subscription-id")
<br>
Initialize Terraform (terraform init)
<br>
Validate configuration (terraform validate)
<br>
Plan deployment (terraform plan -out main.tfplan)
<br>
Apply deployment(terraform apply "main.tfplan")
<br>
Access the App (Terraform outputs the Web App URL after deployment. Open it in a browser to confirm connectivity with the MySQL database.)
<br>
Destroy resources -optional (terraform destroy)
<br>

![web app domain](Learning_App_Web_App.png)

---

Conclusion:
<br>
<br>
This project demonstrates how to design and deploy a secure, automated, and scalable cloud architecture on Azure by combining:

    Infrastructure as Code (Terraform) for repeatable, version-controlled deployments

    Azure App Service integrated with GitHub for continuous delivery of application code

    Linux VM with MySQL bootstrapped via cloud-init for hands-off database provisioning

    Private VNet + NSGs enforcing least-privilege communication and blocking public exposure

By bringing these components together, the project highlights not only technical depth in cloud infrastructure and security, but also an automation-first mindset
