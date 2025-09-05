---
title: Update Credential
excerpt: Update existing authentication credentials including bearer tokens, names, and status with proper validation and security controls.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Update Credential endpoint allows you to modify existing authentication credentials within a tenant. This functionality is essential for:

- Updating credential names and descriptions
- Modifying bearer token values
- Changing credential status (active/inactive)
- Implementing credential lifecycle management
- Maintaining security through credential rotation

**Important**: Credential updates require appropriate permissions within the tenant and must use a valid authentication token. All updates are validated before being applied.

## Update Credential

Update an existing credential's information using `PUT: /v1.0/tenants/{tenant-guid}/credentials/{credential-guid}`. This endpoint allows you to modify credential properties including name, bearer token, and active status.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "UserGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Updated credential",
    "BearerToken": "default",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const updateCredential = async () => {
  try {
    const data = await api.Credential.update({
      UserGUID: "<user-guid>",
      Name: "Updated credential",
      BearerToken: "default",
      Active: true,
      LastUpdateUtc: "2024-12-27T18:12:38.653402Z",
      CreatedUtc: "2024-12-27T18:12:38.653402Z",
      GUID: "<credential-guid>",
      TenantGUID: "",
    });
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Request Parameters

The update request accepts the following credential properties:

- **UserGUID**: The unique identifier of the user associated with the credential (string, required)
- **Name**: A descriptive name for the credential (string, required)
- **BearerToken**: The bearer token value for authentication (string, required)
- **Active**: Whether the credential is active and can be used for authentication (boolean, required)
- **GUID**: The credential's unique identifier (string, read-only)
- **TenantGUID**: The tenant's unique identifier (string, read-only)
- **CreatedUtc**: Timestamp when credential was created (string, read-only)
- **LastUpdateUtc**: Timestamp of last update (string, read-only)
  ged by the system.

## Response

Upon successful update, the API returns a `200 OK` status code with the updated credential object in the response body. The response includes all credential properties with the updated values and automatically updated timestamps.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "UserGUID": "00000000-0000-0000-0000-000000000000",
  "Name": "Updated credential",
  "BearerToken": "default",
  "Active": true,
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:15:42.123456Z"
}
```
