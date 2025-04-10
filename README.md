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
![image](https://github.com/user-attachments/assets/26879d87-1545-4b88-be2e-6991df0e19f6)
![image](https://github.com/user-attachments/assets/f0595dc6-fd60-48fa-ab41-20f18ebd67be)

2. Select **Hybrid Azure AD Join** and click **Next**.
![image](https://github.com/user-attachments/assets/32433e68-03fd-43ad-a204-7862cc218a96)
![image](https://github.com/user-attachments/assets/a5cdac0f-f321-43b6-8763-3f5a2ac14758)

3. Follow the instructions to configure synchronization for devices in your on-premises AD.
4. Complete the setup, and allow Azure AD Connect to begin synchronizing devices.

### Step 3: Test Synchronization:

1. Initiate a manual sync by clicking on the "Run" button under Sync Status or use PowerShell to trigger a synchronization (e.g., Start-ADSyncSyncCycle -PolicyType Delta).
2. Monitor the sync process to ensure it completes without errors.
![image](https://github.com/user-attachments/assets/eea93991-5f63-4078-bdca-600bdb61cca0)

### Step 4: Verify Synchronization in Azure AD:

1. Log in to the Azure AD portal and navigate to Azure Active Directory > Users to confirm that user objects from your on-premises AD have been successfully synchronized.
![image](https://github.com/user-attachments/assets/35941d2c-65d6-4c5d-a508-5beace2810fa)

2. Ensure that changes made in the on-premises AD are reflected in Azure AD, indicating that the sync process is working.
![image](https://github.com/user-attachments/assets/2a49a527-7641-44bd-8d69-2261c32bbeed)

# Conclusion

This configuration enables Windows Server devices to be both domain-joined (on-premises) and Azure AD-joined (cloud), offering centralized management and improved security. By implementing Hybrid Azure AD Join, devices can authenticate seamlessly across both environments, enhancing user access and security across on-premises and cloud resources.


