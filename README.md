# Boomi EDI X12 850 to Salesforce Integration

A Boomi integration project that reads an X12 850 Purchase Order from disk, processes EDI qualifiers and instance identifiers, maps the purchase order into a Salesforce custom object, and creates the record through the Salesforce REST API.

## Documentation

- [Setup Guide](docs/setup.md)
- [Troubleshooting](docs/troubleshooting.md)
- [Boomi Component Inventory](boomi/component-inventory.md)
- [Salesforce Object Schema](salesforce/object-schema.md)
- [Salesforce Permissions](salesforce/permissions.md)

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

## Repository Structure

```text
.
├── boomi/
│   └── exports/
├── docs/
│   ├── architecture/
│   ├── screenshots/
│   └── troubleshooting.md
├── sample-data/
│   ├── inbound/
│   └── expected-output/
├── salesforce/
│   ├── object-schema.md
│   └── permissions.md
├── README.md
└── .gitignore
```

## Boomi Components

The Boomi components used by this integration are documented in:

[Component Inventory](boomi/component-inventory.md)

The EDI-to-Salesforce mapping has also been exported from Boomi:

[Map Export](boomi/exports/x12-850-to-salesforce-map.xlsx)

## Setup Guide

For step-by-step instructions to recreate the integration, see:

[Setup Guide](docs/setup.md)


## Validation

The integration was tested end-to-end using the sample X12 850 file:

`sample-data/inbound/PO_850_001.edi`

The Boomi process completed successfully and created a Salesforce record in:

`Purchase_Order__c`

Verified values:

| Salesforce Field | Value |
|---|---|
| `Name` | `PO12345` |
| `Bill_To_Name__c` | `ABC CORPORATION` |
| `Bill_To_City__c` | `NEW YORK` |
| `Ship_To_Name__c` | `ABC WAREHOUSE` |
| `Ship_To_City__c` | `CHICAGO` |
| `Ship_From_Name__c` | `XYZ FACTORY` |

The result was verified using SOQL:

```sql
SELECT Name, Bill_To_Name__c, Bill_To_City__c, Ship_To_Name__c, Ship_To_City__c, Ship_From_Name__c FROM Purchase_Order__c WHERE Name = 'PO12345'
```

See the execution and Salesforce result screenshots in:

`docs/screenshots/`

