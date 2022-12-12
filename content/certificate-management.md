---
uid: CertificateMgmtFailover
---

# Certificate Management

To enable HTTPs for REST API endpoints, the server requires an SSL certificate. Certificates identify client applications and machines on servers and allow for building a secure communication link. The Client Failover Service generates a self-signed certificate with a 15-year expiration date during installation. Instead of being in the machine’s certificate store, the certificate can be found in a data folder ((%PROGRAMDATA%/AVEVA/Adapter Failover Service/Certificates) on your machine. This is for future compatibility with Linux.

The certificates folder contains a public CRT certificate file and a private KEY file. The public certificate file allows read/write access for the machine’s user and the virtual service account. The private KEY file can be found in a subdirectory named Keys. This folder is only accessible by machine administrators and the virtual service account.

**Note:** The certificate used by Client Failover Service must be trusted by the device running the adapter. If it is not trusted, the ValidateEndpointCertificate configuration must be set to false. 

If the SSL certificate is set to expire within 30 days, the message log receives a warning message. If the SSL certificate has expired, the service logs an error message to the log, but continues to use the certificate. 

## Replacing the SSL Certificate

The certificate that the Client Failover Service generates is applicable to most scenarios. However, you may prefer to replace the default self-signed certificate with one issued by a certificate authority. 

To replace the SSL Certificate, an administrator must:

1. Delete the existing public certificate from the Certificates folder.

2. Convert the CA issued certificate to a public and a private file. <br><br> **Note:** The CRT and KEY files must be in PEM format and share a common file name. 

3. Stop the service. 

4. Place the CRT file into the Certificates folder and the KEY file into the Keys subdirectory. 

5. Restart the failover service. 

If the service does not start properly, check the message log for additional information. 


