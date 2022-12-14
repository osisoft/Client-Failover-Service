---
uid: DeleteASession
---

# Delete a session

Sessions in the Client Failover Service must be deleted individually using one of the following REST tools: cURL or Postman.

## cURL

To delete a session using cURL:

1. Open a command line.

2. Run a `DELETE` command, defining the endpoint port, group ID and session ID to delete:

   ```bash
      curl --request DELETE "http://<endpointport>/api/v1/clientfailover/groups/<groupID>/clientsessions/<sessionID>"
      ```

## Postman

To delete a session using Postman:

1. Select **Delete** from the HTTP request drop-down.

2. Using the following link, define the endpoint port, group ID and session ID for the session you want to delete:

   ```bash
      http://<endpointport>/api/v1/clientfailover/groups/<groupID>/clientsessions/<sessionID>
      ```

3. Select **Send** to delete the session. 
