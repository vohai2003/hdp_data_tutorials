---
title: Sandbox Port Forwarding Guide
author: sandbox-team
tutorial-id: 623
experience: Intermediate
persona: Administrator
source: Hortonworks
use case: Single View
technology: Sandbox
release: hdp-2.6.5
environment: Sandbox
product: HDP
series: HDP > Hadoop Administration > Hortonworks Sandbox
---

# Sandbox Port Forwarding Guide

# Current Sandbox Architecture

## Introduction

This informational tutorial will explain the current Hortonworks Sandbox architecture, starting in HDP 2.6.5 a new Sandbox structure is introduced making it possible to instantiate two single node clusters (i.e. HDP and HDF) within a single Sandbox with the purpose of combining the best features of the Data-At-Rest and Data-In-Motion methodologies in a single environment. Have a look at the graphical representation of the Sandbox below, it shows where the Sandbox exists in relation to the outside world, the instance depicted is of the Connected Data Architecure (CDA) if you are not yet familiarized with the concept of CDA do not worry, we will review it at a later section.

![cda-architecture](assets/cda-architecture.jpg)

At a high level the Sandbox is a Linux (CentOS 7) Virtual Machine leveraging docker to host different Sandbox distributions, namely [HDP](https://hortonworks.com/products/data-platforms/hdp/) or [HDF](https://hortonworks.com/products/data-platforms/hdf/). In order to orchestrate communication between the outside world and the Sandbox a reverse proxy server NGINX is containerized and configured to only open the ports needed to the outside enabling us to granularly interact with each container.

## Prerequisites

- Sandbox [Deployment and Install Guide](https://hortonworks.com/tutorial/sandbox-deployment-and-install-guide/)
- Learning the Ropes of the [HDP Sandbox](https://hortonworks.com/tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)

## Outline

- [Docker Architecture](#docker-architecture)
- [HDP vs HDF](#hdp-vs-hdf)
- [What is CDA?](#what-is-cda)
- [Native Docker Sandbox](#native-docker-sandbox)
- [Summary](#summary)
- [Further Reading](#further-reading)

## Docker Architecture

[![cda-architecture](assets/docker-architecture.jpg)](https://docs.docker.com/engine/docker-overview/)

In the Docker architecture above, Docker registry are services used for storing Docker images, such as Docker Hub. Docker Host is the computer Docker runs on. Diving deeper into the host, you can see the Docker Daemon, which is used to create and manage Docker objects, such as images, containers, networks and volumes. The user or client is able to interact with Docker daemon via Client Docker CLI. The Docker daemon is a long-running program also known as a server. The CLI utilizes Docker’s REST API to interact with the Docker daemon. As you can observe, the Docker Engine is a client-server application comprised of Client Docker CLI, REST API and Docker daemon.

### View Running Containers

If you would like to visualize the running Sandbox container and proxy you you must log on to the host, you may chose to follow along; however, it is not necessary. If you use the standard sandbox `ssh -p 2222 root@sandbox-hdp.hortonworks.com`, you will actually log into the sandbox container, not the containing VM where Docker changes are made. You want to log into the VM running Docker with the following command:

If you are running a VirtualBox Sandbox:

~~~bash
# SSH on to the sandbox using Virtual Box
ssh root@sandbox-hdp.hortonworks.com -p 2202
~~~

Or if you are using VMWare:

~~~bash
# SSH on to the sandbox using VMWare
ssh root@sandbox-hdp.hortonworks.com -p 22
~~~

> Note: The default password is **hadoop**.

Now that you are in the Virtual Machine hosting the containers view the running containers within docker:

~~~bash
docker ps
~~~

If you started out with HDP you will see two containers running, the first is the NGINX proxy container followed by a list of open ports and where they are being forwarded. Since HDP was used as a base we can see that it is listed as a running container.

![docker-ps](assets/docker-ps.jpg)

 here is some context on the information displayed:

|                      CONTAINER ID                      |                                   IMAGE                                  |                                          COMMAND                                          |                 CREATED                 |                              STATUS                             |                                            PORTS                                            |                              NAMES                              |
|:------------------------------------------------------:|:------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------:|:---------------------------------------:|:---------------------------------------------------------------:|:-------------------------------------------------------------------------------------------:|:---------------------------------------------------------------:|
| Container ID given to an instantiated image by docker. | The executable package from which your container has been instantiated.  | Command used to instantiate your container, typically this is the path of an initialization script. | How long ago the container was created. | A container may be: </br>UP</br> UP-PAUSED </br>RESTARTING </br>DEAD </br>CREATED </br>EXITED | Open ports. Note that the proxy container also tells us where ports are being forwarded to. | This is the container name e.g. "sandbox-hdp" & "sandbox-proxy" |

When CDA has been deployed both HDP and HDF are displayed as running containers:

![cda-dockerps](assets/cda-dockerps.jpg)

### Native Docker Sandbox

The Sandbox may also run using Docker which is native to the host operating system; for example, rather than running a VM to instantiate the containers you may directly interact with the docker daemon

The script in the VM that creates configures the proxy server is located at:

~~~bash
/sandbox/proxy/generate-proxy-deploy-script.sh
~~~

## HDP vs HDF

![hdp-stand-alone](assets/both-stand-alone.jpg)

### HDF (Data-In-Motion)

Data-In-Motion is the idea where data is being ingested from all sorts of different devices into a flow or stream. While the data is moving throughout this flow, components or as NiFi calls them “processors” are performing actions on the data to modify, transform, aggregate and route it. Data-In-Motion covers a lot of the preprocessing stage in building a Big Data Application. For instance, data preprocessing is where Data Engineers work with the raw data to format it into a better schema, so Data Scientists can focus on analyzing and visualizing the data.

### HDP (Data-At-Rest)

Data-At-Rest is the idea where data is not moving and is stored in a database or robust datastore across a distributed data storage such as Hadoop Distributed File System (HDFS). Instead of sending the data to the queries, the queries are being sent to the data to find meaningful insights. At this stage data, data processing and analysis occurs in building a Big Data Application.

## What is CDA?

Hortonworks Connected Data Architecture (CDA) is composed of both Hortonworks DataFlow (HDF) and Hortonworks DataPlatform (HDP) sandboxes and allows you to play with both data-in-motion and data-at-rest frameworks simultaneously.

![hortonworks-connected-data-platforms](assets/HDF_secure_data_collection.png)

As data is coming in from the edge, it is collected, curated and analyzed in real-time, on premise or in the cloud using the HDF framework. You can also convert the your Data-In-Motion into Data-At-Rest with the HDP framework. HDP allows you to store, manage and perform further analytics. 

In order for HDF to send data into HDP, both sandboxes need to be set up to communicate with each other. If you would like to know more about the deployment of the CDA architecture check out the [Sandbox Deployment and Install Guide](https://hortonworks.com/tutorial/sandbox-deployment-and-install-guide/) under the **Advanced Topic**. When CDA is enabled a script internal to the Sandbox takes into account what base you started with and calls on the Docker daemon to instantiate the image of the complementing Sandbox flavour (e.g. HDP installs HDF, and HDF installs HDP).

In the image below we used HDP as our base and launched the initialization script for CDA as you can see all the needed components for HDF are being loaded into a new container:

![pulling-hdf](assets/pulling-hdf.jpg)

CDA takes advantage of the sandboxes properties of being Docker containers by taking the HDF Docker container as the base sandbox inside a virtual machine. A custom Docker network was created between the running containers through Docker Engine. One of the many advantages of being a container inside Docker Engine is that containers can communicate directly with each other through a Docker network named bridge.

![cda-network](assets/cda-network.jpg)

## Summary

Congratuations, you have learned a great deal about the structure of our Sandbox, how HDP and HDF are implemented and you have learned about the Sandbox architecture and how CDA is implemented using Docker containers. Additionally, you have learned about the inter-container communication made possible by Docker's internal network.

## Further Reading

- [Hortonworks Connected Data Platforms](https://hortonworks.com/products/data-platforms/)
- [HDP Documentation](https://docs.hortonworks.com/HDPDocuments/HDP2/HDP-2.6.5/index.html)