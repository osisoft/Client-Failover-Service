# Authentication
The Adapter Failover Service performs basic authentication on every request and verifies that the account is a member of the required group or groups to be able to complete the request.

For more information on basic authentication, see https://swagger.io/docs/specification/authentication/basic-authentication/

## Accounts
Credentials provided in the basic authentication header of the request are validated. If the credentials are valid, the request is authorized based on membership of the following local groups.

## Groups
The Failover Service creates two local user groups when it is installed. Group membership is used to determine authorization for each request. 

**PIAdapterFailoverUsers:** Users of the Failover Service, typically accounts running adapters. This group is able to configure the failover service and post heartbeat messages. The account specified in the adapter failover configuration needs to be added to this group.

**PIAdapterFailoverAdministrators:** Administrators of the Failover Service. This group is able to delete failover groups and sessions and POST role overrides.

## REST URLs
The following REST URLs table contains examples of endpoints that you can use to manually create requests along with their corresponding required group membership.

| Relative URL | HTTP verb | Action | Group Required |
| ------------ | --------- | ------ | ------|
| clientfailover/groups/{groupID} | DELETE | Deletes the group specified by groupID | PIAdapterFailoverAdministrators |
| clientfailover/groups/{groupID}/clientSessions | GET | Gets the client sessions in the group specified by groupID | PIAdapterFailoverUsers |
| clientfailover/groups/{groupID}/clientSessions/{sessionID} | DELETE | Deletes the client session in groupID with sessionID | PIAdapterFailoverAdministrators |
| clientfailover/groups/{groupID}/clientSessions/{sessionID}/roleoverride | POST | Sets the session's role to the value specified in the request body | PIAdapterFailoverAdministrators |