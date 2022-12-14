---
uid: PerformARoleOverride
---

# Perform a role override

Administrators can force a secondary session to be the primary session by performing a role override using the POST method using one of the following rest tools: cURL or Postman. The secondary session can be set as primary for a defined amount of time or can be set as the primary indefinitely.

**Note:** If a heartbeat is not received during a period longer than the Failover Timeout and the session becomes stale, the primary session will remain.

## cURL

To perform a role override using cURL:

1. Open a command line.

2. Run a `POST` command, defining the endpoint port, group ID and session ID for the session you want to make primary:

   ```bash
      curl --request POST -d "http://<endpointport>/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride"
      ```
## Postman

To perform a role override using Postman:

1. Select **POST** from the HTTP request drop-down.

2. Using the following link, define the endpoint port, group ID and session ID for the session you want to make primary:

   ```bash
      https://<endpointport>/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride
      ```

3. In the body of the request, enter the Value as **primary**.

4. To set an expiration period, enter the time using the HH:MM:SS format. For example, to set a secondary session as the primary for 8 hours, you would enter 08:00:00.

   If an expiration period is not required, you can remove ExpirationPeriod from the body of the request and the session remains as the Primary session indefinitely.

5. Select **SEND** to complete the override. 

   **Note:** The forced primary session reverts to the default automatic mode by the failover endpoint when the time defined in the ExpirationPeriod expires.
