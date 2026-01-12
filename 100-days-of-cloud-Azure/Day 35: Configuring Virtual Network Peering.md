# Day 35: Configuring Virtual Network Peering

The Nautilus DevOps team has been tasked with demonstrating the use of VNet Peering to enable communication between two VNets. One VNet will be a private VNet that contains a private Azure VM, while the other will be a public VNet containing a publicly accessible Azure VM.

1) **Existing Azure Resources**:

    - **Public VM**: `nautilus-pub-vm` is already in the public VNet.
    - **Private VNet and VM**: `nautilus-priv-vnet` and `nautilus-priv-vm` exist in the private VNet with its subnet: `nautilus-priv-subnet`.

2) **Create VNet Peering**:

   - Create a VNet Peering between the Public VNet and Private VNet.
   - **VNet Peering Name**: `nautilus-pub-to-priv-peering`.

3) **Test the Connection**:

    - SSH into the public VM and verify that you can ping the private VM.

## Task 1: Review all the resource (Optional)

1. **Virtual networks:**

   <img width="1085" height="127" alt="image" src="https://github.com/user-attachments/assets/73c9f1d0-ffe4-454b-85fc-2719ef8ed6fd" />

2. **Virtual machines:**

   <img width="1083" height="125" alt="image" src="https://github.com/user-attachments/assets/5240e72e-9010-491c-abf8-b7aaaa7e725b" />

3. `nautilus-priv-vnet/nautilus-priv-subnet/nautilus-priv-vm` Overview.

   <img width="1083" height="233" alt="image" src="https://github.com/user-attachments/assets/1577ff20-7bac-4664-9796-4c41515a3b42" />

5. `nautilus-pub-vnet/nautilus-pub-subnet/nautilus-pub-vm` Overview.

   <img width="1083" height="252" alt="image" src="https://github.com/user-attachments/assets/3aaee878-4799-49ed-a5b1-59363bc00409" />


## Task 2: Create VNet Peering

1. Go to `Virtual network` dashboard and click one of the vnet and select `Settings` > `Peering` from navigation pane.

   <img width="248" height="32" alt="image" src="https://github.com/user-attachments/assets/182f3d6d-9555-4f3d-a330-f43ab889ab56" />

2. Select `+ Add`.

   <img width="1086" height="273" alt="image" src="https://github.com/user-attachments/assets/6e857cad-99e5-493d-8e56-6a8db9652b04" />

3. Enter peering link name and select the other vnet.

   <img width="1027" height="354" alt="image" src="https://github.com/user-attachments/assets/0ed1a639-fd94-4918-ba01-a4251816e7e3" />

4. Remote virtual network peering settings.

   <img width="933" height="339" alt="image" src="https://github.com/user-attachments/assets/6b6bfabf-3db1-4f0b-956e-0687d0109b99" />

5. Local virtual network summary.

   <img width="932" height="380" alt="image" src="https://github.com/user-attachments/assets/99dcaa74-558e-4bbb-9940-fe0ddb723dbb" />
   
6. Select `Add`.

   <img width="236" height="62" alt="image" src="https://github.com/user-attachments/assets/e18fdebb-c5a7-4df6-bbf2-17628c207e8b" />


## Task 3: Test the Connection

1. **SSH into the public VM from** `azure-client` **host**.

   ```sh
   ssh azureuser@<nautilus-pub-vm-pub-ip>
   ```

2. **Ping the private VM** `nautilus-priv-vm` **using its private IP**.

   ```sh
   ping <nautilus-priv-vm-priv-ip>
   ```

   <img width="1236" height="227" alt="image" src="https://github.com/user-attachments/assets/3e4f204b-cc2f-4677-87de-a919b103c8ac" />
