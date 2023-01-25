---
uid: HealthAndDiagnosticsFailover
---

# Health and Diagnostics

The Client Failover Service produces various types of health data. You can use health data to ensure that your Client Failover Service is running properly. For more information on available Client Failover Service health data, see [health](xref:ClientFailoverHealth).

The Client Failover Service also produces diagnostic data which lives alongside the health data. You can use diagnostic data to find more information about a particular Client Failover Service instance. 

The data can be sent to both PI Web API endpoints or AVEVA Data Hub endpoints. For more information on configuring health, see [Health Endpoints](xref:HealthEndpoints).

## Health endpoint differences

Two OMF endpoints are currently supported for health data:

- PI Web API
- AVEVA Data Hub

There are a few differences in how these two systems treat the associated health and diagnostics data.

- PI Web API parses the information and sends it to configured PI servers for the OMF endpoint. The static data is used to create an AF structure on a PI AF server. The dynamic health data is time-series data that is stored in PI points on a PI Data Archive. You can see it in the AF structure as PI point data reference attributes.

- In AVEVA Data Hub, both health and diagnostics data are created as assets. The data are available in the Asset Explorer and you can use them in the ADH Trend feature. For more information, see the AVEVA Data Hub documentation [Assets](https://docs.osisoft.com/bundle/ocs/page/add-organize-data/organize-data/assets/asset-concept.html). For dynamic data, each value is its own stream with the timestamp property as the single index.

## AF structure

With a health endpoint configured to a PI server, you can use PI System Explorer to view the health and diagnostics of the Client Failover Service. The element hierarchy is shown here.

- The **Elements** root contains a link to the **Client Failover Services** node. This is the root node for all Client Failover Service instances. Each instance of **ClientFailoverService** element contains the diagnostic data for the corresponding service following the format of `{ComputerName}.ClientFailoverService`. For example, in the following image, the computer name is “USOAKL10657”.

    ![Health&Diagnostics](../images/elements-root.png)

- Under each **ClientFailoverService**, you will find a **ClientFailover** node. Each node's name is defined by the node's corresponding computer name, service name, and component type in the following format: `{ComputerName}.ClientFailoverService.ClientFailover`.
  
![Health&Diagnostics](../images/client-failover-node.png)

- To view the diagnostics or health values, select the desired element and then select **Attributes**.