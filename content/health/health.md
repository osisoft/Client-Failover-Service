---
uid: AdapterHealthFailover
---

# Health

Client Failover Service produces various kinds of health data that can be egressed to different health endpoints.

To egress health related data, you have to configure a health endpoint first. See [Health endpoint configuration](xref:HealthEndpointConfiguration).

## Available health data

Dynamic data is sent every minute to configured health endpoints.

The following health data is available:

- [Device status](xref:DeviceStatus)
- [Next Health Message Expected](xref:NextHealthMessageExpected)
