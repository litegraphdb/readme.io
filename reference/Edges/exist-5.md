---
title: Check Edge Existence
excerpt: >-
  Comprehensive guide for checking edge existence using HEAD requests, including
  validation procedures, existence verification, and efficient edge lookup
  operations for effective edge management and data validation.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Edge existence checking operations provide a lightweight and efficient way to verify whether specific edges exist in your graph database without retrieving their full data. This functionality is essential for validation, conditional operations, and optimizing API calls by avoiding unnecessary data transfer. Understanding edge existence checking is crucial for building robust applications that need to validate edge presence before performing operations.

Key capabilities include:

* Checking edge existence using lightweight HEAD requests
* Validating edge GUIDs before performing operations
* Optimizing API calls by avoiding full edge data retrieval
* Supporting conditional logic based on edge presence
* Providing fast existence verification for large edge datasets

These operations support various use cases such as edge data validation, conditional processing, API optimization, and building robust error handling mechanisms.

## Check Edge Existence

Check if an edge exists using `HEAD: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}`. This endpoint performs a lightweight existence check without returning the edge data, making it ideal for validation and conditional operations.

```curl
curl --location --request HEAD 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const existsEdge = async () => {
  try {
    const data = await api.Edge.exists("<edge-guid>");
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
    graph_guid="Graph-Guid",
    access_key="******",
)

def exists_edge():
    exists = litegraph.Edge.exists(guid="edge-guid")
    print(exists)

exists_edge()
```

### Response

The API returns different status codes based on edge existence:

* **200 OK**: Edge exists and is accessible
* **404 Not Found**: Edge does not exist or is not accessible
