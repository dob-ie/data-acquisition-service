# Data Acquisition Service

## Description
A scala version of the Data Acquisition Service based on the **MINTE** approach.

### References
Collarana et al. [MINTE: semantically integrating RDF graphs](https://www.researchgate.net/project/MINTE-A-Semantic-Integration-Approach-for-RDF-Graphs)
Collarana et al. [Synthesizing Knowledge Graphs from web sources with the MINTE+ framework](https://www.researchgate.net/publication/325381996_Synthesizing_Knowledge_Graphs_from_web_sources_with_the_MINTE_framework)

## Dependencies
The reactive project depends on the following software

* JDK 1.8
* Play Web Framework 2.4.6 "Damiya" and Activator 1.3.7

Download Play: https://www.playframework.com/download

Installation steps: https://www.playframework.com/documentation/2.4.x/Installing

This service depends on the Silk Workbench to transform the data collected from the data sources into RDF.
An instance of the workbench must be available with the configuration files containing the transformation rules.
The configuration files for the RDF transformation and all the resources needed to set up an instance of the Silk Workbench are 
provided in the project [Data Integration Workspace](https://github.com/LiDaKrA/data-integration-workspace).
Fuhsen collects data from social networks and other data sources. Some of these require a key to use their API that is 
stored in conf/application.conf. The key must be provided before starting Fuhsen. 

#### IDE support 
The quick and easy way to start compiling, running and coding FuhSen is to use "activator ui".
However, you can also set up your favorits Java IDE (Eclipse or IntellJ Idea). https://www.playframework.com/documentation/2.4.x/IDE

## Install and Build
The service can be installed from the source code on Github or from the Docker image in the [Lidakra repository](https://hub.docker.com/r/lidakra/)

### Install and build from the source code  
To obtain the latest version of the project please clone the github repository

    $ git clone https://github.com/LiDaKrA/FuhSen-reactive.git

The build system for Fuhsen is Sbt. The project can be compiled and run using Sbt or the Typesafe Activator. In order to compile the project with sbt from the project root folder run the command

    $ sbt compile

The project can be packaged in a tar file in /target/universal/ with the command

    $ sbt package universal:packageZipTarball 


Before making a build, update the version of the project in the following files:
.travis.yml, build.sbt, Dockerfile, start_fuhsen.sh

### Install from the Docker image
A Docker image containing Fuhsen can be built from the Docker file or pulled from the Lidakra Repository on Docker Hub.
Once the image has been downloaded or created the configuration file in conf/application.conf must be changed in order to provide
the keys for the data sources used by Fuhsen and also to update the url of the Silk Workbench.
The config file must be provided in a Docker data volume loaded with the config file. As an example copy the config file in 
a folder in the server host (e.g. /home/lidakra/application.conf) then run a container using an image
already available or a small one like alpine (a small Linux version) mapping the config file in the host with the keys to the config file in the container

    $ docker run -it -v /home/lidakra/application.conf:/home/lidakra/fuhsen-1.1.0/conf/application.conf:ro \
                                         --name fuhsen-conf alpine /bin/sh

From within the volume container check that the config file is present. Detach from the volume container with Ctrl-p Ctrl-q.
Start a container with Fuhsen using the config file in the data volume

    $ docker run -it -p 9000:9000 --volumes-from fuhsen-conf --name fuhsen lidakra/fuhsen:v1.1.0

From within the Fuhsen container check in the /conf folder that the config file is present and up to date and then start Fuhsen

    #./bin/fuhsen 


### Run
Fuhsen can be started using Sbt or the Typesafe activator.

#### Run with Sbt
From the project root folder run the command

    $ sbt start

The service server will listen on port 9000.

#### License

* Copyright (C) 2015-2016 EIS Uni-Bonn
* Licensed under the Apache 2.0 License


