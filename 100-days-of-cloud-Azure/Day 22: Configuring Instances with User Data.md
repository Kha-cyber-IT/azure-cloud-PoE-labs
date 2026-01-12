# Day 22: Configuring Instances with User Data

As a member of the Nautilus DevOps Team, your task is to create a VM with the following specifications:

**Instance Name**: The VM must be named `xfusion-vm`.

**Image**: Use any available Ubuntu image to create this VM.

**Custom Script Extension/User Data**: Configure the VM to run a custom script during its launch. This script should:

- Install the `Nginx` package.
- Start the `Nginx` service.
**
Network Security Group (NSG)**: Ensure that the VM allows HTTP traffic on port 80 from the internet.


## Setup Azure Virtual machine with user script

1. Create VM name `xfusion-vm` in `EAST US` region.

   <img width="752" height="117" alt="image" src="https://github.com/user-attachments/assets/52a20daf-66da-4e20-963f-808f566a1400" />
   
2. Select `Ubuntu` image for the virtual machine.

   <img width="763" height="58" alt="image" src="https://github.com/user-attachments/assets/7bfd4fcd-272a-4f89-a039-ea45de2a835b" />

3. Create `SSH` public key and choose `RSA format`.

   <img width="707" height="342" alt="image" src="https://github.com/user-attachments/assets/e626ecb2-82d5-422f-8c2d-bf7c8a074900" />

3. For `size`, select `Standard_B1s`.

   <img width="683" height="96" alt="image" src="https://github.com/user-attachments/assets/4c6e1936-131b-4400-871e-9d198c925990" />

3. On `Disk` tab, select `Standard HDD`

   <img width="777" height="167" alt="image" src="https://github.com/user-attachments/assets/5d60885f-75c7-46e0-9af2-d22a4d0a7f4f" />

4. Now, go to `Advance` tab and click on `Enable user data` under `User data` section.

   <img width="711" height="259" alt="image" src="https://github.com/user-attachments/assets/5f906262-ada5-454d-9a33-df996546ef59" />

   **Enter the following script for `nginx` installation under `User data`**.
   
   ```bash
   #!/bin/bash
   apt update -y
   apt install -y nginx
   systemctl start nginx
   systemctl enable nginx
   ```
5. Create the VM by clicking `Create` on `Review + create` tab.

6. After creating VM, go to resource and choose `Network settings` from navigation pane.

   <img width="220" height="424" alt="image" src="https://github.com/user-attachments/assets/81d5d71d-9c2d-4e99-a0c9-1d21fa6c395b" />

7. From `Network security group`, click on `Create port rule` and choose `Inbound port rule`.

   <img width="1071" height="462" alt="image" src="https://github.com/user-attachments/assets/cbeff78c-6c7b-41be-922a-36232d6fb1e4" />

8. Add rule for `HTTP` port.

   <img width="506" height="343" alt="image" src="https://github.com/user-attachments/assets/9f1cf713-0d20-4149-809d-582903b3ac4a" />

9. Enter port rule name and description(optional) and click on `Add`.

   <img width="502" height="292" alt="image" src="https://github.com/user-attachments/assets/2135f806-5937-4ea9-86b1-0ec58a408788" />

10. Verify new rule added to the `Inbound port rule` dashboard.

    <img width="1045" height="259" alt="image" src="https://github.com/user-attachments/assets/6879bf7e-9deb-4be6-9848-c02006b0c5bf" />

11. Now copy the VM public IP from `Overview` section and enter it on a browser to see `Nginx` welcome page.

    <img width="601" height="240" alt="image" src="https://github.com/user-attachments/assets/06dbb8f8-867e-43d5-91c2-0d9e0a9b6f4f" />

12. Also, you can ssh into the Azure VM using ssh key you generated and check Nginx status.

    ```bash
    sudo systemctl status nginx
    ```

    <img width="1012" height="296" alt="image" src="https://github.com/user-attachments/assets/070970d3-4e5e-4b37-a8d2-2f2edc9fb7f8" />

    ```bash
    curl http://<xfusion-vm-ip>
    ```
    
    <img width="994" height="432" alt="image" src="https://github.com/user-attachments/assets/c705c70d-76bb-4ac1-8777-57aa8a5feb31" />
