---
uid: overview
---

# Overview

The Client Failover Service is an application that minimizes data loss by enabling adapter-level failover. This service manages multiple failover groups by  assigning primary and secondary roles to adapters in each individual failover group.

This service acts as an endpoint that receives and sends failover messages to and from adapters. These messages report on the health of the adapter, help inform the adapter of its role within the failover group, and provides users with the ability to monitor the adapter's health.

If a primary adapter stops reporting its own health and status to the Client Failover Service, this service promotes an adapter in the secondary role to the primary role to ensure continuous data flow.

The Client Failover Service supports cold, warm, and hot failover modes.

**Note:** Only the 1.4 version of OPC UA and the 1.3 version of MQTT currently support the Client Failover Service. 

## Client Failover Service installation

The Client Failover Service is installed with a downloadable install kit. See the [Installation section](xref:Installation) for additional information.

This version of the Client Failover Service only supports Windows Operating Systems. See the [System Requirements](xref:SystemRequirements) section for more details.

## Client Failover Service configuration

The Client Failover Service supports minimal configuration options, all of which can be configured using REST endpoints.

To add adapters to a failover group, you must update the Failover Configuration Facet section in the adapter configuration.
