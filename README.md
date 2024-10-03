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
   
2.Run a scan on Kali machine by running the command: ```sudo nmap <vm-ip>``` . You can also run a scan of your host machine if you place your Kali VM on a “bridged” network.

![2024-10-02_11-08](https://github.com/user-attachments/assets/97f4a27c-f557-4192-91c9-66f8adaad2e1)

3. This scan generates several security events, such as the detection of open ports and the identification of services running on those ports.

# Task 5: Querying for Security Events in the Elastic SIEM

Now that we have forwarded data from the Kali VM to the SIEM, we can start querying and analyzing the logs in the SIEM.

To do this, follow these steps:

 1.Inside your Elastic Deployment, click on the menu icon at the top-left with the three horizontal lines and then click on the “Logs” tab under “Observability” to view the logs from the Kali VM.
 
 2. In the search bar, enter a search query to filter the logs. For example, to search for all logs related to Nmap scans, enter the query:``` event.action:
    “nmap_scan”``` or ```process.args: “sudo”```.

3. Click on the “Search” button to execute the search query.

4. The results of the search query will be displayed in the table below. You can click on the three dots next to each event to view more details.

![2024-10-02_11-43_1](https://github.com/user-attachments/assets/83d3bb18-69be-426d-a310-d398800f249b)

![2024-10-02_13-09](https://github.com/user-attachments/assets/fb1c9030-4464-4ef0-9abe-a01cf0a499c5)

By generating and analyzing different types of security events in Elastic SIEM like the one above, or generating authentication failures by typing in the wrong password for a user or attempting SSH logins an incorrect password, you can gain a better understanding of how security incidents are detected, investigated, and responded to in real-world environments.

# Task 6: Create an Alert

In a SIEM, alerts are a crucial feature for detecting security incidents and responding to them in a timely manner. Alerts are created based on predefined rules or custom queries, and can be configured to trigger specific actions when certain conditions are met. In this task, we will walk through the steps of creating an alert in the Elastic SIEM instance to detect Nmap scans. By following these steps, you can create an alert that will monitor your logs for Nmap scan events and then notify you when they are detected.

Here are the steps:

 1. Click on the menu icon on the top-left, then under “Security,” click on “Alerts.”

 2. Click on “Manage rules” at the top right.

![2024-10-02_16-16](https://github.com/user-attachments/assets/e39294bd-9ada-4a4a-8a73-404b11396c19)

3. Click on the “Create new rule” button at the top right.

4. Under the “Define rule” section, select the “Custom query” option from the dropdown menu.

5. Under “Custom query,” set the conditions for the rule. You can use the following query to detect Nmap scan events.

![2024-10-02_16-19](https://github.com/user-attachments/assets/2b4f5763-55a7-46f6-ab03-b0a63ced64f6)

This query will match all events with the action “nmap_scan.” Then click “Continue.”

6. Under the “About rule” section, give your rule a name and a description (Nmap Scan Detection).

7. Set the severity level for the alert, which can help you prioritize alerts based on their importance. Keep all the other default settings under “Schedule rule” and click “Continue.”

![2024-10-02_16-26](https://github.com/user-attachments/assets/c6b16e67-2cbe-4d29-b4c9-74724cd771d3)

8. In the “Actions” section, select the action you want to take when the rule is triggered. You can choose to send an email notification, create a Slack message, or trigger a custom webhook.

9. Finally, click the “Create and enable rule” button to create the alert.

    

