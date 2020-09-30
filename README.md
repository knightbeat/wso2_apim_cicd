# CICD Pipeline for WSO2 API Manager / Enterprise Integration

Following guidelines will help you to determine how to setup the CICD pipeline for WSO2 APIM and Integration, we call this API platform.
APIs have become the defacto for connecting apps, services and data. Organizations have multiple environments such as 
Dev, Test and Prod for different purposes. Therefore, the APIs and integration goes hand to hand and  need to be available 
in each environment after developers specify the required conditions.WSO2 Enterprise Integrator is an open-source, light-weight, battle-tested, hybrid integration platform which comes with Apache 2.0 license.

Combine effort of automating the deployment process will be hugely reduce the manually promoting APIs and deploying composite artifacts, we have noticed in the past, integrating  artifacts between environments which is a tedious, error-prone, and 
time-consuming task thus all these effort is to streamline the operations much faster.

![CI/CD pipeline for APIs with WSO2 API Manager](images/ci-cd-pipeline-for-apis-with-wso2-apim.png)


## Solution

For this demonstration the following architecture will be used.

![CI/CD pipeline architecture](images/cicd-pipeline-demo-architecture-ei-apim.png)

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

### 2. Install the Jenkins server

Installing jenkins server is straight forward, you can either deploy it as docker or you can get Web application ARchive (WAR) and there are other options too . Please refer to their official [documentation](https://www.jenkins.io/doc/book/installing/)
for this.

### 3. Install WSO2 API Manager

For installing WSO2 API Manager please refer to this [documentation](https://apim.docs.wso2.com/en/latest/install-and-setup/install/installing-the-product/installing-the-product/)
for more information on that. For this demonstration I'll be having two environments called Dev and Test but any number 
of environments can be there and the steps are pretty much the same.

### 3. Install WSO2 Enterprise Integrator 

For installing WSO2 Enterprise Integrator  please refer to this [documentation](https://docs.wso2.com/display/EI660/Installation+Guide/)
for more information on that. 

## Configurations

This demo consists of two parts, i.e deploying artifacts for APIM and while using the CTL tool functionalists. Sametime, prepare carbon application for integration, deploy them
in the EI. Both having two different approach as of now, let's get into more detail in coming section

##### API Project
* API artifacts deployer will use [here](UserAPI), please refer to the the detail of the API definitions to understand the resources it exposing

* You need to start two APIM nodes dev with port offset 0 i.e dev.apim.com, prod with port offset 1 i.e prod.apim.com

* Execute the below commands to deploy this API on your development server. If your development server is not on the local machine, 
please change the URLs accordingly.

    * Add the dev environment : `apictl add-env -e dev --apim https://dev.apim.com:9443 --token https://dev.apim.com:8243/token`
    * Login to the dev environment : `apictl login dev -u admin -p admin -k`
    * Add the prod environment : `apictl add-env -e prod --apim https://prod.apim.com:9444 --token https://prod.apim.com:8244/token`
    * Login to the dev environment : `apictl login dev -u admin -p admin -k`


