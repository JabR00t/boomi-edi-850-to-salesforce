# Changelog

## v1.0.0

Initial working version of the Boomi EDI 850 to Salesforce integration.

### Features

- Reads X12 850 Purchase Order files from Disk
- Parses X12 850 using a Boomi EDI profile
- Uses N101 qualifiers:
  - BT - Bill To
  - ST - Ship To
  - SF - Ship From
- Uses N1 Loop Instance Identifiers
- Maps EDI purchase order data to Salesforce
- Connects to Salesforce through the Salesforce REST connector
- Uses OAuth 2.0 Client Credentials
- Creates records in `Purchase_Order__c`
- Includes sample EDI data
- Includes screenshots and troubleshooting documentation
