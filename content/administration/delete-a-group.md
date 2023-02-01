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

   ```
   curl -i -k -u <username>:<password> -X DELETE "https://<host>:<port>/api/v1/clientfailover/groups/<groupID>"
   ```

For additional information on the curl parameters, such as -i or -k, refer to the [Configuration Tools](xref:ConfigurationTools) section.

## Postman

**Note:** All endpoints in Postman require basic authorization. For more information on basic authorization, refer to the [Configuration Tools](xref:ConfigurationTools) section.

To delete a group using Postman:

1. Select **Delete** from the HTTP request drop-down.

2. Use the following Request URL, defining the endpoint host, port, and group ID:

   **Note:** To delete a group, there cannot be any active open sessions within the group.

   ```
   https://<host>:<port>/api/v1/clientfailover/groups/<groupID>
      ```

3. Select **Send** to delete the group.
