---
uid: CancelaRoleOverride
---

# Cancel a role override

An administrator can cancel a role override at any time by using the OFF option. This allows the session’s role to be automatically calculated by the failover engine.

## cURL

To cancel an override using cURL:

1. Open a command line.

2. Run a `POST` command, defining the endpoint port, group ID and session ID:

```
curl -i -k -u <username>:<password> -X POST "https://<host>:<port>/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride" -H "Content-Type: application/json" --data-raw "{"Value": "Off"}"
```

For additional information on the curl parameters, such as -i or -k, refer to the [Configuration Tool](xref:ConfigurationTools) section.

## Postman

**Note:** All endpoints in Postman require basic authorization. For more information on basic authorization, refer to the [Configuration Tool](xref:ConfigurationTools) section.

To cancel an override using Postman:

1. Select **POST** from the HTTP request drop-down.

2. Use the following Request URL for the session you want to cancel, defining the endpoint host, port, group ID and session ID:

```
https://<host>:<port>/clientfailover/groups/<groupID>/clientsessions/<sessionID>/roleoverride
```

3. In the body of the request, enter the Value as **OFF**.

```json
{
   "Value": "Off"
}
```

4. Select **Send** to cancel the role override. 
