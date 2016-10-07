Example from "Getting Started with Apache Servicemix" webinar
========================================================

The Camel routes used in this example are explained by the following diagram:

![EIP Diagram](https://raw.github.com/FuseByExample/rider-auto-osgi/master/doc/EIP_Routes_Diagram.png)

To run this example project build the project and deploy to ServiceMix  
according to the steps below. 

Setup
==============================
- Install Apache Maven 3+
    - Download distribution from http://maven.apache.org. 
    - Unzip the downloaded Maven distribution to a location on your hard disk
    that you find suitable.
    - configure this location as the environment variable MAVEN_HOME
    - add MAVEN_HOME/bin to your PATH environment variable

- Install JBoss Fuse  6.3.0
    - Download from https://access.redhat.com/jbossnetwork/ (registration required) and extract

Build & Run
==============================

1) Build this project so bundles are deployed into your local maven repo

    <project home> $ mvn clean install

2) Start JBoss Fuse

    <JBoss Fuse home>  $ bin/fuse

3) Install the activemq-camel feature

    JBossFuse:karaf@root> features:install activemq-camel

4) Add this projects features.xml config to Fuse from the Console
   (makes it easier to install bundles with all required dependencies)

JBossFuse:karaf@root>  features:addUrl mvn:org.fusesource.examples/rider-auto-common/4.0-SNAPSHOT/xml/features

5) Install the project.

    JBossFuse:karaf@root>  features:install rider-auto-osgi

6) To test the file processing, there are existing files in the
   rider-auto-common module.

    '<project home> $' cp rider-auto-common/src/data/message1.xml '<JBoss Fuse home>'/target/placeorder

   To see what happened look at the log file, either from the console

    JBossFuse:karaf@root>  log:display

   or from the command line

    '<JBoss Fuse home>' $ tail -f data/log/fuseesb.log

6) To test the WS, use your favorite WS tool (e.g. SoapUI) against the following
   WSDL hosted by the rider-auto-ws bundle.
   * http://localhost:8182/cxf/order?wsdl

