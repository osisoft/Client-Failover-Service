---
uid: DeviceStatusFailover
---

# Device status

The device status indicates the health of this component and whether it is running properly. This time-series data is stored within a PI point or AVEVA Data Hub stream, depending on the endpoint type. During healthy steady-state operation, a value of `Good` is expected.

| Property                        | Type                                 | Description                     |
|---------------------------------|--------------------------------------|---------------------------------|
| **Time**                        | `string`                             | Timestamp of the event          |
| **DeviceStatus**                | `string`                             | The value of the `DeviceStatus` |

The possible statuses are:

| Status                          | Meaning                               |
|---------------------------------|---------------------------------------|
| `Good`                          | The service is running and operating normally. |
| `DeviceInError`                 | The service has encountered an error that requires intervention. One example is that the certificate is expired. Refer to the logs for more information. |
| `Shutdown`                      | The service is either in the process of shutting down or has finished. |
