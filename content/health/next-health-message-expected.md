---
uid: NextHealthMessageExpectedFailover
---

# Next health message expected

This property is similar to a heartbeat. A new value for `NextHealthMessageExpected` is sent by an individual Client Failover Service component on a periodic basis while it is functioning properly. This value is a timestamp that indicates when the next value should be received. 

When monitoring, if the next value is not received by the indicated time, this likely means that there is an issue. It could be an issue with the Client Failover Service, network connection between the health endpoint and the Service, and so on.

| Property                        | Type                                 | Description                            |
|---------------------------------|--------------------------------------|----------------------------------------|
| **Time**                        | `string`                             | Timestamp of the event                 |
| **NextHealthMessageExpected**   | `string`                             | Timestamp when next value is expected  |
