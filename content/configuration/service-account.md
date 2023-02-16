---
uid: ServiceAccount
---

# Service account
When the Client Failover Service is installed, it creates a Windows Service named "Client Failover Service".  This service runs under a virtual service account named "NT SERVICE\AVEVAFailover".

## Change the service account
It is possible to change the account used to run the Client Failover Service, to either a domain account or another account on the local machine.
Before changing the service to run under a different account, you must give that account access to the service's data folders.  These folders are located in the system's "ProgramData" folder, which is normally on the "C:" drive.  The folder names are as follows:

- %ProgramData%\AVEVA\Client Failover Service
- %ProgramData%\AVEVA\Client Failover Service\Certificates
- %ProgramData%\AVEVA\Client Failover Service\Certificates\Archive
- %ProgramData%\AVEVA\Client Failover Service\Certificates\Keys

Before changing the service's account, perform the following steps on each of the folders listed above:

1. In Windows Explorer, right-click on the folder name and select "Properties"
2. Click on the "Security" tab
3. Click the "Edit" button
4. Select the desired user account from the "Group or user names" list
5. In the "Permissions for Users" list, check "Read" and "Write" if they are not already selected
6. Click "OK" twice to close both dialogs

  > **Note:** If you have configured health endpoints, follow the instructions in the section "Reconfigure Health Endpoints" below.

After setting folder permissions, perform these steps to change the service account:
1. Open the "Services" control panel applet
2. Select "Client Failover Service"
3. Right-click and select "Properties"
4. Click the "Log On" tab
5. Under "This Account", select the desired account name and password
6. Click "OK" to close the dialog
7. Right-click on the service and select "Restart"

## Reconfigure health endpoints
Use the following procedure to reconfigure the service account if the configuration includes one of the following:
- Health endpoints that use Basic authentication (Username and Password) while sending data to PI Web API OMF endpoint
- Health endpoints that uses ClientId or ClientSecret while sending data to the AVEVA Data Hub OMF endpoint
 
1. Use the `GET` method in conjunction with the `https://<host>:<port>/api/v1/configuration/healthendpoints` REST endpoint to read the configuration.
2. Save a copy of the response body from step 1. The Password or ClientSecret values you originally entered will have been replaced with asterisks. In the saved copy, replace the asterisks with the original ones.
3. Use the `DELETE` method in conjunction with the `https://<host>:<port>/api/v1/configuration/healthendpoints` REST endpoint to delete the health endpoints.
4. Stop the service.
5. Perform the service account changes listed above.
6. Start the service with the new user account as listed above. 
7. Use the `PUT` method in conjunction with the `https://<host>:<port>/api/v1/configuration/healthendpoints` with the body from step 2 to restore the configuration.
