# Spring-Boot CXF REST service example


This example demonstrates how you can use JBoss Fuse  with Spring Boot
More at: https://access.redhat.com/documentation/en/red-hat-jboss-middleware-for-openshift/3/single/red-hat-jboss-fuse-integration-services-20-for-openshift
Make sure your repositiries are configured as shown in the above link !

Since this was done during FIS2.0 preview; Start Jboss Dev Studio go to Properties --> Maven-->Archtypes
 and add FIS2.0 archtype from https://maven.repository.redhat.com/earlyaccess/all/io/fabric8/archetypes/archetypes-catalog/2.2.180.redhat-000004/archetypes-catalog-2.2.180.redhat-000004-archetype-catalog.xml


Install and start up OpenShift on your local machine
Install FIS image stream definition into OpenShift (raw.githubusercontent.com/jboss-fuse/application-templates/application-templates-2.0.redhat-000026/fis-image-streams.json)


OpenShift:
--> Login into OpenSHift
--> oc project openshift
--> oc create -f fis-image-streams.json

### Building

The example can be built with

    mvn clean install


### Running the example locally

The example can be run locally using the following Maven goal:

    mvn spring-boot:run

Service Root Context in /services/medical - stored in application.properties 
Service UrL- http://localhost:8080/services/medical/claims

Swagger JSON, YAML
http://localhost:8080/services/medical/claims.json ( .yaml)
Swagger UI access.
http://localhost:8080/services/medical/claims/api-docs?/url=services/medical/claims/swagger.json

### Running the example in Kubernetes

It is assumed a running Kubernetes platform is already running. If not you can find details how to [get started](http://fabric8.io/guide/getStarted/index.html).

Assuming your current shell is connected to  OpenShift so that you can type a command like



or for OpenShift

```
oc get pods
```

Then the following command will package your app and run it on Kubernetes:

```
mvn fabric8:run
```
The output log will give the URL to access the endpoint, something like
```
[INFO] F8:[SVC] RestCXFSprinBoot: http://192.168.64.7:32225
```

You will need to append the context-path to access the JAX-RS service so the url is something like

http://192.168.64.7:32225/services/medical/claims

To list all the running pods:

    oc get pods

Then find the name of the pod that runs this quickstart, and output the logs from the running pods with:

    oc logs <name of pod>

You can also use the [fabric8 developer console](http://fabric8.io/guide/console.html) to manage the running pods, and view logs and much more.

To access the endpoint, use the host and port from the output log when run mvn fabric8:run

http://192.168.64.7:32225/services/medical/claim/test/FIS
will display "Hello FIS, Welcome to CXF RS Spring Boot World!!!"


You can find more details about running this [quickstart](http://fabric8.io/guide/quickstarts/running.html) on the website. This also includes instructions how to change the Docker image user and registry.

