# Boomi EDI X12 850 to Salesforce Integration

A Boomi integration project that reads an X12 850 Purchase Order from disk, processes EDI qualifiers and instance identifiers, maps the purchase order into a Salesforce custom object, and creates the record through the Salesforce REST API.

## Architecture

```mermaid
flowchart LR
    A[EDI X12 850 File] --> B[Boomi Disk Connector]
    B --> C[X12 850 Profile]
    C --> D[N1 Qualifiers & Instance Identifiers]
    D --> E[Boomi Map]
    E --> F[Salesforce REST Connector]
    F --> G[Purchase_Order__c]
```

## Integration Flow

1. Boomi reads an X12 850 Purchase Order from disk.
2. The X12 850 EDI profile parses the document.
3. N101 qualifiers identify:
   - `BT` — Bill To
   - `ST` — Ship To
   - `SF` — Ship From
4. Instance Identifiers distinguish the repeating N1 loops.
5. The Boomi Map transforms the EDI fields into the Salesforce structure.
6. The Salesforce REST connector creates a `Purchase_Order__c` record.

## Field Mapping

| X12 850 Source | Salesforce Field |
|---|---|
| BEG03 | Name |
| BEG05 | Order_Date__c |
| N1 Loop [BT] → N102 | Bill_To_Name__c |
| N1 Loop [BT] → N4 → N401 | Bill_To_City__c |
| N1 Loop [ST] → N102 | Ship_To_Name__c |
| N1 Loop [ST] → N4 → N401 | Ship_To_City__c |
| N1 Loop [SF] → N102 | Ship_From_Name__c |

## Screenshots

### X12 850 Profile

![X12 850 Profile](docs/screenshots/02-edi-profile.png)

### N101 Qualifiers

![N101 Qualifiers](docs/screenshots/03-n101-qualifiers.png)

### Instance Identifiers

![Instance Identifiers](docs/screenshots/04-instance-identifiers.png)

### EDI to Salesforce Map

![Boomi Map](docs/screenshots/05-boomi-map.png)

### Boomi Process

![Boomi Process](docs/screenshots/06-main-process.png)

### Salesforce Result

![Salesforce Result](docs/screenshots/07-salesforce-result.png)