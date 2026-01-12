# Day 15: Create and Configure Network Security Group (NSG) in Azure

- For this task, create a network security group (NSG) with the following requirements:
- Name of the NSG should be `devops-nsg`.
- Add an inbound security rule named `Allow-HTTP` for `HTTP` service on port `80`, with the source CIDR range of `0.0.0.0/0`.
- Add another inbound security rule named `Allow-SSH` for `SSH` service on port `22`, with the source CIDR range of `0.0.0.0/0`.

### Create a network security group

1. In the search box at the top of the portal, enter `Network security group`. Select `Network security groups` in the search results.
2. Select + `Create`.

   <img width="1366" height="563" alt="image" src="https://github.com/user-attachments/assets/914a6567-a850-4c81-8f09-2d68caad6491" />

4. On the Create network security group page, under the Basics tab, enter or select the following values:

   <img width="937" height="408" alt="image" src="https://github.com/user-attachments/assets/63348cb6-2d61-43ac-b99c-8cd6d6161323" />

6. Select `Review + create`.
7. After you see the `Validation passed` message, select `Create`.

   <img width="927" height="538" alt="image" src="https://github.com/user-attachments/assets/29f404ec-f0f1-4631-803b-8402d44b4b7b" />

8. Click on the newly created resource and in it's navigation pane, select `Settings, inbound rule`

   <img width="245" height="514" alt="image" src="https://github.com/user-attachments/assets/bfab3cc4-1733-41e9-ad96-4686067e1c32" />

9. In `inbound rules`, Click on `+ Add` and add `HTTP` for port `80` and name it `Allow-HTTP` and click `Save`.

    <img width="1348" height="593" alt="image" src="https://github.com/user-attachments/assets/00cebe03-3819-4cce-b019-d71b4ac2d9a5" />

10. In `inbound rules`, Click on `+ Add` and add `SSH` for port `22` and name it `Allow-SSH` and click `Save`.

    <img width="585" height="569" alt="image" src="https://github.com/user-attachments/assets/9dbb3d48-363d-4f5e-8c9d-c7f283f0c4c6" />

10. Preview added inbound rules.

    <img width="1101" height="360" alt="image" src="https://github.com/user-attachments/assets/338a5837-6bb2-4299-b25d-d04513d7bf15" />


