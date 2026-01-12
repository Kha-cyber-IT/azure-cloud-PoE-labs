# Day 33: Integrating Virtual Machines with Application Load Balancer

The Nautilus DevOps team is currently working on setting up a simple application on the Azure cloud. They aim to establish an Azure Load Balancer in front of a Virtual Machine (VM) where an Nginx server is currently running. While the Nginx server currently serves a sample page, the team plans to deploy the actual application later.

- Set up an **Azure Load Balancer** named `datacenter-lb`.
- Configure the Load Balancer’s frontend IP configuration with the name `datacenter-lb-ip` and assign a public IP address with the same name (`datacenter-lb-ip`).
- Create a backend pool named `datacenter-backend-pool` and add the VM running `Nginx` to this pool.
- Create a health probe named `datacenter-health-probe` on port `80` to check the VM's health.
- Set up a load balancer rule named `datacenter-lb-rule` to route traffic on port `80` to the backend pool on port `80`.
- Add an inbound rule to the existing NSG of the VM to allow `HTTP` traffic on port `80`.

## Task 1: Create Load balancer

1. Go to `Load Balancer` dashboard and click `+ Create` to choose `Standard Load Balancer`.
   
3. Under `Basic` tab, enter name and choose region `EAST US`.

   <img width="1125" height="438" alt="image" src="https://github.com/user-attachments/assets/ccf02153-a296-4dcc-b152-cdbe282b557b" />

4. Next on the `Frontend IP configuration` tab, click on `Add a frontend IP configuration`.

   <img width="523" height="577" alt="image" src="https://github.com/user-attachments/assets/ddfdf3bd-d87e-4d35-ad0b-d26ea8c18fdf" />

   **To add Public IP Address: click on `Create new` and enter same name as configuration.**

5. Next on the `Backend pool` tab, enter name of the pool add the VM running `Nginx` to this pool.

   <img width="1365" height="554" alt="image" src="https://github.com/user-attachments/assets/dc9d5fc4-d282-4f8c-a169-f76234c89d4d" />

6. Set up a load balancer rule named nautilus-lb-rule to route traffic on port 80 to the backend pool on port 80.

   <img width="504" height="416" alt="image" src="https://github.com/user-attachments/assets/db1ae8bc-204e-4c96-be2e-78cf8b604e49" />

7. On the same `Add load balancing rule` tab, create a health probe by clicking `Create new`.

   <img width="523" height="252" alt="image" src="https://github.com/user-attachments/assets/732cb856-3f50-465e-a55e-035f57af6a1e" />

8. Review rules added to `Inbound rules section` as follows:

   <img width="1344" height="485" alt="image" src="https://github.com/user-attachments/assets/248132c7-7f27-4746-94d3-e5b01f750c59" />

9. Now proceed to `Review + create` tab and click `Create` after review all requirment.

   <img width="576" height="468" alt="image" src="https://github.com/user-attachments/assets/2b5ec143-f841-4c9a-b331-49856885d375" />


## Task 2: Adjust VM's NSG 

1. Go to virtual machien dashboard and select `Networking` > `Network settings` from navigation pane.

   <img width="231" height="465" alt="image" src="https://github.com/user-attachments/assets/f3a6eb2e-9192-4d12-8e13-e07394647508" />

2. Select VM's NSG from `Rules` section.

   <img width="1341" height="547" alt="image" src="https://github.com/user-attachments/assets/21b089ef-cafa-4288-9bcf-33bed8d9692c" />

3. Click on `+ Create port rule` and select `Inbound port rule` to allow HTTP traffic on port 80.

   <img width="585" height="566" alt="image" src="https://github.com/user-attachments/assets/70da34f0-e8c1-495f-b55d-ae6018cd6807" />

## Task 3: Verify Nginx server accessible from internet.

1. Go to load balancer dashboard and select `datacenter-lb`.

   <img width="1101" height="245" alt="image" src="https://github.com/user-attachments/assets/bb3c459b-ade6-4ff5-87b4-29bc1eb7b6db" />

2. Click `datacenter-lb` and enter it's `Frontend IP Address` in a browser.

   <img width="1081" height="291" alt="image" src="https://github.com/user-attachments/assets/a7698f9a-4359-471d-9968-ab712e030f4d" />

3. Nginx welcome page shoulde be available from that IP address.

   <img width="1361" height="310" alt="image" src="https://github.com/user-attachments/assets/4ef22906-079a-4667-8603-590b7dbf5049" />
