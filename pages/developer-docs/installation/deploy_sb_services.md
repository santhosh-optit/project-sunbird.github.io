---
type: landing
directory: developer-docs/installation/
title: Deploying Sunbird Services
page_title: Deploying Sunbird Services
description: Deploy Sunbird services
allowSearch: true
---

The Sunbird application consists of multiple services, each service serves a specific purpose. All services except keycloak are set up using Docker. The following steops will install docker, pull the required images and create services based on those images.

## Preparation to Setup Application

- SSH into the application server. If you have used automated scripts as described in the previous steps, then this server would be vm-1
- Clone the sunbird-devops repo using git clone https://github.com/project-sunbird/sunbird-devops.git
- Copy over the generated configuration directory from the DB server(`<implementation-name>-devops`) to your machine
- Modify all the configurations under # APPLICATION CONFIGURATION block.
- The automated setup also creates a proxy server and like all proxy servers, it requires a SSL certificate. Ensure you have a certificate and key for the domain that you wish to use.
- Run `cd sunbird-devops/deploy && sudo ./install-deps.sh` to install the dependencies.

## API Manager services
Run `sudo ./deploy-apis.sh <implementation-name>-devops/ansible/inventories/<environment-name>`. This will set up the API Manager services.

**Note:** The following steps are necessary only when the application is being deployed for the first time and should be skipped for subsequent deploys.

- deploy-apis.sh script will print a JWT token that needs to be updated in the application configuration. To find the token search the script output to look for "JWT token for player is :", copy the corresponding token. Example output below, token is highlighted in italics:

      changed: [localhost] => {"changed": true, "cmd": "python /tmp/kong-api-scripts/kong_consumers.py /tmp/kong_consumers.json .......       "JWT token for player is :                            
      eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJlMzU3YWZlOTRmMjA0YjQxODZjNzNmYzQyMTZmZDExZSJ9.L1nIxwur1a6xVmoJZT7Yc0Ywzlo4v-    
      pBVmrdWhJaZro", "Updating rate_limit for consumer player for API cr......"]}

Update sunbird_api_auth_token in your configuration with the above copied token.

- Update sunbird_ekstep_api_key in your configuration with the API token obtained from ekstep portal. The steps are [described here](developer-docs/installation/medium_scale_deploy#api-keys)


## Core services

To deploy the Sunbird core services, execute the following command:

Run `sudo ./deploy-core.sh <implementation-name>-devops/ansible/inventories/<environment-name>`. 


## Proxy services

To deploy  the Sunbird proxy services , execute the following command:

Run `sudo ./deploy-proxy.sh <implementation-name>-devops/ansible/inventories/<environment-name>`.

**Note:** The automation walk-through provided (PART 5) (PART6) & (PART7), shows you the process for  deployment for Sunbird services.

### Automation Walkthrough

[Part 5](https://sunbirdpublic.blob.core.windows.net/installation/demo/demo-5.gif){:target="_blank"}

[Part 6](https://sunbirdpublic.blob.core.windows.net/installation/demo/demo-6.gif){:target="_blank"}

[Part 7](https://sunbirdpublic.blob.core.windows.net/installation/demo/demo-8.gif){:target="_blank"}
