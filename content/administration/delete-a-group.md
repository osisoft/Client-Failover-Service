---
uid: DeleteAGroup
---

# Delete a group

Groups in the Client Failover Service must be deleted individually using one of the following REST tools: cURL or Postman.

## cURL

To delete a group using cURL:

1. Open a command line.

2. Run a `DELETE` command, defining the endpoint port and group ID:

   **Note:** To delete a group, there cannot be any active open sessions within the group. 

   ```bash
      curl --request DELETE "https://<endpointport>/api/v1/clientfailover/groups/<groupID>"
      ```

## Postman

To delete a group using Postman:

1. Select **Delete** from the HTTP request drop-down.

2. Using the following link, define the endpoint port and group ID:

   **Note:** To delete a group, there cannot be any active open sessions within the group. 

   ```bash
      https://<endpointport>/api/v1/clientfailover/groups/<groupID>
      ```

3. Select **Send** to delete the group. 
