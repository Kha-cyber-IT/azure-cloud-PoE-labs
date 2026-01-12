# Day 11: Change Azure Virtual Machine Size Using Console

- Change the VM size from `Standard_B1s` to `Standard_B2s` for the virtual machine named `xfusion-vm`.
- Ensure the VM is in the `running` state after the size change is complete.
   
Azure Docs to be followed: [Change the size of a virtual machine](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes/resize-vm?tabs=portal#change-the-vm-size)

To change the VM size using the Azure portal:

1. Open the [Azure portal](https://portal.azure.com/).
2. Type virtual machines in the search. Under `Services`, select `Virtual machines`.
4. In the `Virtual machines` page, select the virtual machine you want to resize.

   <img width="1086" height="287" alt="image" src="https://github.com/user-attachments/assets/75606224-668e-4a3a-a496-a14190b367c4" />
   
6. In the left menu, in the `Availability + scale` section, select `size`.

   <img width="246" height="494" alt="image" src="https://github.com/user-attachments/assets/b5270bac-ce17-4adc-9f54-d036c977099b" />

7. Pick a new compatible size from the list of available sizes and then select `Resize`.

   <img width="1074" height="414" alt="image" src="https://github.com/user-attachments/assets/7d46e64d-3a00-4fa5-abcc-bbd4f3ceaadc" />

6. Ensure the vm is in running state from `Virtual Machine` page.

   <img width="1083" height="239" alt="image" src="https://github.com/user-attachments/assets/2b22e20b-a866-4b08-bc52-ef58bcd617b8" />


