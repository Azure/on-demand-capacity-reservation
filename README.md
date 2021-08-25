This repo has resources that will be used for on-demand capacity reservation public preview program

Detailed documentation available at - https://docs.microsoft.com/en-us/azure/virtual-machines/capacity-reservation-overview



***Not able to deploy Virtual Machines or Virtual Machine Scale Sets (Uniform) with Capacity Reservation***

If you have an existing Capacity Reservations that you are not able to use with Virtual Machines or Virtual Machine Scale Sets, it could be because of any of the reasons below:

1. Limitations and Restrictions of Capacity Reservation
       a. Not all deployment constraints are currently supported. Some of the constraints are:
              i. Proximity Placement Group
              ii. Update domains
              iii. UltraSSD storage 
       b. Spot VMs and Azure Dedicated Host Nodes are not supported with capacity reservation. 
       c. For the supported VM series during public preview, up to 3 Fault Domains (FDs) will be supported. A deployment with more than 3 FDs will fail to deploy against capacity reservation.
       d. Availability Sets are not supported with capacity reservation. 
       e. The scope for capacity reservation is subscription i.e., only the subscription that created the reservation can use it.  So, if your VM/VMSS is in a different subscription, please create a new reservation in that subscription or create your VM/VMSS in the subscription that already has access to the capacity reservation.

2. Not deploying explicitly against the reservation 
   In order to consume Capacity Reservation, it should be explicitly added as a property of the Virtual Machine or Virtual Machine Scale Sets. Please refer to the documentation below to learn more about how to do that:
        • Click [here](https://docs.microsoft.com/en-us/azure/virtual-machines/capacity-reservation-associate-vm) to learn more about how to associate a new Virtual Machine to Capacity Reservation 
        • Click [here](https://docs.microsoft.com/en-us/azure/virtual-machines/capacity-reservation-associate-vm-scale-set) to learn more about how to associate a new Virtual Machine Scale Sets to Capacity Reservation 


3. Trying to attach running VM/VMSS without deallocating them first 
   In order to attach running VM/VMSS to Capacity Reservation, they need to be deallocated first and then at the time of reallocation, reference Capacity Reservation as a property of the VM/VMSS. 


***Not able to create Capacity Reservation***

Following are some of the reasons why you are not able to create capacity reservation:

1. Lack of capacity in the Region/Availability Zone
   Azure doesn't have capacity for the combination of requested VM size/location/Qty. In this case, either retry after some time as new capacity might become available or try a different combination of VM size/location/Qty. 
   Please note that Capacity Reservation creation succeeds or fails in its entirety. For a request to reserve 10 instances, success is returned only if all 10 could be allocated. Otherwise, the capacity reservation creation will fail.

2. Unsupported VM size
   Not all VM sizes are supported with Capacity Reservation. During Public Preview, we support only Av2, B, D, E, & F VM series. Support for other VM series is in progress and will be announced when available. 

3. Subscription doesn't have the required quota 
   Restricted by quota: Creating capacity reservations requires quota in the same manner as it does for creating virtual machines. If you get insufficient quota error while creating capacity reservation, please request additional quota by clicking [here](https://docs.microsoft.com/en-us/azure/azure-portal/supportability/per-vm-quota-requests) or try a different combination of VM size/location/Qty.

4. Don’t have access to create reservation
   Reservations are only available to paid Azure customers. Sponsored accounts such as Free Trial and Azure for Students are not eligible to use this feature. In order to create a new paid Azure subscription, please click [here](https://docs.microsoft.com/en-us/azure/azure-portal/supportability/per-vm-quota-requests).


Steps to create Capacity Reservation
https://docs.microsoft.com/en-us/azure/virtual-machines/capacity-reservation-create



***Not able to delete Capacity Reservation or Group***
 
Capacity Reservations can be deleted only when no Virtual Machines or Virtual Machine Scale Sets are associated to the group. 

Click [here](https://docs.microsoft.com/en-us/azure/virtual-machines/capacity-reservation-modify) for detailed steps on how to delete capacity reservation. 

Azure will only allow a Capacity Reservation Group to be deleted when all member Capacity Reservations.




***Capacity Reservation in “Failed” provisioning State***

It is possible, in a very rare circumstances, that an existing Capacity Reservation goes into a “Failed” provisioning state due to a system error or due to a customer-initiated action such as modifying the quantity reserved. In most cases, just retrying should fix the issue. However, in case the Capacity Reservation goes into the “Failed” provisioning state as a result of increasing the quantity reserved, just retrying may not fix the issue. In this situation, follow the steps below to restore the reservation:

Steps:
1. Go to the [Application Change Analysis](https://ms.portal.azure.com/#blade/Microsoft_Azure_ChangeAnalysis/ChangeAnalysisBaseBlade) screen on Azure portal. 
2. From the filters at the top of the page, select subscription, resource group, and time range. Please note that you can only go back up to 14 days in the past.
3. In the search box, type in the name of the capacity reservation and look for the change in “sku.capacity” property for that reservation. Find out the original quantity reserved which will be the value under the “Old Value” column. 
4. Update capacity reservation to the old quantity reserved by following the steps detailed here. Once updated, the reservation should be available immediately for use with virtual machines. 

If capacity reservation is still in failed provisioning state after taking the steps above, please create a support ticket. 

