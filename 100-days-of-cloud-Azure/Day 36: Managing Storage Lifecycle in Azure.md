# Day 36: Managing Storage Lifecycle in Azure

The Nautilus DevOps team needs to optimize data retention costs by automating the deletion of old blobs. They plan to implement Blob Lifecycle Management for a specific container in Azure Storage.

1) **Create a Storage Account:**

   - Name the storage account `datacenterstor28832`.
   - Set the region to `East US`.
   - Use `Locally-redundant storage (LRS)` as the redundancy option.

2) **Create a Blob Container:**

   - Name the container `datacenter-container28832`.

3) **Upload a File to the Container:**

   - Upload the file named `tempfile.txt` to the container. The file is present under `/root` of the client host.

4) **Configure Blob Lifecycle Management:**

   - Apply a Lifecycle Management rule named `datacenter-del-rule` to the container `datacenter-container28832` to delete blobs after `7` days of last modification.

5) **Validation:**

   - Verify that the Lifecycle Management rule named `datacenter-del-rule` is correctly applied.


## Task 1: Create storage account

1. Go to `Storage account` dashboard and click `Create`.

   <img width="1101" height="439" alt="image" src="https://github.com/user-attachments/assets/a1abfa07-fd10-41e6-bf4a-2a0cbb6177a8" />

2. Enter resource name and choose region `East US`.

   <img width="1345" height="335" alt="image" src="https://github.com/user-attachments/assets/19a77fb2-99b1-4c0a-a1b8-b34567f0b695" />

3. Use Locally-redundant storage (LRS) as the redundancy option.

   <img width="1348" height="170" alt="image" src="https://github.com/user-attachments/assets/c4ef522e-d51d-4e9e-9d95-ab1e96e6fc31" />

4. Go to `Review + create` tab anc click `Create`.

   <img width="310" height="52" alt="image" src="https://github.com/user-attachments/assets/aafddf25-6636-41a1-b84e-e76a8723b401" />


## Task 2: Create a Blob Container

1. Go to `Storage center` dashboard and click on the storage account you just created.

   <img width="1351" height="480" alt="image" src="https://github.com/user-attachments/assets/7011bcd5-599a-4fcf-b433-93eac559a8da" />

2. From storage account dashboard navigation pane, select `Storage browser`.

   <img width="1321" height="518" alt="image" src="https://github.com/user-attachments/assets/30c6b7b7-bb18-479f-9bfe-3d269f37f4eb" />

3. Select `Blob container` and click on `+ Add container`.

   <img width="1101" height="331" alt="image" src="https://github.com/user-attachments/assets/30fb44c5-6898-4b14-b5a4-0c2f0c69f1f0" />

4. Enter container name and click `Create`.

   <img width="435" height="574" alt="image" src="https://github.com/user-attachments/assets/a1580dde-f7c7-45b1-9dda-b4baa5367806" />


>[!Important]
> Find file upload using Azure portal at the end of the **Task 3**

## Task 3: Upload File to the Container using CLI

1. Login to Azure from azure-client

   ```sh
   az login
   ```

>[!Note]
> If prompted, open the URL and enter the code to authenticate.

2. Set required variables

   ```sh
   STORAGE_ACCOUNT="datacenterstor28832"
   CONTAINER_NAME="datacenter-container28832"
   FILE_PATH="/root/tempfile.txt"
   BLOB_NAME="tempfile.txt"
   ```

3. Get the Storage Account Key

   ```sh
   az storage account keys list \
    --account-name $STORAGE_ACCOUNT \
    --query "[0].value" \
    --output tsv
   ```

   Expected output:export AZURE_STORAGE_KEY="[REDACTED_FOR_SECURITY]"

   
   
   **Copy the key and export it:**

   ```sh
   export AZURE_STORAGE_KEY= export AZURE_STORAGE_KEY="[REDACTED_FOR_SECURITY]"
   ```
   
5. Upload the file using Azure CLI

   ```sh
   az storage blob upload \
    --account-name $STORAGE_ACCOUNT \
    --container-name $CONTAINER_NAME \
    --name $BLOB_NAME \
    --file $FILE_PATH \
    --auth-mode key
   ```

6. Verify the upload using CLI

   ```sh
   az storage blob list \
    --account-name $STORAGE_ACCOUNT \
    --container-name $CONTAINER_NAME \
    --output table \
    --auth-mode key
   ```
   
**Expected output:**

```
Name          Blob Type    Blob Tier    Length    Content Type    Last Modified              Snapshot
------------  -----------  -----------  --------  --------------  -------------------------  ----------
tempfile.txt  BlockBlob    Hot          25        text/plain      2026-01-04T13:17:33+00:00
```

## (Optional) Upload File to the Container using Azure portal

>[!Note]
> Create the `tempfile.txt` file on your pc with  same content.

1. On the blob container dashboard, click on `Upload`.

   <img width="1046" height="210" alt="image" src="https://github.com/user-attachments/assets/dc5459ed-9d24-4931-9cde-0e70f2a399c1" />

2. Verify the upload using Azure portal

   <img width="1040" height="353" alt="image" src="https://github.com/user-attachments/assets/98e4ac04-a36e-4fe4-9481-34aa91f463fa" />


## Task 4: Configure Blob Lifecycle Management

1. Go back to the storage account `datacenterstor28832`, From the navigation pane, click `Lifecycle management`

   <img width="248" height="383" alt="image" src="https://github.com/user-attachments/assets/4aa59c87-5b72-462b-aace-3320e1ca2bbc" />

2. Click `+ Add a rule`, enter rule name and choose `Run scope` for `Limit blobs with filter` and click `Next`.

   <img width="652" height="560" alt="image" src="https://github.com/user-attachments/assets/7341d12f-ea6a-4381-a258-af2c0faa17c6" />

3. On the `Base blob` tab, set lifecycle rule and click `Next`.

   <img width="755" height="477" alt="image" src="https://github.com/user-attachments/assets/20ac9708-ede9-48ea-a761-afcf4c849bbd" />

4. Under `Blob prefix` enter container name as `datacenter-container28832/` and click `Add`.

   <img width="1310" height="380" alt="image" src="https://github.com/user-attachments/assets/e4e8aff6-07d7-4efa-9c51-fa9f457d5a6d" />

