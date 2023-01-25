---
uid: Troubleshooting
---

# Troubleshooting

The Client Failover Service provides features for troubleshooting issues related to connectivity, authentication, configuration and health. If you are still unable to resolve issues or need additional guidance, contact OSIsoft Technical Support through the [OSIsoft Customer Portal](https://my.osisoft.com/).

## Logs

Client Failover Service logs messages in windows event viewer.

Perform the following steps to view the Client Failover Service logs:

1. Navigate to the Event Viewer: <br> 
   Event Viewer > Windows Logs > Application <br>
   Source for the logs is 'Client Failover Service'.
   
   **Example:**<br> A successful message when client gets promoted from Secondary to Primary in the event viewer log:

    ```json
    [11:12:18:075 INF PIWebAPI:0000000F] Client 'f9d86db5-65c5-462b-8519-8d332dbcaf66' promoted to Primary. 
    Reason: Only one client in group.
    ```

2. Optional: [Change the log level](/content/configuration/log-levels.md) of the Client Failover Service to receive more information and context. 

## Health and diagnostics egress to PI Web API

1. The Client Failover Service sends health and diagnostics data to PI Web API; in some cases, conflicts may occur that are due to changes or perceived changes in PI      Web API. For example, a `409 - Conflict` error message displays if you upgrade your client failover service version and the PI points do not match in the upgraded      version. However, data is continued to be sent as long as containers are created, so buffering only starts if no containers are created.

   To resolve the conflict, please refer to [Clean up the development environment](https://docs.aveva.com/bundle/omf-with-pi-web-api/page/clean-up-the-development-environment.html) in the PI Web API documentation.

2. The Client Failover Service sends tracing data to PI Web API, when log level is set to Verbose.
   
   **Example:**<br> Response received if user is unauthorized. 
   
   ```json
   [10:42:40:106 DBG 0HMNPH3J4VEE4:00000006] Post to https://pi.osisoft.int/piwebapi/omf/ unsuccessful: Unauthorized
   Request Content: [{"containerid":"SPHINX-W11A.ClientFailoverService.System.Diagnostics","values":[{"Timestamp":"2023-01-25T18:42:40.0864423Z","ProcessIdentifier":3968,"StartTime":"2023-01-18T03:33:42.3798201Z","WorkingSet":50.05312,"TotalProcessorTime":135.875,"TotalUserProcessorTime":89.203125,"TotalPrivilegedProcessorTime":46.671875,"ThreadCount":25,"HandleCount":1001,"ManagedMemorySize":12.735408,"PrivateMemorySize":73.998336,"PeakPagedMemorySize":74.002432,"StorageTotalSize":107027.099648,"StorageFreeSpace":64866.410496}]},{"containerid":"SPHINX-W11A.ClientFailoverService.ClientFailover.DeviceStatus","values":[{"Timestamp":"2023-01-25T18:42:40.0908109Z","DeviceStatus":0}]},{"containerid":"W11A.ClientFailoverService.ClientFailover.FailoverObjectCount","values":[{"Timestamp":"2023-01-25T18:42:40.0908126Z","Groups":1,"Sessions":2}]},{"containerid":"W11A.ClientFailoverService.ClientFailover.NextHealthMessageExpected","values":[{"Timestamp":"2023-01-25T18:42:40.0908161Z","NextHealthMessageExpected":"2023-01-25T18:43:40.0908162Z"}]}]
   ```
