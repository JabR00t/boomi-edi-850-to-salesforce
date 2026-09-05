# Boomi EDI X12 850 to Salesforce Integration

A Boomi integration project that reads an X12 850 Purchase Order from disk, processes EDI qualifiers and instance identifiers, maps the purchase order into a Salesforce custom object, and creates the record through the Salesforce REST API.

## Architecture

```text
EDI X12 850 File
       |
       v
Boomi Disk Connector
       |
       v
X12 850 Profile
       |
       +-- N101 = BT (Bill To)
       +-- N101 = ST (Ship To)
       +-- N101 = SF (Ship From)
       |
       v
N1 Loop Instance Identifiers
       |
       v
Boomi Map
       |
       v
Salesforce REST Connector
       |
       v
Purchase_Order__c