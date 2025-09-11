---
title: Check Tenant Existence
excerpt: >-
  Check if a specific tenant exists in your LiteGraph instance by its unique
  identifier using lightweight HEAD requests with administrative authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Check Tenant Existence endpoint allows you to efficiently verify whether a specific tenant exists in your LiteGraph instance without retrieving the full tenant data. This is particularly useful for:

* Validating tenant IDs before performing operations
* Implementing conditional logic based on tenant existence
* Optimizing applications by avoiding unnecessary data retrieval
* Performing lightweight existence checks in bulk operations
* Administrative monitoring and tenant management

**Important**: Tenant existence checks require administrative privileges and must use the LiteGraph administrative bearer token for authentication.

## Check Tenant Existence

Verify if a tenant exists by its unique identifier using `HEAD: /v1.0/tenants/{tenant-guid}`. This endpoint returns only HTTP status codes without any response body, making it ideal for quick existence checks.

```curl
curl --location --head 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const tenantExists = async () => {
  try {
    const data = await api.Tenant.exists("<tenant-guid>");
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

def tenant_exists():
    exists = litegraph.Tenant.exists(guid="tenant-guid")
    print(exists)

tenant_exists()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

public static class Example
{
    public static async Task Main(string[] args)
    {
        LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
        liteGraph.InitializeRepository();
        bool exists = liteGraph.Tenant.ExistsByGuid(Guid.Parse("<tenant-guid>"));
    }
}
```

## Response

The HEAD request returns only HTTP status codes without any response body:

* **200 OK**: The tenant exists and is accessible
* **404 Not Found**: The tenant does not exist
