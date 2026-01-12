# Day 10: Attach Public IP to Azure Virtual Machine

- An existing VM named `nautilus-vm-pip` and a public IP address named `nautilus-pip` already exist.
- Attach the public IP `nautilus-pip` to the network interface of the VM `nautilus-vm-pip`.
- Make sure the VM is properly assigned the public IP.

Azure Docs to be followed: [Associate a public IP address to a virtual machine](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/associate-public-ip-address-vm?tabs=azure-portal#prerequisites)

## Associate a public IP address to a virtual machine

1. Sign in to the [Azure portal](https://portal.azure.com/).

2. In the portal, search for and select the VM that you want to add the public IP address to.

3. Under `Settings` in the left pane, select `Networking`, and then select the network interface you want to add the public IP address to.

   <img width="1345" height="509" alt="image" src="https://github.com/user-attachments/assets/fafa7e65-7d91-44d2-a13a-e17821105029" />

4. From the `Network interface` window, under `Settings`, select `IP configurations`, `Enable IP forwarding` and then select an IP configuration from the list.

   <img width="1350" height="527" alt="image" src="https://github.com/user-attachments/assets/2155f517-3df0-4d0a-80ac-575cea11afda" />

5. In the `Edit IP configuration` window, select `Associate public IP address`, then select `Public IP address` to choose an existing public IP address from the drop-down list.

6. Select `Apply`.

8. Search for `Public IP Addresses` and find existing `nautilius-pip`

   <img width="1366" height="426" alt="image" src="https://github.com/user-attachments/assets/27e862b8-bdc2-479f-a0c1-7b9b2878325f" />

10. Select the IP Address, and click on `Associate to a resource`

    <img width="1366" height="514" alt="image" src="https://github.com/user-attachments/assets/712857d1-273c-44aa-8967-b5931fdd4be5" />

12. From dialouge box, select `Resource Type` as `Network Interface` and choose the network interface of your vm and click `Ok`.

    <img width="585" height="568" alt="image" src="https://github.com/user-attachments/assets/5b51e2ce-48df-4558-a1bc-adc56f7c4a77" />

7. In the `IP Configurations window`, view the public IP address assigned to the IP configuration. It might take a few seconds for a newly associated IP address to appear.

   <img width="1078" height="184" alt="image" src="https://github.com/user-attachments/assets/bb39cb8e-a51c-48b8-a30a-7528f800d866" />
