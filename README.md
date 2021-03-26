**Welcome to the Private Preview program for On-demand capacity reservation! We are very excited to have you as a customer and look forward to receiving your feedback for this new feature.**

This preview is designed for our customers to test out the feature and try our APIs and provide any feedback. For now, private preview will only support limited VM SKU sizes for standalone VMs in South Central and West Central US regions. We will be adding support for Virtual Machine Scale Sets in the next few weeks as part of the private preview program. For the list of supported scenarios, please refer to the "On-Demand Capacity Reservation.docx". We will be updating the list of supported scenarios as needed. 


**Supporting documents**
1. To learn more about the feature, please read the feature overview document called "On-Demand Capacity Reservation.docx"
2. API details are provided in the document - On-Demand Capacity Reservation-APIs.docx
3. Same ARM templates are in the file - Sample ARM Template.zip

**Note:** 
1. The feature is currently in Private Preview phase. That means, customers should only use it for testing purposes. It is not recommended to use this feature at this point for any mission-critical workloads. **For the purpose of testing, it is advised to only create reservations for less than 5 instances of any VM size in order to keep the cost low**
3. The feature is currently supported via ARM templates only. Other client tools support such as Azure Portal, CLI, PS etc. will be coming later.
4.	During Private Preview, production SLAs will not be enforced. 

**Billing** 

During Private Preview, you will be charged for the virtual machines that are attached to a capacity reservation. You will also be charged for the unused capacity reservation spots. For more information on billing, please read “VM Capacity Reservations: Usage and Billing” section in the "On-Demand Capacity Reservation.docx" document. 

**Supported Regions during Private Preview**
During private preview, the only supported regions are South Central US and West Central US. That said, it is technically possible to deploy reservations in other regions as well. Howerver, the E2E functionaltiy may not work as expected. Hence, it is strongly advised to only use the supported regions for this private preview program. 


Let's get started!
