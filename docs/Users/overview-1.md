---
title: Overview
excerpt: This section covers api abd sdk methods related to User object.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Structure

Tenant objects have the following structure:

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "FirstName": "Default",
  "LastName": "user",
  "Email": "default@user.com",
  "Password": "password",
  "Active": true,
  "CreatedUtc": "2025-01-20T03:07:17.100136Z",
  "LastUpdateUtc": "2025-01-20T03:07:17.100137Z"
}
```

## Properties

* **`GUID`** - A globally unique identifier for the user, represented as a UUID string.
* **`TenantGUID`** - A globally unique identifier for the tenant that the user belongs to, represented as a UUID string.
* **`FirstName`** - The given name of the user.
* **`LastName`** - The surname (family name) of the user.
* **`Email`** - The email address associated with the user.
* **`Password`** - The password credential for the user’s account (stored as plain text here, but should be secured and hashed in practice).
* **`Active`** - A boolean flag indicating whether the user account is currently active (`true`) or inactive (`false`).
* **`CreatedUtc`** - The date and time (in UTC) when the user account was initially created.
* **`LastUpdateUtc`** - The date and time (in UTC) when the user account object was last updated.