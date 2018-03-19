---
title: Schema Registry Architecture
---

# Schema Registry in Trucking IoT on HDF

## Schema Registry Architecture

## Introduction

This is the introductory paragraph for the tutorial.  It should introduce the reader to what they're about to learn and do in this particular section of the tutorial series.


## Outline

-   [Main Components](#main-components)
-   [Schema Entities](#schema-entities)
-   [Integration with HDF](#integration-with-hdf)
-   [Next: Using the Web Interface](#next-using-the-web-interface)


## Main Components

> TODO: Cleaned up image from (https://docs.hortonworks.com/HDPDocuments/HDF3/HDF-3.1.1/bk_overview/content/ch04s03.html) goes here.

Schema Registry has the following main components:

Component | Description
--- | --- | ---
Registry Web Server | Web Application exposing the REST endpoints you can use to manage schema entities. You can use a web proxy and load balancer with multiple Web Servers to provide HA and scalability.
Schema Metadata Storage | Relational store that holds the metadata for the schema entities. In-memory storage and mySQL databases are supported.
Serdes Storage | File storage for the serializer and deserializer jars. Local file system and HDFS storage are supported.
Schema Registry Client | A java client that HDF components can use to interact with the RESTful services.

> TODO: Cleaned up image from slideshow (check snagit) goes here.


## Schema Entities

Schema Registry can be seen as being made up of different type of metadata entities.

> TODO: Cleaned up graphic from (https://docs.hortonworks.com/HDPDocuments/HDF3/HDF-3.1.1/bk_overview/content/schema-entities.html) can go here.

Entity | Description | Example
--- | --- | ---
Schema Group | A logical grouping of similar schemas. A Schema Group can be based on any criteria you have for managing schemas.  Schema Groups can have multiple Schema Metadata definitions. | The group name **trucking_data_truck** or **trucking_data_traffic**
Schema Metadata	| Metadata associated with a named schema. A metadata definition is applied to all the schema versions that are assigned to it. | Key metadata elements include: Schema Name, Schema Type, Description, Compatibility Policy, Serializers/Deserializers
Schema Version | The versioned schema (the actual schema text) associated with a schema metadata definition. | (Schema text example in following sections)


## Integration with HDF

When Schema Registry is paired with other services available as part of the Hortonworks DataFlow (HDF), integration with Schema Registry is baked in.

Component | Schema Registry Integration
--- | ---
NiFi | New processors and controller services in NiFi interact with Schema Registry.  This allows creating flows using drag-and-drop processors that grant the benefits mentioned in the previous section without writing any code.
Kafka | A Kafka serializer and deserializer that uses Schema Registry is included with Kafka, allowing events to be marshalled and unmarshalled automatically.
Streaming Analytics Manager (SAM) | Using a drag-and-drop paradigm to create processing jobs, SAM will automatically infer schema from data sources and sinks, ensuring that data expected by connected services are compatible with one another.


## Next: Using the Web Interface

Congratulations, you've finished your first tutorial!  Including a review of the tutorial or tools they now know how to use would be helpful.
