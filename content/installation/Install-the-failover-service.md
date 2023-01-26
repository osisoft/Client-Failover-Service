---
uid: InstallTheService
---

# Install the Client Failover Service

Before installing the Client Failover Service, please note that it is only compatible with machines using the Windows operating system. We recommend that you review the system requirements before installation to ensure that your machine is compatible.

To install:

1. Double-click the .msi file in the installation kit to launch the Client Failover Service Setup Wizard. 

2. In the Configuration window, verify the system location to install the Client Failover Service. You can accept the default location on your C: drive or select **Change** to customize your location. 
 
3. Verify the Port Number. The port number defaults to 5590 but it can be modified to any number between 1024 and 49151.

4. Click **Next**. 

5. In the "Ready to install Client Failover Service" page, click **Install** to begin the installation. To modify the location or port number, select **Back** to return to the Configuration page. 

6. After installation is completed, the wizard will navigate to the "Add Users" page. Click **Add Users** to add users to the local groups created by the installer, or configure at a later time. Refer to [Groups](https://github.com/osisoft/Client-Failover-Service/blob/pbi/381223-installation/content/installation/authentication.md#groups) for details.

   **Note:** The "Local Users and Groups" window will not launch on Windows Server Core operating systems.

7. Click **Next**.

9. Click **Finish** to close the setup wizard.
