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

    ```
    [11:12:18:075 VRB PIWebAPI:0000000F] Client 'f9d86db5-65c5-462b-8519-8d332dbcaf66' promoted to Primary. 
    Reason: Only one client in group.
    ```

2. Optional: [Change the log level](xref:LogLevels) of the Client Failover Service to receive more information and context. 

## Health and diagnostics egress to PI Web API

The Client Failover Service sends health and diagnostics data to PI Web API. In some cases, conflicts may occur that are due to changes or perceived changes in PI      Web API. For example, a `409 - Conflict` error message displays if you upgrade your client failover service version and the PI points do not match in the upgraded      version.

To resolve the conflict, perform following steps:

1. Stop the Client Failover Service.
2. Stop PI Web API.
3. Delete the relevant AF structure and templates.
4. Delete the associated health and diagnostics PI points and digital state sets on any or all PI Data Archives created by PI Web API.
5. Start PI Web API.
6. Start the Client Failover Service.

The Client Failover Service sends tracing data to PI Web API, when log level is set to Verbose.
   
   **Example:**<br> A successful message when data is send to PI Web API.
    ```
    [16:08:23:064 DBG 0HMNQ7IS2FB6H:00000006] Post to https://<Machine Name>/piwebapi/omf successful: Accepted
   Request Content: [{"containerid":"<Machine Name>.ClientFailoverService.System.Diagnostics","values":[{"Timestamp":"2023-01-24T00:08:23.0570163Z","ProcessIdentifier":1676,"StartTime":"2023-01-19T16:33:02.7475975Z","WorkingSet":99.745792,"TotalProcessorTime":7.109375,"TotalUserProcessorTime":5.015625,"TotalPrivilegedProcessorTime":2.09375,"ThreadCount":21,"HandleCount":826,"ManagedMemorySize":14.065176,"PrivateMemorySize":74.09664,"PeakPagedMemorySize":80.596992,"StorageTotalSize":107027.099648,"StorageFreeSpace":77163.081728}]},{"containerid":"<Machine Name>.ClientFailoverService.ClientFailover.DeviceStatus","values":[{"Timestamp":"2023-01-24T00:08:23.0590385Z","DeviceStatus":0}]},{"containerid":"<Machine Name>.ClientFailoverService.ClientFailover.FailoverObjectCount","values":[{"Timestamp":"2023-01-24T00:08:23.0590398Z","Groups":1,"Sessions":2}]},{"containerid":"<Machine Name>.ClientFailoverService.ClientFailover.NextHealthMessageExpected","values":[{"Timestamp":"2023-01-24T00:08:23.0590425Z","NextHealthMessageExpected":"2023-01-24T00:09:23.0590427Z"}]}  
    ```
