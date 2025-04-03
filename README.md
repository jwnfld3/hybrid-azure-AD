
# Checking if a Windows Server 2022 is Hybrid Azure AD Joined

## Summary  
This lab outlines the steps to check if a Windows Server 2022 is Hybrid Azure AD joined. A Hybrid Azure AD join configuration allows devices to be both domain-joined and registered in Azure AD, enabling cloud-based management alongside on-premises management. This lab demonstrates how to verify this configuration using several methods, including the Azure AD portal, local tools on the server, and Event Viewer logs.

---

## Lab Requirements

- **Azure AD**: A cloud-based identity and access management service that enables secure authentication and device management for cloud-based resources.
- **Hybrid Azure AD Join**: A configuration that allows devices to be joined to both on-premises Active Directory and Azure AD, facilitating seamless authentication and management across environments.
- **Windows Server 2022**: The operating system on which the Hybrid Azure AD Join configuration will be checked.
- **Administrator Access**: Required to run commands and access settings on the server.
- **Azure AD Connect**: A tool that synchronizes on-premises Active Directory with Azure AD for Hybrid Azure AD Join.
- **Event Viewer**: A Windows tool used for viewing detailed event logs that can help in troubleshooting device join issues.

---

## Who  
IT administrators and security professionals responsible for managing enterprise devices in both on-premises and cloud environments.

## What  
This lab demonstrates how to check if a Windows Server 2022 device is Hybrid Azure AD joined by using various methods, including checking Azure AD, local server tools, and Event Viewer logs.

## When  
When verifying if Windows Server devices are properly integrated with both on-premises Active Directory and Azure AD for hybrid management.

## Where  
Performed on a Windows Server 2022 machine, either on-premises or in a virtual environment, connected to the corporate network.

## Why  
Hybrid Azure AD Join ensures that domain-joined devices can be managed both on-premises and in the cloud, enabling seamless access to enterprise resources and enhancing security and compliance.

---

## Steps

### Step 1: Check in Azure AD Portal

**Definition**:  
The Azure AD portal is a cloud-based management interface that provides insights into devices, users, and organizational settings.

**Objective**:  
Verify the device's Hybrid Azure AD Join status by checking the device’s details in the Azure AD portal.

**Steps**:
1. Sign in to the [Microsoft Entra (Azure AD)](https://entra.microsoft.com) portal.
2. Navigate to **Devices** > **All Devices**.
3. In the search bar, enter the **server name** and press Enter.
4. Check the **Join Type** column:
   - **Hybrid Azure AD Joined** indicates the device is Hybrid Azure AD joined.
   - **Domain Joined** or **Azure AD Joined** suggests the device is not Hybrid Azure AD joined.

---

### Step 2: Check Locally on the Server

#### Using Command Prompt

**Definition**:  
Command Prompt is a command-line interface in Windows that allows execution of system commands to retrieve system information.

**Objective**:  
Check the device's join status using the `dsregcmd` command to verify if it’s Hybrid Azure AD joined.

**Steps**:  
1. Open **Command Prompt** as Administrator.
2. Run the command:  
   ```powershell
   dsregcmd /status
   ```
3. Review the output under **Device State**:
   - **AzureAdJoined**: Should be **NO** for Hybrid Azure AD Join.
   - **DomainJoined**: Should be **YES** for Hybrid Azure AD Join.
   - **AzureAdPrt**: Should be **YES**, indicating Azure AD authentication works.

---

#### Using PowerShell

**Definition**:  
PowerShell is a command-line scripting language that allows system administrators to automate tasks and retrieve system data.

**Objective**:  
Use PowerShell to retrieve device join status for Hybrid Azure AD Join.

**Steps**:  
1. Open **PowerShell** as Administrator.
2. Run the following command:  
   ```powershell
   Get-MsolDevice -DeviceId (Get-WmiObject Win32_ComputerSystem).UUID
   ```
   *Note*: If the device is Hybrid Azure AD joined, device information will be returned.

---

### Step 3: Check in Local Group Policy

**Definition**:  
Group Policy is a tool for configuring and enforcing settings across devices in an Active Directory environment.

**Objective**:  
Ensure that devices are set to register with Azure AD, allowing Hybrid Azure AD Join.

**Steps**:
1. Open **gpedit.msc** on the server.
2. Navigate to:  
   ```
   Computer Configuration > Administrative Templates > Windows Components > Device Registration
   ```
3. Ensure that **"Register domain-joined computers as devices"** is set to **Enabled**.

---

### Step 4: Check in Event Viewer

**Definition**:  
Event Viewer is a Windows tool used to view event logs that track system activities, including device join events.

**Objective**:  
Use Event Viewer to identify Hybrid Azure AD Join events that confirm successful registration.

**Steps**:
1. Open **Event Viewer**.
2. Navigate to:  
   ```
   Applications and Services Logs > Microsoft > Windows > User Device Registration > Admin
   ```
3. Look for the following event IDs:
   - **Event ID 201**: Successful device registration.
   - **Event ID 202**: Azure AD-registered device.
   - **Event ID 304**: Device registration status.

---

### Step 5: Troubleshooting Hybrid Azure AD Join Issues

**Definition**:  
Troubleshooting involves identifying and resolving problems with device registration, group policies, or Azure AD synchronization.

**Objective**:  
Address common issues preventing Hybrid Azure AD Join, such as incorrect Group Policy settings or misconfigured Azure AD Connect.

**Steps**:
1. Ensure **Azure AD Connect** is properly set up and synchronizing devices between on-premises AD and Azure AD.
2. Verify that **Group Policy** is correctly configured to allow devices to register with Azure AD.
3. Ensure that the server has internet access to reach necessary Azure AD endpoints.

---

## Conclusion

After completing this lab, the ability to verify if a Windows Server 2022 is Hybrid Azure AD joined using multiple methods should be achieved. Understanding how to troubleshoot Hybrid Azure AD Join configurations is essential for maintaining secure and compliant access to both on-premises and cloud resources.

---

## Next Steps

1. **Automate Device Join with Windows Autopilot**: Simplify the device setup process by automating Hybrid Azure AD Join and Intune enrollment.
2. **Configure Conditional Access Policies**: Set up security policies that restrict access to resources based on device compliance.
3. **Integrate with Microsoft Defender for Endpoint**: Enhance endpoint security by integrating Microsoft Defender for threat protection.

