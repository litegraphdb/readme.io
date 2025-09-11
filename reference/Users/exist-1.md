---
title: Check User Existence
excerpt: >-
  Check if a specific user exists in a tenant by its unique identifier using
  lightweight HEAD requests with proper authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Check User Existence endpoint allows you to efficiently verify whether a specific user exists within a tenant without retrieving the full user data. This is particularly useful for:

* Validating user IDs before performing operations
* Implementing conditional logic based on user existence
* Optimizing applications by avoiding unnecessary data retrieval
* Performing lightweight existence checks in bulk operations
* User authentication and access control validation

## Check User Existence

Verify if a user exists by its unique identifier using `HEAD: /v1.0/tenants/{tenant-guid}/users/{user-guid}`. This endpoint returns only HTTP status codes without any response body, making it ideal for quick existence checks.

```curl
curl --location --head 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const userExists = async () => {
  try {
    const data = await api.User.exists("<user-guid>");
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

def exists_user():
    exists = litegraph.User.exists(guid="user-guid")
    print(exists)

exists_user()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
bool exists = liteGraph.User.ExistsByGuid(Guid.Parse("<tenant-guid>"), Guid.Parse("<user-guid>"));
```

## Response

The HEAD request returns only HTTP status codes without any response body:

* **200 OK**: The user exists and is accessible
* **404 Not Found**: The user does not exist or you don't have access to it
