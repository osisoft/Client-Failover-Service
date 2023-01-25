---
uid: DeviceStatusFailover
---

# Device status

The device status indicates the health of this component and whether it is running properly. This time-series data is stored within a PI point or AVEVA Data Hub stream, depending on the endpoint type. During healthy steady-state operation, a value of `Good` is expected.

| Property                          | Type                                 | Description                    |
|-----------------------------------|--------------------------------------|--------------------------------|
| **Time**                        | `string`                               | Timestamp of the event        |
| **DeviceStatus**                | `string`                               | The value of the `DeviceStatus` |

The possible statuses are:

| Status                          | Meaning                               |
|-----------------------------------|---------------------------------------|
| `Good`                          | The component is connected to the data source and it is collecting data. |
| `DeviceInError`                 | The component encountered an error either while connecting to the data source or attempting to collect data. |
| `Shutdown`                      | The component is either in the process of shutting down or has finished. |
