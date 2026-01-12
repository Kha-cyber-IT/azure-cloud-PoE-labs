# Day 14: Create and Attach Managed Disks in Azure

For this task:
- Create a managed disk with the following requirements:
- Name of the disk should be `datacenter-disk`.
- Disk type must be `Standard_LRS`.
- Disk size must be `2 GiB`.

## To create a managed disk

1. In the `Azure Portal`, go to `Azure Disks` in `Storage center` and click `Create`

   <img width="1327" height="507" alt="image" src="https://github.com/user-attachments/assets/45472b4d-aa16-423c-b937-de7da36f2a90" />

2. Under the `Basic` tab, select `Resource group`, `Disk name`, `Region` and `Size`

   <img width="622" height="487" alt="image" src="https://github.com/user-attachments/assets/688175ed-62d8-428a-af6b-e1d0b3019b63" />

3. To select custom size i.e `2 GiB` and `Standard LRS`, click on `change size` and select `Standard HDD` for `Storage type`

   <img width="540" height="183" alt="image" src="https://github.com/user-attachments/assets/b1da5daf-0114-4715-8514-f3756c0b467a" />

4. For size, at the bottom of the page, enter `2` at `Custom disk size` and hit `ok`.

   <img width="550" height="188" alt="image" src="https://github.com/user-attachments/assets/4a328da7-ebed-4304-8e9d-41c3437cf817" />

5. Under `Review + create` tab, click `Create`

   <img width="1208" height="540" alt="image" src="https://github.com/user-attachments/assets/9e46f775-d7b9-403e-a61e-804559b1c0ee" />

6. Confirm successful deployment of the disk.

   <img width="796" height="304" alt="image" src="https://github.com/user-attachments/assets/b0ff14ba-0bd7-4d8f-bad0-16996bc01720" />
