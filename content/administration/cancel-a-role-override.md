---
uid: CancelaRoleOverride
---

# Cancel a role override

An administrator can cancel a role override at any time by using the OFF option. This allows the session’s role to be automatically calculated by the failover engine.

## cURL

To cancel an override using cURL:

1. Open a command line.

2. Run a `POST` command, defining the endpoint port, group ID and session ID:

   ```bash
      curl -d '{"Value":"Primary"}' - request POST "https://<endpointport>/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride"
      ```

## Postman

To cancel an override using Postman:

1. Select **POST** from the HTTP request drop-down.

2. Using the following link, define the endpoint port, group ID and session ID for the session you want to cancel:

   ```bash
      https://<endpointport>/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride
      ```

3. In the body of the request, enter the Value as **OFF**.

   ```bash
   {
      "Value": "Off"
   }
      ```

4. Select **Send** to cancel the role override. 







