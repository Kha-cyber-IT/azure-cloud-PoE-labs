# Day 19: Convert Public Azure Blob Container to Private

Two blob containers named `nautilus-container-18181` and `nautilus-priv-29130` are available in the `East US` region within the storage account `nautilusst10815`. The `nautilus-container-18181` is currently public, and `nautilus-priv-29130` is private.

1) Convert the blob container `nautilus-container-18181` from public to private while leaving `nautilus-priv-29130` unchanged.

2) Make sure the access level for `nautilus-container-18181` is set to `private` with no public access.


1. Go to `Storage center` and locate the storage account `nautilusst10815`.

   <img width="1071" height="311" alt="image" src="https://github.com/user-attachments/assets/96a098c6-b498-4480-926c-685828146f27" />

2. Click on the storage account `nautilusst10815` and select `Storage Browser` from navigation pane.

   <img width="242" height="416" alt="image" src="https://github.com/user-attachments/assets/7d85b0fd-8cb0-404e-a756-053f37ce23b2" />

3. To find the container, Select `Blob container` where you will find the required container mentioned in the task.

   <img width="1073" height="345" alt="image" src="https://github.com/user-attachments/assets/b5af0ca5-542c-4345-a842-c0482b28b40d" />

4. Select container `nautilus-container-18181` and click on `Change access level` and select `Private`.

   <img width="776" height="240" alt="image" src="https://github.com/user-attachments/assets/635f9b13-8ad2-492d-91fe-8a595f7bdcdb" />

5. Verify containers statuses are private.

   <img width="1072" height="344" alt="image" src="https://github.com/user-attachments/assets/52febd1f-3953-4816-88f5-f6bef8ee699c" />
