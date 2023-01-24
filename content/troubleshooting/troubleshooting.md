---
uid: Troubleshooting
---

# Troubleshooting

The Client Failover Service provides features for troubleshooting issues related to connectivity, data flow, and configuration. Resources include adapter logs and the Wireshark troubleshooting tool . If you are still unable to resolve issues or need additional guidance, contact OSIsoft Technical Support through the [OSIsoft Customer Portal](https://my.osisoft.com/).

**Note:** Make sure to also check the troubleshooting information specific to the adapter in the subsequent user guide.

## Logs

Client Failover Service logs messages in event viewer. Messages from the Client Failover Service logs provide information on the status of the service, groups, sessions, adapters in the client failover service.

Perform the following steps to view the Client Failover Service logs:

1. Navigate to the Event Viewer: <br> 
   Event Viewer > Windows Logs > Application
   Source for the logs is 'Client Failover Service'.
   
   **Example:**<br> A successful message when client gets promoted from Secondary to Primary in the event viewer log:

    ```json
    [11:12:18:075 INF 0HMMN3GUU0D8T:0000000F] Client 'f9d86db5-65c5-462b-8519-8d332dbcaf66' promoted to Primary. 
    Reason: Only one client in group.
    ```

2. Optional: Change the log level of the Client Failover Service to receive more information and context. 

### ASP .NET Core platform log

The ASP .NET Core platform log provides information from the Kestrel web server that hosts the application. The log could contain information that the adapter is overloaded with incoming data. Perform the following steps to spread the load among multiple adapters:

1. Decrease the scan frequency.
2. Lower the amount of data selection items.

## Wireshark

Wireshark is a protocol-specific troubleshooting tool that supports all current adapter protocols. Perform the following steps if you want to use Wireshark to capture traffic from the data source to the adapter or from the adapter to the OMF destination.

1. Download [Wireshark](https://www.wireshark.org/download.html).
2. Familiarize yourself with the tool and read the [Wireshark user guide](https://www.wireshark.org/docs/wsug_html_chunked/).

## Health and diagnostics egress to PI Web API

The adapter sends health and diagnostics data to PI Web API; in some cases, conflicts may occur that are due to changes or perceived changes in PI Web API. For example, a `409 - Conflict` error message displays if you upgrade your adapter version and the PI points do not match in  the upgraded version. However, data is continued to be sent as long as containers are created, so buffering only starts if no containers are created.

To resolve the conflict, perform the following steps:

1. Stop the adapter.
2. Delete the `Health` folder inside of the `Buffers` folder.
3. Stop PI Web API.
4. Delete the relevant adapter created AF structure.
5. Delete the associated health and diagnostics PI points on any or all PI Data Archives created by PI Web API.
6. Start PI Web API.
7. Start the adapter.
