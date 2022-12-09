# Authentication
The Client Failover Service performs basic authentication on every request and verifies that the account is a member of the required group or groups to be able to complete the request.

## Accounts
Credentials provided in the basic authentication header of the request are validated. If the credentials are valid, the request is authorized based on membership of the following local groups.

## Groups
The Failover Service creates two local user groups when it is installed. Group membership is used to determine authorization for each request. 

**AVEVAFailoverUsers:** Users of the Failover Service, typically accounts running adapters. Members of this group are able to configure the failover service and post heartbeat messages. The account specified in the adapter failover configuration must be a member of this group.

**AVEVAFailoverAdministrators:** Administrators of the Failover Service. Members of this group are able to delete failover groups, delete sessions, post role overrides, and get or put the global configuration.

## REST URLs
The following REST URLs table contains examples of endpoints that you can use to manually create requests along with their corresponding required group membership.

| Relative URL | HTTP verb | Action | Group Required |
| ------------ | --------- | ------ | ------|
| api/v1/clientfailover/groups/{groupID} | GET | Gets all existing groups | AVEVAFailoverUsers |
| api/v1/clientfailover/groups/{groupID} | DELETE | Deletes the group specified by groupID | AVEVAFailoverAdministrators |
| api/v1/clientfailover/groups/{groupID}/clientSessions | GET | Gets the client sessions in the group specified by groupID | AVEVAFailoverUsers |
| api/v1/clientfailover/groups/{groupID}/clientSessions/{sessionID} | DELETE | Deletes the client session in groupID with sessionID | AVEVAFailoverAdministrators |
| api/v1/clientfailover/groups/{groupID}/clientSessions/{sessionID}/roleoverride | POST | Sets the session's role to the value specified in the request body | AVEVAFailoverAdministrators |
| api/v1/configuration | GET | Gets the global configuration | AVEVAFailoverAdministrators |
| api/v1/configuration | PUT | Sets the global configuration | AVEVAFailoverAdministrators |
