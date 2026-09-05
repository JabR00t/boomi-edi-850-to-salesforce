# Troubleshooting

## OAuth invalid_grant

Error:

`invalid_grant, request not supported on this domain`

Cause:

The generic Salesforce login token endpoint was used for Client Credentials authentication.

Solution:

Use the Salesforce My Domain token endpoint:

`https://<my-domain>/services/oauth2/token`

---

## Salesforce REST 404

Error:

`404 - The requested resource does not exist`

Cause:

The configured Salesforce REST API version was not available for the org.

Solution:

Use a supported API version in the Service URL.

Example:

`https://<my-domain>/services/data/v67.0`

---

## Purchase_Order__c Missing From Boomi Import

Boomi returned hundreds of Salesforce objects and limited the browser to 500 results.

Solution:

Use the Filter field during Salesforce REST Operation Import:

`Purchase_Order__c`

Also ensure the OAuth Run As user has access to the custom object.

---

## Salesforce Object Permissions

The custom Purchase Order object was not initially visible through the API.

Solution:

Create a permission set and grant:

- Read
- Create
- Edit

Also grant Read/Edit field-level access to the custom fields.

---

## EDI Date Parsing Error

Error:

`Failed parsing '20260905~' due to extra trailing character '~'`

Cause:

Boomi was treating `~` as part of BEG05 instead of the X12 segment terminator.

Solution:

Configure the EDI profile delimiters:

- Element delimiter: `*`
- Segment terminator: `~`
- Composite delimiter: `>`

The Date Format map function then converts:

`yyyyMMdd`

to:

`yyyy-MM-dd`