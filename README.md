# Kestra Flow for Multi-cloud Deployment:
This repository contains the Kestra flow for multi-cloud deployment, including local, Google Cloud Platform (GCP), and Microsoft Azure environments.

This flow uses GitHub public repository, Docker Hub, ngrok, GCP Cloud Run Service, and Azure Container App.

You will get success for local and Azure deployment, but a warning for GCP deployment. GCP deployment is working fine, but it reported a warning as you require to authenticate yourself with an authentication identity token to access your application.

> [!WARNING]
> Make sure to clean up your resources after verifying your application in a specific environment.

## Kestra Secrets:
You require to define the Kestra secrets as mentioned in the prerequisites. It must be encoded Base64 as mentioned in the Kestra documentation.

> [!TIP]
> Choose Line Feed (LF) as End Of Line (EOL) characters in the `.env` file before encoding Kestra secrets. Your secret value must be on a single line.

## Prerequisites:
1. Local deployment:
   1. Your Docker Hub account and a valid Personal Access Token (PAT).
      1. DOCKER_HUB_USERNAME - Secret for your Docker Hub username
      2. DOCKER_HUB_PAT - Secret for your Docker Hub PAT
   3. Your ngrok account, a valid auth token, and a valid static domain.
      1. NGROK_AUTH_TOKEN - Secret for the ngrok auth token
      2. NGROK_STATIC_DOMAIN - Secret for the ngrok static domain
2. GCP deployment:
   1. Your GCP account, a valid project ID, and a valid service account key JSON.
      1. GCP_PROJECT_ID - Secret for GCP project ID
      2. GCP_SERVICE_ACCOUNT - Secret for GCP service account key JSON
   3. Enable the artifact remote repository API.
   4. Define the GCP valid region in the Kestra secret.
      1. GCP_REGION - Secret for GCP region (ex., `asia-south1`)
3. Microsoft Azure deployment:
   1. Your Microsoft Azure account.
   2. Create a resource group.
      1. AZURE_RESOURCE_GROUP - Secret for your valid resource group
   4. Register a resource provider for a container instance.
   5. Create a service principal with the role `contributor` and a resource group's resource ID as a scope. You will get the followed values in a response.
      1. AZURE_APP_ID - Secret for Azure application ID
      2. AZURE_SERVICE_PRINCIPAL_PASSWORD - Secret for the password of a service principal
      3. AZURE_TENANT_ID - Secret for tenant ID
   6. Define the Azure valid location in the Kestra secret.
      1. AZURE_LOCATION - Secret for Azure location (ex., `centralindia`)

## References:
1. Kestra:
   1. https://kestra.io
   2. https://kestra.io/docs/installation/docker-compose
   3. https://kestra.io/plugins
   4. https://kestra.io/blueprints
   5. https://kestra.io/docs/concepts/secret
   6. This flow is implemented using the following plugins and tasks:
      1. https://kestra.io/plugins/core/flow/io.kestra.plugin.core.flow.workingdirectory
      2. https://kestra.io/plugins/plugin-git/io.kestra.plugin.git.clone
      3. https://kestra.io/plugins/plugin-docker/io.kestra.plugin.docker.build
      4. https://kestra.io/plugins/core/flow/io.kestra.plugin.core.flow.switch
      5. https://kestra.io/plugins/plugin-docker/io.kestra.plugin.docker.run
      6. https://kestra.io/plugins/tasks/io.kestra.plugin.scripts.shell.commands
      7. https://kestra.io/plugins/core/docker/io.kestra.plugin.scripts.runner.docker.docker
      8. https://kestra.io/plugins/plugin-gcp/cli/io.kestra.plugin.gcp.cli.gcloudcli
      9. https://kestra.io/plugins/plugin-azure/cli/io.kestra.plugin.azure.cli.azcli
2. Docker:
   1. https://hub.docker.com/
   2. https://docs.docker.com/security/for-developers/access-tokens/
3. GitHub:
   1. https://github.com/
   2. https://github.com/AlapMistry/spring-boot-demo
4. ngrok:
   1. https://ngrok.com/
   2. https://ngrok.com/docs/
   3. https://ngrok.com/blog-post/free-static-domains-ngrok-users
5. GCP:
   1. https://cloud.google.com/free?hl=en
   2. https://console.cloud.google.com/
   3. https://cloud.google.com/sdk/gcloud
   4. https://cloud.google.com/sdk/docs/cheatsheet
   5. https://cloud.google.com/run/docs/overview/what-is-cloud-run
   6. https://cloud.google.com/artifact-registry/docs/enable-service
6. Azure:
   1. https://azure.microsoft.com/en-in/pricing/free-services/
   2. https://portal.azure.com/
   3. https://learn.microsoft.com/en-us/azure/container-apps/
   4. https://learn.microsoft.com/en-us/azure/container-instances/container-instances-quickstart
   5. https://learn.microsoft.com/en-us/cli/azure/?view=azure-cli-latest
   6. https://learn.microsoft.com/en-us/cli/azure/authenticate-azure-cli?view=azure-cli-latest
   7. https://learn.microsoft.com/en-us/cli/azure/authenticate-azure-cli-service-principal?view=azure-cli-latest
   8. https://learn.microsoft.com/en-us/cli/azure/azure-cli-sp-tutorial-1?view=azure-cli-latest&tabs=bash
   9. https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles
   10. https://learn.microsoft.com/en-us/cli/azure/container?view=azure-cli-latest

## Scope of Improvements:
1. Create subflows for different deployments
2. Get authentication tokens from the respective cloud, if possible
3. Support other cloud providers like AWS, Civo, etc.
4. Get the application deployment URL from logs, if possible
