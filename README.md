# Hybrid Azure AD Join for Windows Server 2022

## Overview
This repository contains a lab that demonstrates how to connect a Windows Server 2022 to Azure AD via **Hybrid Azure AD Join**. This setup allows Windows Server devices to be both **domain-joined** (on-premises) and **Azure AD-joined** (cloud), providing centralized management and enhanced security. Hybrid Azure AD Join enables devices to authenticate across both environments seamlessly.

## Lab Requirements

- **Azure AD**: A cloud-based identity and access management service that enables secure authentication and device management for cloud-based resources.
- **Hybrid Azure AD Join**: A configuration that allows devices to be joined to both on-premises Active Directory and Azure AD, enabling seamless management and authentication across both environments.
- **Windows Server 2022**: The operating system on which the Hybrid Azure AD Join configuration will be performed.
- **Administrator Access**: Required to perform actions on the server and configure hybrid Azure AD join settings.
- **Azure AD Connect**: A tool that synchronizes on-premises Active Directory with Azure AD and is required for Hybrid Azure AD Join configuration.
- **Internet Access**: Required to ensure the server can communicate with Azure AD endpoints.

## Lab Steps

### Step 1: Install and Configure Azure AD Connect

1. Download the latest version of **Azure AD Connect** from the [Microsoft website](https://www.microsoft.com/en-us/download/details.aspx?id=47594).
![image](https://github.com/user-attachments/assets/5b59dcf1-06a7-4b20-88e0-598957a46267)
![image](https://github.com/user-attachments/assets/277dfa29-e64a-4609-a806-b6bc68b609cf)

2. Run the installation and follow the prompts to configure Azure AD Connect.
![image](https://github.com/user-attachments/assets/48f333eb-f39b-4533-80fc-dd86159cb62b)

3. During setup, select **"Use Express Settings"** and choose **Hybrid Azure AD Join** as the synchronization method.
![image](https://github.com/user-attachments/assets/55e6fad4-4f35-4068-af84-04b37d221102)


4. Enter your **Azure AD credentials** (Global Administrator role) to allow Azure AD Connect to sync with your Azure AD instance.
![image](https://github.com/user-attachments/assets/ac9045a4-f9eb-4122-969a-229c3c313045)
![image](https://github.com/user-attachments/assets/375fd3b4-c09b-46f9-9622-6cccc9a01794)
![image](https://github.com/user-attachments/assets/54504fb0-2198-4f44-8dce-31dfb20cffed)
![image](https://github.com/user-attachments/assets/d84e6038-8a9e-456c-8418-9e3547e81f7b)

5. Confirm that **Azure AD Connect** is properly set up and can sync with both on-premises Active Directory and Azure AD.

### Step 2: Configure Hybrid Azure AD Join in Azure AD Connect

1. Open **Azure AD Connect** and go to **Configure**.
2. Select **Hybrid Azure AD Join** and click **Next**.
3. Choose **Windows Server 2022** as the device type.
4. Follow the instructions to configure synchronization for devices in your on-premises AD.
5. Complete the setup, and allow Azure AD Connect to begin synchronizing devices.

### Step 3: Verify Domain-Joined Server 2022

1. On your **Windows Server 2022**, open **Settings** > **System** > **About**.
2. Under **Computer name, domain, and workgroup settings**, ensure that the **Domain** is displayed as the correct Active Directory domain.
3. If the server is not yet domain-joined, click **Change settings**, and then **Domain** to join the server to the correct domain.

### Step 4: Check Hybrid Azure AD Join Configuration on the Server

1. Open **Command Prompt** as Administrator.
2. Run the command:  
   ```powershell
   dsregcmd /status
