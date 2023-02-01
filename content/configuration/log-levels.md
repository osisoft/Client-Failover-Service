---
uid: LogLevels
---

# Log levels

The Client Failover Service writes log messages to the application log. To view these messages, open the Windows Event Viewer, select **Windows Logs | Application**, and look for events with a source of "Client Failover Service". 

## Logging parameters

The following parameter is available to configure logging:

| Parameter                 |  Type     | Description                                                  |
| ------------------------- | --------- | ------------------------------------------------------------ |
| LogLevel                   | string    | The current logging level of the service. This parameter sets the severity level for the messages that are included in the log. <br><br> The default for this parameter is **Information**. <br><br> Additional levels include (in low to high severity order): *Verbose, Debug, Information, Warning, Error, Fatal* <br><br> For additional information on logging levels, see the table below. <br><br> When a level is defined, you will receive the level set as well as all severity levels above your defined level. For example, if you set the level to **Warning**, you will also receive **Error** and **Fatal** messages in logs as well.|

### Logging levels defined

| Parameter                 | Description                                                  |
| ------------------------- | ------------------------------------------------------------ |
| Verbose                    | Logs that contain the most detailed messages. These messages may contain sensitive application data like actual received values. <br><br> **Note:** These messages should not be enabled in production environment. |
| Debug                     | Logs that can be used to troubleshoot data flow issues by recording metrics and detailed flow related information. |
| Information               | Logs that track the general flow of the application. Any non-repetitive general information like the following can be useful for diagnosing potential application errors: <br><br> - Version information related to the software at startup <br> - External services used <br> - Data source connection string <br> - Number of measurements <br> - Egress URL <br> - Change of state “Starting” or “Stopping” <br> - Configuration |
| Warning                   | Logs that highlight an abnormal or unexpected event in the application flow that does not otherwise cause the application execution to stop. Warning messages can indicate an unconfigured data source state, an insecure communication channel in use, or any other event that could require attention but does not impact data flow. |
| Error                     | Logs that highlight when the current flow of execution is stopped due to a failure. These should indicate a failure in the current activity and not an application-wide failure. It can indicate an invalid configuration, unavailable external endpoint, or an internal flow error. |
| Fatal                     | Logs that describe an unrecoverable application or system crash or a catastrophic failure that requires immediate attention. This can indicate application wide failures like beta timeout expired, unable to start self-hosted endpoint, or unable to access vital resource (for example, Data Protection key file). |

## Change log levels

Administrators can change the log level using cURL or Postman.

### cURL

To change the log level using cURL:

1. Open a command line.

2. Run a `PUT` command, defining the host and the port number:

```
curl -i -k -u <username>:<password> -X PUT "https://<host>:<port>/api/v1/configuration/logging" -H "Content-Type: application/json" --data-raw "{ "LogLevel": "Information" }"
```

For additional information on the curl parameters, such as -i or -k, refer to the [Configuration Tools](xref:ConfigurationTools) section.

### Postman

**Note:** All endpoints in Postman require basic authorization. For more information on basic authorization, refer to the [Configuration Tools](xref:ConfigurationTools) section.

To change the log level using Postman:

1. Select **PUT** from the HTTP request drop-down.

2. Enter the following for the Request URL, defining the host and the port number:

   ```
   https://<host>:<port>/api/v1/configuration/logging
   ```

3. In the body of the request, enter the following and change the level to the desired value:

   ```json
   {
       "LogLevel": "Information"
   }
   ```

4. Select **SEND** to change the log level. 
