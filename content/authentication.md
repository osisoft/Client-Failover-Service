# Authentication
The Adapter Failover Service performs basic authentication on every request and verifies that the account is a member of the required group or groups to be able to complete the request.

## Accounts
Credentials provided in the basic authentication header of the request are validated. If the credentials are valid, the request is authorized based on membership of the following local groups.

## Groups
The Failover Service creates two local user groups when it is installed. Group membership is used to determine authorization for each request. 

**PIAdapterFailoverUsers:** Users of the Failover Service, typically accounts running adapters

**PIAdapterFailoverAdministrators:** Administrators of the Failover Service

The group membership required for each type of request can be seen in the {link to endpoints table}.