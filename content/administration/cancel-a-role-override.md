---
uid: CancelaRoleOverride
---

# Cancel a role override

An administrator can cancel a role override at any time by using the OFF option. This allows the session’s role to be automatically calculated by the failover engine.

## Postman

To cancel an override in Postman:

1. Select **POST** from the HTTP request drop-down.

2. Using the following link, define the endpoint port, group ID and session ID for the session you want to cancel:

   ```bash
      "http://<endpointport>/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride"
      ```

3. In the body of the request, enter the Value as **OFF**

4. Select **Send** to cancel the role override. 







