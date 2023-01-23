---
uid: ServiceAccount
---

# Service Account
When the Client Failover Service is installed, it creates a Windows Service named "Client Failover Service".  
This service runs under an account named "NT SERVICE\AVEVAFailover".

It is possible to change the account used
to run the Client Failover Service, to either a domain account or another account on the local machine.
Before changing the service to run under a different account, it is first necessary to modify permissions on
the data folders used by the service.  These folders are located in the system's "ProgramData" folder, which
is normally on the "C:" drive.  The folder names are as follows:

- C:\ProgramData\AVEVA\Client Failover Service
- C:\ProgramData\AVEVA\Client Failover Service\Certificates
- C:\ProgramData\AVEVA\Client Failover Service\Certificates\Archive
- C:\ProgramData\AVEVA\Client Failover Service\Certificates\Keys

Before changing the service's account, perform the following steps on each of the folders listed above:

- In Windows Explorer, right-click on the folder name and select "Properties"
- Click on the "Security" tab
- Click the "Edit" button
- Select the desired user account from the "Group or user names" list
- In the "Permissions for Users" list, check "Read" and "Write" if they are not already selected
- Click "OK" twice to close both dialogs

After setting these folder permissions, perform these steps to change the service account:
- Open the "Services" control panel applet
- Select "Client Failover Service"
- Right-click and select "Properties"
- Click the "Log On" tab
- Under "This Account", select the desired account name and password
- Click "OK" to close the dialog
- Right-click on the service and select "Restart"


