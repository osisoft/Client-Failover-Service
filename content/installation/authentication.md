---
uid: AuthenticationFailover
---

# Authentication

## Authentication Methods

The Client Failover Service supports the following authentication methods for PI Adapter clients and REST tools.

### Kerberos

Kerberos provides per-user security that is native to Windows and Active Directory, and is supported with PI Adapters and some REST clients. Kerberos does not rely on credentials being transmitted across the wire, which makes it ideal for use with untrusted connections.

If the Client Failover Service is running with the default identity of "NT SERVICE\AVEVAFailover", it is not necessary to configure Service Principal Names (SPNs) on the machine where the service is running.  However, if the service identity is changed to a domain user account, the following SPNs must be configured and associated with that domain account:

  * HTTP/*hostname*
  * HTTP/*fully.qualified.hostname*

> Note: If the failover service runs as a domain account but the SPN is not set up correctly, the following error message (excerpt) can be expected in the adapter log. The resolution is to set up the SPN for domain account under which the client failover service is running. 
> 
> `[Error] Could not send heartbeat to endpoint https://<failover service node>:<Port>/api/v1/clientfailover/ {"OperationId":"86e17027c84c4e1721b438606db413be","Error":"An error occurred.","Reason":"System.InvalidOperationException: An anonymous request was received in between authentication handshake requests..."}`
  
### Basic

Basic authentication is defined in the Request for Comments document [RFC 2617 HTTP Authentication](https://www.ietf.org/rfc/rfc2617.txt)
and is supported by PI Adapters and most REST clients (e.g., cURL and Postman). Basic authentication as implemented in the Client Failover Service
is simple to use, provides granular, per-user security based on Windows identity, and can help avoid configuration problems related to Kerberos. 
When combined with SSL, as in all Client Failover Service requests, Basic authentication is reasonably secure.

However, Basic authentication is less secure than Kerberos, since Windows user credentials, though encrypted, must be included and are transmitted with each request. In addition, Basic authentication requires that the Client Failover Service keeps the decrypted username and password in memory for the duration of the request. You should not use Basic authentication unless you are confident of the security of the server on which you are running the Client Failover Service.

## Groups
The Failover Service creates two local user groups when it is installed. For both Kerberos and Basic authentication, the Client Failover Service performs authorization on every request and validates the requesting account. When Basic authentication is used, the account specified as "Username" in the adapter's failover configuration must be a member of the required group. When Kerberos authentication is used, the service account for the adapter must be a member of the group.

**AVEVAFailoverUsers:** Users of the Failover Service, typically accounts running adapters. Members of this group are able to configure the failover service (such as creating failover groups/sessions and delete sessions) and post heartbeat messages. The account specified in the adapter failover configuration must be a member of this group.

**AVEVAFailoverAdministrators:** Administrators of the Failover Service. Members of this group are able to delete failover groups, post role overrides, and modify the global configuration.

## REST URLs
The following REST URLs table contains examples of endpoints that you can use to manually create requests along with their corresponding required group membership.

| Relative URL | HTTP verb | Action | Group Required |
| ------------ | --------- | ------ | ------|
| api/v1/clientfailover/groups/{groupID} | GET | Gets the group specified by groupID | AVEVAFailoverUsers |
| api/v1/clientfailover/groups/{groupID} | DELETE | Deletes the group specified by groupID | AVEVAFailoverAdministrators |
| api/v1/clientfailover/groups/{groupID}/clientSessions | GET | Gets the client sessions in the group specified by groupID | AVEVAFailoverUsers |
| api/v1/clientfailover/groups/{groupID}/clientSessions/{sessionID} | DELETE | Deletes the client session in groupID with sessionID | AVEVAFailoverUsers |
| api/v1/clientfailover/groups/{groupID}/clientSessions/{sessionID}/roleoverride | POST | Sets the session's role to the value specified in the request body | AVEVAFailoverAdministrators |
| api/v1/configuration | GET | Gets the global configuration | AVEVAFailoverAdministrators |
| api/v1/configuration | PUT | Sets the global configuration | AVEVAFailoverAdministrators |
