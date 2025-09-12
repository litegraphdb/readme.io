---
title: Check Credential Existence
excerpt: >-
  Check if a specific credential exists in a tenant by its unique identifier
  using lightweight HEAD requests with proper authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Check Credential Existence endpoint allows you to efficiently verify whether a specific credential exists within a tenant without retrieving the full credential data.

**Important**: Credential existence checks require appropriate permissions within the tenant and must use a valid authentication token.

## Check Credential Existence

Verify if a credential exists by its unique identifier using `HEAD: /v1.0/tenants/{tenant-guid}/credentials/{credential-guid}`. This endpoint returns only HTTP status codes without any response body, making it ideal for quick existence checks.

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const existsCredential = async () => {
  try {
    const data = await api.Credential.exists("<credential-guid>");
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    access_key="******",
)

def exists_credential():
    exists = litegraph.Credential.exists(guid="credential-guid")
    print(exists)

exists_credential()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
bool exists = liteGraph.Credential.ExistsByGuid(Guid.Parse("<tenant-guid>"), Guid.Parse("<credential-guid>"));
```

## Response

The HEAD request returns only HTTP status codes without any response body:

* **200 OK**: The credential exists and is accessible
* **404 Not Found**: The credential does not exist
