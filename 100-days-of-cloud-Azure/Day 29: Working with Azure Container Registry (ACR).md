# Day 29: Working with Azure Container Registry (ACR)

The Nautilus DevOps team has been tasked with setting up a containerized application. They need to create a Azure Container Registry (ACR) to store their Docker images. Once the repository is created, they will build a Docker image from a Dockerfile located on the `azure-client` host and push this image to the ACR repository. This process is essential for maintaining and deploying containerized applications in a streamlined manner.

1) Create a ACR repository named `xfusionacr19709` under East US.

2) Pricing plan must be `Basic`.

3) `Dockerfile` already exists under `/root/pyapp` directory on `azure-client` host.

4) Build a Docker image using this `Dockerfile` and push the same to the newly created ACR repo. The image tag must be latest i.e `xfusionacr19709:latest`.

## Create Azure Container Registry using `Azure CLI`

1. Check existing Resource Groups

   ```sh
   az group list --output table
   ```
   ```
   Name                          Location    Status
   ----------------------------  ----------  ---------
   kml_rg_main-00388d3fca46483c  westus      Succeeded
   ```
   
3. Create Azure Container Registry (ACR)
   
   ```sh
   az acr create \
    --name xfusionacr19709 \
    --resource-group <RESOURCE_GROUP_NAME> \
    --location eastus \
    --sku Basic
   ```

## Create Azure Container Registry using `Azure Portal`

1. Go to Azure portal and Select `Container registries` and click `Create`.

   <img width="1311" height="523" alt="image" src="https://github.com/user-attachments/assets/7c0ce332-3fc9-43d9-8dbe-70b0d2170aa0" />

3. Enter name `xfusionacr19709` under `East US`.

   <img width="1249" height="378" alt="image" src="https://github.com/user-attachments/assets/ed891164-6dba-4e29-8543-5c155061378c" />

3. Select `Pricing plan` as `Basic`.

   <img width="1183" height="197" alt="image" src="https://github.com/user-attachments/assets/56bc35a1-7b3f-4db3-a259-e34fb39ef44d" />

4. On the `Review + create` tab, click `Create`.

   <img width="701" height="550" alt="image" src="https://github.com/user-attachments/assets/4468031b-a78a-406b-be45-83f4d4e84eef" />


## Build image from Dockerfile

1. Go to the container directory

   ```sh
   cd pyapp
   ```

2. Build Docker image (tagged for ACR)

   ```sh
   docker build -t xfusionacr19709.azurecr.io/xfusionacr19709:latest .
   ```

## Push  image to your Azure container registry using the Docker CLI

1. Login to Azure Container Registry

   ```sh
   az acr login --name xfusionacr19709
   ```

2. Push image to ACR

   ```sh
   docker push xfusionacr19709.azurecr.io/xfusionacr19709:latest
   ```

3. Verification

   ```sh
   az acr repository list --name xfusionacr19709
   ```
