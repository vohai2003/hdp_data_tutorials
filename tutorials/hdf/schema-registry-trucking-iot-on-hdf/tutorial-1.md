---
title: Benefits of a Schema Registry
---

# Schema Registry in Trucking IoT on HDF

## Benefits of a Schema Registry

## Introduction

So what is Schema Registry and what benefits does it provide?  Would using it make a data pipeline more robust and maintainable?  Let us explore exactly what Schema Registry is and how it fits into modern data architectures.

## Prerequisites

-   [Hortonworks DataFlow (HDF) Sandbox Installed](https://hortonworks.com/downloads/#sandbox)
-   Some understanding of schemas and serialization

## Outline

-   [What is Schema Registry?](#what-is-schema-registry)
-   [Smaller Payloads](#smaller-payloads)
-   [Differing Schemas](#differing-schemas)
-   [Schema Evolution](#schema-evolution)
-   [Next: A Closer Look At The Architecture](#next-a-closer-look-at-the-architecture)


## What is Schema Registry?

> TODO: SR graphic/screenshot goes here.

Schema Registry provides a centralized repository for schemas and metadata, allowing services to flexibly interact and exchange data with eachother without the challenge of managing and sharing schemas between them.

Schema Registry has support for multiple underlying schema representations (Avro, JSON, etc.) and is able to store a schema's corresponding serializer and deserializer.


## Smaller Payloads

Typically, when serializing data for transmission using schemas, the actual schema (text) needs to be transmitted with the data.  This results in an increase of payload size.

Using Schema Registry, all schemas are registered with a central system.  Data producers no longer need to include the full schema text with the payload, but instead only include the ID of that schema, also resulting in speedier serialization.

> TODO: Payload graphic goes here.


## Differing Schemas

Consider the case where thousands of medical devices are reading the vitals of patients and relaying information back to a server.

The services and applications in your pipeline are expecting data using a specific format and fields that these medical devices use.

What about when medical devices from a different vendor are added to the system?  Data in a different format carrying a different set of fields would typically require updates to the different components of your data pipeline.

**Schema Registry enables generic format conversion and generic routing**, allowing you to build a resilient pipeline able to handle data in different format with varying sets of fields.


## Schema Evolution

Following the use-case above, consider the case when the software in some of the medical devices you are collecting data from is updated.  Some devices now collect new datapoints, while other devices report to same limited number of fields as before.  Similarly, consider when the processing step in the pipeline is altered to output data with fewer or more fields than its previous version.  Typically, for either of these cases, the rest of your pipeline would need to be upated to handle these changes.

**With Schema Registry, the different components in your architecture (IoT devices, routing logic, processing nodes, etc.) can evolve at different rates.**  Components can change the shape of its data while Schema Registry handles the translation from one schema to another, ensuring compatibility with downstream services.


## Next: A Closer Look At The Architecture

Congratulations, you've finished your first tutorial!  Including a review of the tutorial or tools they now know how to use would be helpful.
