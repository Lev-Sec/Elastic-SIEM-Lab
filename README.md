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
 
# Task 3: Setting up the Agent to Collect Logs
To set up the agent to collect logs from your Kali VM and forward them to your Elastic SIEM instance, follow these steps:

 1. Log in to your Elastic SIEM instance and navigate to the Integrations page by: clicking on the Kibana main menu bar at the top left, then selecting “Integrations” at the bottom.
 2. Search for “Elastic Defend” and click on it to open the integration page.

![2024-10-02_10-03](https://github.com/user-attachments/assets/e0a3c444-efd8-4da7-b86f-33bbe5bfef1a)


3. Click on “Install Elastic Defend” and follow the instructions provided on the integration page to install the agent on your Kali VM.

![2024-10-02_10-44](https://github.com/user-attachments/assets/f032a45b-fc6c-4082-beb2-1f146ac37a0a)

4. Paste the command given to you into the Kali terminal (command line).

You can verify that the agent has been installed correctly by running this command:```sudo systemctl status elastic-agent.service```

# Task 4: Generating Security Events on the Kali VM

To verify that the agent is working correctly, you can generate some security-related events on your Kali VM. To do this, we can use a tool like Nmap. Nmap (Network Mapper) is a free and open-source utility used for network exploration, management, and security auditing.

To run an Nmap scan, follow these steps:

 1. Install Nmap on the Linux VM if you’re not using Kali, Nmap already comes preinstalled in Kali. Open a new Terminal and run this command to install it: sudo apt-get install nmap.
    
 2.Run a scan on Kali machine by running the command: sudo nmap <vm-ip>. You can also run a scan of your host machine if you place your Kali VM on a “bridged” network.
