---
title: Read Credential By BearerToken
excerpt: >-
  Check if a specific credential exists by using its bearer token with proper
  authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `CredentialReadByBearer`Token endpoint enables retrieval of a credential object by its bearer token. This endpoint requires admin authentication, and the bearer token is used to verify access. It allows administrators to fetch the credential details if it exists, or a Not Found error will be returned if the credential does not exist.

**Important:** This operation requires admin-level authentication and the correct bearer token for accessing the credential data.

## Credential Read by Bearer Token

Retrieve a credential using its bearer token with the following `GET request: /v1.0/credentials/bearer/{bearerToken}`. The request expects a valid bearer token and returns the corresponding credential if found. If the credential does not exist, a **404 Not Found** error is returned.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const CredentialReadByBearerToken = async () => {
  try {
    const data = await api.Credential.readByBearerToken('def****'); // Replace 'def****' with actual bearer token
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Response

The `GET` request will return the credential object or an error based on its existence:

* **200 OK:** The credential is found and returned in the response body.
* **404 Not Found:** The credential does not exist in the system.

<br />
