---
uid: CertificateMgmtFailover
---

# Certificate Management

To enable HTTPs for REST API endpoints, the server requires an SSL certificate. Certificates identify client applications and machines on servers and allow for building a secure communication link. The Client Failover Service generates a self-signed certificate with a 15-year expiration date during installation. Instead of being in the machine’s certificate store, the certificate can be found in a data folder ((%PROGRAMDATA%/AVEVA/Client Failover Service/Certificates) on your machine.

The Certificates folder contains a public CRT certificate file and a private KEY file. It allows read access for all users of the machine and the virtual service account (NT SERVICE\AVEVAFailover). The private KEY file can be found in a subdirectory named Keys. This folder is only accessible by machine administrators and the virtual service account.

The Certificates folder also contains a folder named Archive.  This folder is normally empty, but it may contain copies of certificate and/or key files that are detected as invalid when the service starts.  These may be useful when troubleshooting any problems with certificates.

**Note:** The certificate used by Client Failover Service must be trusted by the device running the adapter. If it is not trusted, the [ValidateEndpointCertificate](configuration/health-endpoints.md) must be set to false. 

If the SSL certificate is set to expire within 30 days, the message log receives a warning message. If the SSL certificate has expired, the service logs an error message to the log, but continues to use the certificate. 

## Replacing the SSL Certificate

The certificate that the Client Failover Service generates is applicable to most scenarios. However, you may prefer to replace the default self-signed certificate with one issued by a certificate authority. 

To replace the SSL Certificate, an administrator must:

1. Delete the existing self-signed public certificate (with the CRT extension) from the Certificates folder.

2. Convert the CA-issued certificate to a public file with a CRT extension and the certificate's private key to a file with a KEY extension. <br><br> **Note:** The CRT and KEY files must be in PEM format and share a common file name (e.g., MyCertificate.crt and MyCertificate.key).  The KEY file must **not** be password-protected.

3. Stop the service. 

4. Place the CRT file into the Certificates folder and the KEY file into the Keys subdirectory.

5. For each of the above two files, perform the following additional steps to ensure that the service has the correct access to the certificate files:
   * Select the file in Windows Explorer
   * Right-click on the file name and select "Properties"
   * Click the "Security" tab
   * Click the "Edit" button
   * In the "Group or user names" list, select the user under which the Client Failover Service is running; this is normally "AVEVAFailover" but it may have been changed to another domain or user account
   * In the "Permissions" list, click "Allow" for "Full control"

6. Restart the failover service. 

If the service does not start properly, check the message log for additional information. 


