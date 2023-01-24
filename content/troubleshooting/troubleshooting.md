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

   To resolve the conflict, please refer to this document: <br>
   https://docs.aveva.com/bundle/pi-adapter-mqtt/page/main/shared-content/troubleshooting/troubleshooting.html

2. The Client Failover Service sends tracing data to PI Web API, when log level is set to Verbose.
   
   **Example:**<br> A successful message after receiving response from get configuration endpoint. 
   
   ```json
   [15:17:10:773 VRB PIWebAPI:00000002] [Basic] HTTP GET /api/v1/configuration responded 200 in 2538.1131 ms
   ```
