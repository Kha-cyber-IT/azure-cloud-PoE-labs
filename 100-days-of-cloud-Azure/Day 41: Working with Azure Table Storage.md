# Day 41: Working with Azure Table Storage

The Nautilus DevOps team is developing a simple 'To-Do' application using Azure Table Storage to store and manage tasks efficiently. The team needs to create an Azure Table to hold tasks, each identified by a unique taskId. Each task will have a description and a status, which indicates the progress of the task (e.g., 'completed' or 'in-progress').

Your task is to:

- Create an Azure Storage Account named `xfusiontablest11268` with a Table Storage table called `tasks`.
- Insert the following tasks into the table:
  - **Task 1**: PartitionKey: 'tasks', **RowKey**: '1', **description**: 'Learn Table Storage', **status**: 'completed'
  - **Task 2**: PartitionKey: 'tasks', **RowKey**: '2', **description**: 'Build To-Do App', **status**: 'in-progress'
- Verify that **Task 1** has a status of `completed` and **Task 2** has a status of `in-progress`.

> [!Note] 
> **Use the Azure CLI to insert these tasks into the table.**


## Task 1: Create an Azure Storage account

1. **Go to `Storage center` and select `Blob storage` from it's menu.**

   <img width="1365" height="507" alt="image" src="https://github.com/user-attachments/assets/03be5a9e-96d0-465c-b511-a585d7da26bb" />

2. **Click on `Create` and enter account name with `LRS` redundency setting.**

   <img width="1348" height="357" alt="image" src="https://github.com/user-attachments/assets/1b5633ed-20f3-4260-9e29-ec81c9ccdc99" />

3. **Next go to `Review + create` and click `Create`**


## Task 2: Create Table Storage

1. **From storage account menu, select `Tables`.**

   <img width="1085" height="404" alt="image" src="https://github.com/user-attachments/assets/bc142450-2782-4b92-86fd-2c3bdfe95e4e" />

2. **CLick on `+ Add table` and enter name `task`.**

   <img width="1128" height="281" alt="image" src="https://github.com/user-attachments/assets/4b421cf8-d73c-4377-89a5-9d0871083691" />

## Task 3: Insert tasks to the table with CLI

1. **Login to access Azure**

   ```sh
   az login
   ```

2. **Get Storage Account Key from CLI**

   ```sh
   az storage account keys list \
    --account-name xfusiontablest11268 \
    --query '[0].value' \
    -o tsv
   ```

3. **Insert Task 1**

   ```sh
   az storage entity insert \
    --account-name xfusiontablest11268 \
    --account-key <ACCESS-KEY> \
    --table-name tasks \
    --entity PartitionKey=tasks RowKey=1 description="Learn Table Storage" status=completed
   ```

4. **Insert Task 2**

   ```sh
   az storage entity insert \
    --account-name xfusiontablest11268 \
    --account-key <ACCESS-KEY> \
    --table-name tasks \
    --entity PartitionKey=tasks RowKey=2 description="Build To-Do App" status=in-progress
   ```

5. **Verify Tasks with Azure CLI**

   ```sh
   az storage entity query \
    --account-name xfusiontablest11268 \
    --account-key <ACCESS-KEY> \
    --table-name tasks \
    --output table
   ```

   **Expected:**

   ```
   PartitionKey    RowKey    Description          Status
   --------------  --------  -------------------  -----------
   tasks           1         Learn Table Storage  completed
   tasks           2         Build To-Do App      in-progress
   ```
   
