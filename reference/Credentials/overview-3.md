---
title: Overview
excerpt: This section covers api abd sdk methods related to Credential object.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Structure

Credential objects have the following structure:

```json
 {
   "GUID": "00000000-0000-0000-0000-000000000000",
   "TenantGUID": "00000000-0000-0000-0000-000000000000",
   "UserGUID": "00000000-0000-0000-0000-000000000000",
   "Name": "Default credential",
   "BearerToken": "default",
   "Active": true,
   "CreatedUtc": "2025-01-20T03:07:36.530841Z",
   "LastUpdateUtc": "2025-01-20T03:07:36.530841Z"
 }
```

## Properties

* **`GUID`** - A globally unique identifier for the credential, represented as a UUID string.
* **`TenantGUID`** - A globally unique identifier for the tenant associated with the credential, represented as a UUID string.
* **`UserGUID`** - A globally unique identifier for the user associated with the credential, represented as a UUID string.
* **`Name`** - The name or description of the credential.
* **`BearerToken`** - The token used for authorization, typically included in HTTP requests for bearer authentication.
* **`Active`** - A boolean flag indicating whether the credential is currently active (`true`) or inactive (`false`).
* **`CreatedUtc`** - The date and time (in UTC) when the credential was initially created.
* **`LastUpdateUtc`** - The date and time (in UTC) when the credential object was last updated.
