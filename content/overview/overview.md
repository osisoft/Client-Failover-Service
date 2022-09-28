---
uid: overview
---

# Overview

The Client Failover Service is an application that minimizes data loss by enabling adapter-level failover. This Service manages multiple failover groups by  assigning primary and secondary roles to adapters in each individual failover group. 

This Service acts as an endpoint that receives and sends failover messages to and from adapters. These messages report on the health of the adapter, help inform the adapter of its role within the failover group, and provides users with the ability to monitor the adapter's health.

In the event that a primary adapter stops reporting its own health and status to the Client Failover Service, this Service enables the transition of an adapter in the secondary role to the primary role to ensure continuous data flow. 

The Client Failover Service supports cold, warm, and hot failover modes. 



## Client Failover Service installation

The Client Failover Service is installed with a downloadable install kit. Please see the (Insert Link here) Installation section for additional information. 

This version of the Client Failover Service only supports Windows Operating Systems. Please see the (Insert Link here) System Requirements section for more details. 



## Client Failover Service configuration
The Client Failover Service supports minimal configuration options, all of which can be configured via the Admin endpoint. 

In order to add adapters to a failover group, users need to update the Failover Configuration Facet section in their adapter configuration. 
