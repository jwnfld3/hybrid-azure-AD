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
2. Run the installation and follow the prompts to configure Azure AD Connect.
3. During setup, select **"Customize"** and choose **Hybrid Azure AD Join** as the synchronization method.
4. Enter your **Azure AD credentials** (Global Administrator role) to allow Azure AD Connect to sync with your Azure AD instance.
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
