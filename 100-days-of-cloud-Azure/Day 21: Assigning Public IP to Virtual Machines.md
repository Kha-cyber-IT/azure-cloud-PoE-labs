The Nautilus DevOps Team has received a new request from the Development Team to set up a new Azure Virtual Machine (VM). This VM will be used to host a new application that requires a stable public IP address. To ensure that the VM has a consistent public IP, a Static Public IP address needs to be associated with it. The VM will be named `datacenter-vm`, and the Static Public IP will be named `datacenter-pip`. This setup will help the Development Team to have a reliable and consistent access point for their application.

- Create an Azure VM named `datacenter-vm` using any available Ubuntu image, with the VM size `Standard_B1s`.
- Generate an SSH public key on the `azure-client` host and associate it with the VM for SSH access.
- Associate a Static Public IP address named `datacenter-pip` with this VM.
- Ensure the VM is accessible via SSH using the generated public key.

### To create a virtual machine

- Go to Virtual machine dashboard, and create a virtual machine name `datacenter-vm`.

  <img width="914" height="371" alt="image" src="https://github.com/user-attachments/assets/28958f7f-e078-41d5-acaa-6f30470f73f7" />

- Next, in the `Disk` tab, choose `Standard HDD` for storage.

  <img width="916" height="310" alt="image" src="https://github.com/user-attachments/assets/1a83e3db-aa81-4118-b965-9850a9c3b60b" />

### To SSH into the Azure VM

- Now create public ssh key on azure client.

  ```bash
  ssh-keygen -t rsa
  ```

- Copy azure client public key `id_rsa.pub` to `datacenter-vm`'s `authorized_keys`.
- Check ssh connection from azure client to `datacenter-vm`.

  `ssh azureuser@<datacenter-vm-ip>`

### [Associate Public IP to Azure Virtual Machine](https://github.com/mirakib/100-days-of-cloud-Azure/blob/main/Day%2010%3A%20Attach%20Public%20IP%20to%20Azure%20Virtual%20Machine.md#day-10-attach-public-ip-to-azure-virtual-machine)

- Go to `Public IP Address` and create a public ip `datacenter-pip`.

  <img width="582" height="541" alt="image" src="https://github.com/user-attachments/assets/0d340291-07f9-4275-a6d2-33078636ed1b" />

- Go to `datacenter-vm`, Under `Settings` in the left pane, select `Networking`, and then select the network interface you want to add the public IP address to. From the Network interface window, under `Settings`, select `IP configurations`, `Enable IP forwarding` and then select an `IP configuration` from the list. In the `Edit IP configuration` window, select `Associate public IP address`, then select `Public IP address` to choose `datacenter-pip` from the drop-down list.
  
  <img width="1366" height="559" alt="image" src="https://github.com/user-attachments/assets/e52edca8-d925-4401-9a73-dde82453458f" />

- Now try to ssh from azure client to `datacenter-vm` using the new ip address.
