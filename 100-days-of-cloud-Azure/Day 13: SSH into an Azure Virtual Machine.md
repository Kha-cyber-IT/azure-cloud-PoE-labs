# Day 13: SSH into an Azure Virtual Machine

The Nautilus DevOps team is working on setting up secure SSH access for their virtual machines in Azure. One of the requirements is to add the SSH public key of the root user from the Azure client host (landing host) to the `nautilus-vm` Azure VM's `authorized_keys` file. This ensures secure and password-less SSH access to the VM.
Task Details:

1) **VM Details**:

- The VM is named `nautilus-vm` and is running in the `West US` region. The default SSH user is `azureuser` — use this user to connect to the VM.
- You need to add the root user's SSH public key from the Azure client host to the `authorized_keys` file of the VM's root user.
- The SSH public key of the root user on the Azure client host is located at `/root/.ssh/id_rsa.pub`.

2) **Public Key Addition**:
- Copy the public key located at `/root/.ssh/id_rsa.pub` on the Azure client host to the `authorized_keys` file of the root user on `nautilus-vm`.
- Ensure that the proper permissions for the `.ssh` folder and `authorized_keys` file are set on the VM.

3) **Verification**:
- After adding the public key, make sure that you are able to SSH into the `nautilus-vm` VM as the root user from the Azure client host without needing a password.

**Important Notes**:
- Ensure that the VM is up and running before attempting to SSH.
- You may need to adjust the firewall or security group rules for the VM to allow SSH access.


## Steps to enable root login

1. View and copy public key from client vm.

   `cd .ssh`
   
   `cat id_rsa.pub`

3. Login to `nautilus-vm` through SSH.

   `ssh azureuser@<nautilus-vm-ip>`
   
   IP can be found on Azure Virtual Machine Dashboard

5. Prompt to `root` user.

   `sudo su`

6. Go to root directory

   `cd ~`

7. Open `authorized_keys` in `.bash/authorized_keys`

   `cd .ssh`
   
   Copy public key here
   
   `vi authorized_keys`

8. Logout and move to client vm.

   `exit`

9. Try login with root to azure vm `nautilus-vm`

   `ssh root@<nautilus-vm-ip>
