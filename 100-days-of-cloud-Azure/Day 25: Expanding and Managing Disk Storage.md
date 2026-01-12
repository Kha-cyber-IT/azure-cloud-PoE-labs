# Day 25: Expanding and Managing Disk Storage

For this task:

1) Expand the existing VM `devops-vm` disk from `32Gi` to `64Gi`.

2) Also create a new `standard HDD` data disk named `devops-disk` of `64Gi` and mount the disk to VM `devops-vm` at location `/mnt/devops-disk`.


## Task 1: Expand `devops-vm` disk from `32Gi` to `64Gi`

1. First, stop the `devops-vm`.

   <img width="1117" height="231" alt="image" src="https://github.com/user-attachments/assets/34013c6a-8973-4b19-907d-262ab6c3c420" />

3. Select the VM and from nagivation pane, select `Settings > Disk`.

   <img width="233" height="418" alt="image" src="https://github.com/user-attachments/assets/e6c23d23-92b7-473f-9f8f-46b9abdb25e3" />

4. See `Disk` size which is now `32Gi`

   <img width="602" height="150" alt="image" src="https://github.com/user-attachments/assets/670badb7-52cf-44a3-abcd-e97e0ff14a51" />

3. Select the disk, from it's navigation pane, select `Settings > Size + Performance`

   <img width="217" height="377" alt="image" src="https://github.com/user-attachments/assets/7a0fbf11-a5e0-44bf-a67f-23f6ac4dc7c6" />

4. Select new size, and click on `Save`

   <img width="1097" height="491" alt="image" src="https://github.com/user-attachments/assets/aefa254f-2bc2-4153-84ac-f1b1e130cad9" />

5. In the navigation pane, review size changes from `Overview`

   <img width="1105" height="278" alt="image" src="https://github.com/user-attachments/assets/8f683dfe-d8c1-449b-9d2e-461e9140b231" />

6. Start the `devops-vm` and you should still see the attached disk size to `64Gi` now. You might need to click on `Refresh` first.

   <img width="586" height="145" alt="image" src="https://github.com/user-attachments/assets/39ee95ef-80dc-47ac-9bff-3a1e063cf007" />


## Task 2: Create a new `standard HDD` data disk named `devops-disk` of `64Gi` and mount the disk to VM `devops-vm`.

1. Navigate to your Virtual Machine `devops-vm` in the portal. In the navigation pane, from `Settings > Disk > Create and attach disk` and enter disk information.

   <img width="605" height="199" alt="image" src="https://github.com/user-attachments/assets/66831036-1d53-46e3-9d21-cc06cda207a7" />

2. Review the disk after creation in `Data disk`

   <img width="599" height="188" alt="image" src="https://github.com/user-attachments/assets/0b3340cc-3e79-4780-a194-a49e562cd6f4" />

3. Prepare and Mount the Disk (Linux CLI)

   Connect to your VM via SSH and run these commands.

   ```bash
   lsblk
   ```
   <img width="821" height="230" alt="image" src="https://github.com/user-attachments/assets/454cfd78-e345-4a69-8cd7-43448ad1fe7a" />

   **Create a Filesystem**

   ```bash
   sudo mkfs -t ext4 /dev/sdc
   ```
   ` Since this is a brand new disk, it has no filesystem. We will format it as ext4.`

   <img width="969" height="249" alt="image" src="https://github.com/user-attachments/assets/2676e1fe-84dd-4bdc-bce0-ff831fb10f14" />

   **Create the Mount Point**

   ```bash
   sudo mkdir -p /mnt/devops-disk
   ```
   `Create the folder where you want to access the disk.`

   **Mount the Disk**

   ```bash
   sudo mount /dev/sdc /mnt/devops-disk
   ```
   `This connects the physical disk sdc to the folder you just created.`

   **Make it Permanent (Persistent Mount)**

   ```bash
   sudo blkid /dev/sdc
   ```
   `Get the UUID: Look for the part that says UUID="abcd-1234..." and copy that long string.`

   <img width="1051" height="41" alt="image" src="https://github.com/user-attachments/assets/4c6ce0ef-9df2-43ba-ba2f-c639626e4c45" />

   **Edit the `fstab` file**

   ```bash
   sudo nano /etc/fstab
   ```

   **Add this line at the end of the file (replace YOUR-UUID-HERE with the actual ID you copied):**

   ```bash
   UUID=YOUR-UUID-HERE   /mnt/devops-disk   ext4   defaults,nofail   1   2
   ```
   Example: `UUID="147e66f5-b37b-4d3a-9e2e-72999e6f109c"   /mnt/devops-disk   ext4   defaults,nofail   1   2`

   <img width="1361" height="143" alt="image" src="https://github.com/user-attachments/assets/31e671dc-60ac-49a1-b57f-7122ef351b74" />

   **Verify the Mount**

   ```bash
   df -h /mnt/devops-disk
   ```
   <img width="1039" height="58" alt="image" src="https://github.com/user-attachments/assets/e8657308-724d-4e34-94cf-1cf6a8eb9f0b" />

   **Currently, that folder is owned by root. If you want your azureuser to be able to write files to it without using sudo, run this:**

   ```bash
   sudo chown azureuser:azureuser /mnt/devops-disk
   ```

   **To see the changes:**

   ```bash
   lsblk
   ```
   <img width="968" height="214" alt="image" src="https://github.com/user-attachments/assets/d68ec003-1912-43ad-9257-afa92f146b73" />

   **Check the Usable Space:**
   
   ```bash
   df -h
   ```
   <img width="999" height="201" alt="image" src="https://github.com/user-attachments/assets/2bbf1532-5079-4bb8-8de5-a58a92022b03" />

> [!IMPORTANT]  
> Understand the concept behind this task

## We followed a "Prepare, Place, Plug" workflow:

1. **Prepare (mkfs)**: We "formatted" the disk. This creates a "grid" on the disk so the OS knows how to store data. We used the `ext4` format, which is the standard for Linux.

2. **Place (mkdir)**: We created an empty folder at `/mnt/devops-disk`. This is the "doorway" to your disk.

3. **Plug (mount)**: We told Linux: "Take the hardware at `/dev/sdc` and connect it to the folder `/mnt/devops-disk`."

## Why mount it in /mnt/?

You can technically mount a disk anywhere, but Linux has a standard called the **Filesystem Hierarchy Standard (FHS)**:

- `/mnt/`: This is the traditional place for "temporarily mounted filesystems."

- **Why there?** It keeps the root directory (`/`) clean. If you just saved everything to `/`, your OS disk (the 32/64GB one) would get full. By mounting to `/mnt/devops-disk`, you ensure that data goes to the new 64GB HDD instead of the OS disk.
