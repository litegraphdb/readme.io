---
title: Create Credential
excerpt: Create new authentication credentials for users including bearer tokens and API keys with proper security validation and access control.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Create Credential endpoint allows you to generate new authentication credentials for users within a tenant.

## Create Credential

Create a new credential for a user using `PUT: /v1.0/tenants/{tenant-guid}/credentials`. This endpoint generates authentication credentials that can be used for API access and user authentication.

```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "UserGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "New credential",
    "BearerToken": "foobar",
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

const createCredential = async () => {
  try {
    const data = await api.Credential.create({
      UserGUID: "<user-guid>",
      Name: "New credential",
      BearerToken: "foobar",
      Active: true,
    });
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Request Parameters

The credential creation request accepts the following parameters:

- **UserGUID**: The unique identifier of the user for whom the credential is being created (string, required)
- **Name**: A descriptive name for the credential (string, required)
- **BearerToken**: The bearer token value for authentication (string, required)
- **Active**: Whether the credential is active and can be used for authentication (boolean, required)

**Note**: The BearerToken should be a secure, randomly generated value. Consider using cryptographically secure random generators for production environments.

## Response

Upon successful credential creation, the API returns a `201 Created` status code with the created credential object in the response body. The response includes all credential properties with system-generated values.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "UserGUID": "00000000-0000-0000-0000-000000000000",
  "Name": "Default credential",
  "BearerToken": "default",
  "Active": true,
  "CreatedUtc": "2025-08-29T13:54:55.175279Z",
  "LastUpdateUtc": "2025-08-29T13:54:55.174491Z"
}
```

## Next Steps

After successfully creating a credential, you can:

- Test the credential by using it for API authentication
- Implement credential management interfaces for users
- Set up credential rotation and expiration policies
- Create credential monitoring and usage tracking
- Implement credential revocation mechanisms
- Build credential sharing and delegation features
- Set up automated credential validation and testing
