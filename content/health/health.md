---
uid: ClientFailoverHealth
---

# Health

Client Failover Service produces various kinds of health data that can be egressed to different health endpoints.

To egress health related data, you must configure a health endpoint first. See the [Health endpoints](xref:HealthEndpoints) configuration for additional information.

## Available health data

Dynamic data is sent every minute to configured health endpoints.

The following health data is available:

- [Device status](xref:DeviceStatusFailover)
- [Next Health Message Expected](xref:NextHealthMessageExpectedFailover)
- FailoverObjectCount
   - Sessions - The number of active sessions (adapters) communicating with the Client Failover Service.
   - Groups - The total number of groups configured in the ClientFailoverService. 
