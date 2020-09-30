CICD Pipeline for WSO2 API Manager / Enterprise Integration

Following guidlines will help you to determine the how to setup CICD pipleline for WSO2 APIM and Integration, we call this API platform.
APIs have become the defacto for connecting apps, services and data. Organizations have multiple environments such as 
Dev, Test and Prod for different purposes. Therefore, the APIs and integration goes hand to hand and  need to be available 
in each environment after developers specify the required conditions.WSO2 Enterprise Integrator is an open-source, light-weight, battle-tested, hybrid integration platform which comes with Apache 2.0 license.

Combine effort of automating the deployment process will be hugely reduce the manually promoting APIs and deploying composite artifacts, we have noticed in the past, integrating  artifacts between environments which is a tedious, error-prone, and 
time-consuming task thus all these effort is to streamline the operations much faster.

![CI/CD pipeline for APIs with WSO2 API Manager](images/ci-cd-pipeline-for-apis-with-wso2-apim.png)


## Solution

For this demonstration the following architecture will be used.

![CI/CD pipeline architecture](images/ci-cd-pipeline-demo-architecture.png)

## Prerequisites

1. Deploy the backend server
2. Install the Jenkins server
3. Install WSO2 API Manager
4. Install WSO2 Enterprise Integrator

### 1. Setup hosts for deployment

You need to setup following at the hosts for domain mappings
* <<host>> dev.apim.com  prod.apim.com
* <<host>> dev.be.com  prod.be.com
* <<host>> dev.ei.com  prod.ei.com

### 2. Deploy the backend server

Sample user service is used as the backend server and the complete source code of that server can be found 
[here](backend_server). Note that this is a Spring Boot application and the following commands can be used to start 
or build the application

* Start the application : `mvn spring-boot:run`
* Build the application : `mvn clean install`

Note that the jar is already built and stored [here](backend_server/target/backend-server-1.0.0.jar) and that can be 
simply started by executing `java -jar target/backend-server-1.0.0.jar`

All the available services will be shown in the Swagger UI.

Swagger UI URL: [http://localhost:8595/swagger-ui.html]()

![Swagger UI](images/swagger-ui.png)