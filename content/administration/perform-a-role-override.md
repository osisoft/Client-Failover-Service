---
uid: PerformARoleOverride
---

# Perform a role override

Administrators can forcefully promote an adapter in the secondary role to the primary role by performing a role override. You can do this using the
POST method with one of the following REST tools: cURL or Postman. 

The secondary adapter can be set as primary adapter for a defined amount of time or it can be set as the primary indefinitely. This option is particularly useful for maintenance periods when an individual adapter is on a machine that may be restarting often.

## cURL

To perform a role override using cURL:

1. Open a command line.

2. Run a `POST` command, defining the endpoint port, group ID and session ID for the session you want to make primary:

```
curl -i -k -u <username>:<password> -X POST "https://<host>:<port>/api/v1/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride" -H "Content-Type: application/json" --data-raw "{"Value": "Primary"}"
```

For additional information on the curl parameters, such as -i or -k, refer to the [Configuration Tools](xref:ConfigurationTools) section.

## Postman

**Note:** All endpoints in Postman require basic authorization. For more information on basic authorization, refer to the [Configuration Tools](xref:ConfigurationTools) section.

To perform a role override using Postman:

1. Select **POST** from the HTTP request drop-down.

2. Use the following Request URL for the session you want to make primary, defining the endpoint host, port, group ID and session ID:

   ```
   https://<host>:<port>/api/v1/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride
   ```
   
3. In the body of the request, enter the _Value_ as _primary_. To set an expiration period, enter the _ExpirationPeriod_ using the HH:MM:SS format. For example, to set a session as the primary for 8 hours, you would enter 08:00:00. If an expiration period is not required, you can remove ExpirationPeriod from the body of the request and the session remains as the Primary session indefinitely.
      
      ```json
   {
       "Value": "Primary",
       "ExpirationPeriod": "08:00:00"
   }
   ```
   
   | Parameter            | Required      | Type          | Description                     |
   |----------------------|---------------|---------------|---------------------------------|
   | Value                | Required      | String        | Set to ‘Primary’ to promote the adapter to the Primary role. Set to ‘Secondary’ to demote to the secondary role. Set to ‘Off’ to remove the role override. |
   | ExpirationPeriod     | Optional      | String in HH:MM:SS format | Enforces the role override for a timed period. If no ExpirationPeriod is set, then the role override will be indefinitely enforced. |
   
   **Note:** The forced primary session reverts to the default automatic mode by the failover endpoint when the time defined in the ExpirationPeriod expires.

4. Select **SEND** to complete the override. 

   **Note:** When heartbeats are not received during a period longer than the Failover Timeout and the session becomes stale, the session will still remain in primary role while the role override is in effect.
   
