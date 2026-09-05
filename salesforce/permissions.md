# Salesforce Permissions

A dedicated permission set named:

`Boomi Salesforce Integration`

was created for the integration.

## Object Permissions

For `Purchase_Order__c`:

- Read
- Create
- Edit

## Field Permissions

Read and Edit access were enabled for:

- Order_Date__c
- Bill_To_Name__c
- Bill_To_City__c
- Ship_To_Name__c
- Ship_To_City__c
- Ship_From_Name__c

The permission set is assigned to the Salesforce user used by the OAuth Client Credentials flow.