# Boomi Component Inventory

## Connections

- `CONN - Disk - Inbound EDI 850`
- `CONN - Salesforce REST`

## Operations

- `OP - Disk - Query EDI 850 Files`
- `OP - Salesforce REST - Create Purchase Order`

## Profiles

- `PROFILE - X12 850 Purchase Order`
- `Salesforce REST Purchase_Order__c CREATE Request`

## Maps

- `MAP - X12 850 to Salesforce Purchase Order`

## Processes

- `PROC - Inbound EDI 850 to Salesforce`

## EDI Qualifiers

N101 qualifiers:

| Code | Meaning |
|---|---|
| BT | Bill-to-Party |
| ST | Ship To |
| SF | Ship From |

## Instance Identifiers

The instance identifiers are defined at the N1 Loop level:

- `N1 Loop [N101=BT]`
- `N1 Loop [N101=ST]`
- `N1 Loop [N101=SF]`

## Boomi Components

The Boomi components used by this integration are documented in:

[Component Inventory](boomi/component-inventory.md)

The EDI-to-Salesforce mapping has also been exported from Boomi:

[Map Export](boomi/exports/x12-850-to-salesforce-map.xlsx)