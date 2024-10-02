# Elastic-SIEM-Lab
How to set up a Elastic SIEM Lab

In this guide, I’ll walk you through steps on how to set up a home lab for Elastic Stack Security Information and Event Management (SIEM) using the Elastic Web portal and a Azure Kali Linux VM. You will also learn how to generate security events on the Kali VM, set up an agent to forward data to the SIEM, and query and analyze the logs in the SIEM. 

# Prerequisites

Before we get started, make sure you have the following:

 - A fully set up Microsoft Azure account.
 - Basic knowledge of Linux and Azure.

# Overview of the tasks

  - Set up a free Elastic account.
  - Setup the Azure Kali VM.
  - Configure the Elastic Agent on the Linux VM to collect the logs and forward it to the SIEM.
  - Generate security events on the Kali VM.
  - Query to find the security events in the Elastic SIEM.
  - Create a Dashboard to visualize security events.
  - Create alerts for security events.

# Task 1: Set up an Elastic Account

Before we get started, we need to create a free account to set up a cloud Elastic instance that we can run the SIEM on. To do that, follow these steps:

  1. Sign up for a free trial to use Elastic Cloud at https://cloud.elastic.co/registration
  2. Once you have an Elastic account, log in to the Elastic Cloud console at https://cloud.elastic.co.
  3. Click on “Start your free trial.”
  4. Click on the “Create Deployment” button and select “Elasticsearch” as the deployment type.
  5. Choose a region and deployment size that fits your needs and click on “Create Deployment.”
  6. Wait for the configuration to complete.
  7. Once the deployment is ready, click “continue.”

# Task 2: Setting up the Azure Kali Linux VM

To set it up, follow these steps:

 1. Subscription: Choose the appropriate Azure subscription.
 2. Resource Group: Create a new resource group or select an existing one.
 3. VM Name: Provide a name for your VM (e.g., KaliVM).
 4. Region: Select a region close to your location for better performance.
 5. Availability options: Choose the availability option that suits your needs.
 6. Image: Ensure that Kali Linux is selected.
 7. Size: Click on "Select size" and choose the appropriate VM size based on your requirements. For testing, a Standard B1s or B2s is usually sufficient.
 8. Administrator Account: Choose the authentication type (password or SSH public key) and enter a username and password (or SSH key).

Step 2: Configure Networking

  1. Virtual Network: You can either create a new virtual network or select an existing one.
  2. Subnet: The default subnet will be automatically selected.
  3. Public IP: Ensure you select Create new for a public IP if you want to access it over the internet.
  4. Network Security Group: You can either use a new or existing security group. For simplicity, use the default.
  5. Inbound Port Rules: Allow SSH (port 22) for remote access.

Step 3: Review + Create

  1. Review your configurations in the Review + create tab.
  2. Click on Create to start the deployment of your Kali Linux VM.

![2024-10-02_08-58](https://github.com/user-attachments/assets/dbf115f4-5946-47db-b2ee-2795f9826e0a)


Step 4: Accessing Your VM

   Once the deployment is complete, navigate to the resource (your VM).
   Click on Connect and select SSH.
    If you chose password authentication, you can use any SSH client (like PuTTY or the terminal on Linux/Mac) to connect. Use the public IP provided in the overview.
        Command: ```ssh username@your_public_ip```
        Replace username with the one you created, and your_public_ip with the VM's public IP.

 ![2024-10-02_09-21](https://github.com/user-attachments/assets/dfa727fd-a426-40a2-9316-5d591ac2281f)




