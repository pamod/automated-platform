# WSO2 Platform creation Ansible scripts

The following guide will allow a user to rapidly create an APIM/EI setup in the local environment. Please following the instructions below 

## Supported Operating Systems

- Ubuntu 16.04 or higher
- CentOS 7

## Supported Ansible Versions

- Ansible 2.8.0

## Architecture 

![Architecture](/images/quick_walkthrough_arch.png)

## Prerequisites 

- Download and install Ansible (current setup is tested with Ansible 2.8.0). Refer https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html for more information on installation. 
- Download and install MySQL Server (tested with 8.0.16). 
- Make sure JDK is installed in your local environment. 
- Download the following binaries into $automated-platform/files/packs
    - wso2am-3.0.0.zip
    - wso2am-analytics-3.0.0.zip
    - wso2mi-1.1.0.zip

## Installation 

- Locate the DB scripts in $automated-platform/database/platformdbscripts.sql and execute it. 
- Execute the following at $automated-platform `ansible-playbook -i dev site.yml`
- Navigate to ../$automated-platform/setup directory. You’ll observe apim, am-analytics and mi directories created under the setup folder 
Execution
- Navigate to $setup/wso2am-analytics-3.0.0/bin directory and start WSO2 APIM Analytics Worker by executing `sh ./worker.sh`
- Navigate to $setup/wso2am-analytics-3.0.0/bin directory and start WSO2 APIM Analytics Dashboard by executing `sh ./dashboard.sh`
- Navigate to $setup/wso2am-3.0.0/bin directory and start WSO2 API Manager by executing `sh ./wso2server.sh`
- Navigate to $setup/wso2mi-1.1.0/bin directory and start WSO2 Micro Integrator by executing `sh ./micro-integrator.sh`


## Testing

### API Manager 

APIM Management Console - https://localhost:9443/carbon/admin/login.jsp  
APIM Publisher https://localhost:9443/publisher/apis 
APIM Dev Portal https://localhost:9443/devportal/apis
APIM Analytics Dashboard https://localhost:9643/analytics-dashboard/

### Initializing the Sample Services

Navigate to $automated-platform/services directory and execute `ballerina run order_mgt_service.bal` 

### Micro Integrator 

- Navigate to $automated-platform/workspace/OrderMgtCapp/target and copy the Capp `OrderMgtCapp_1.0.0.car` and paste it into $automated-platform/repository/deployment/server/carbonapps directory.
- Restart Micro Integrator if already running 
- Navigate to $automated-platform/client directory and import PlatformDemo.postman_collection.json to RestClient. 

In Postman Client navigate to OrderMgt_ESB_EP/PlaceOrder request and dispatch. You’ll observe a response similar to below 

![place order request](/images/rq_Place_Order_ESB.png)






