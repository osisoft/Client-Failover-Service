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

5. In the "Ready to install Client Failover Service" window, click **Install** to begin the installation. To modify the location or port number, select **Back** to return to the Configuration page. 

6. After installation is completed, the wizard will navigate to the "Add Users" window. Two Windows local groups have been created automatically if they didn't already exist: AVEVAFailoverUsers and AVEVAFailoverAdministrators. Click **Add Users** to add users to these groups manually, or configure at a later time. Users in the AVEVAFailoverUsers group are typically adapter user accounts, which have permissions to configure failover groups and sessions. Users in the AVEVAFailoverAdministrators group have admin privileges to delete group, post failover role override, and perform global configuration including logging and health endpoints.
   >Note: The "Local Users and Groups" window will not launch on Windows Server Core operating systems.

7. Click **Next**.

9. Click **Finish** to close the setup wizard.
