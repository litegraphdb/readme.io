---
title: Check Graph Existence
excerpt: >-
  Check if a specific graph exists in your tenant by its unique identifier using
  lightweight HEAD requests.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Graph Existence endpoint allows you to efficiently check whether a specific graph exists in your tenant without retrieving the full graph data. This is particularly useful for:

- Validating graph IDs before performing operations
- Implementing conditional logic based on graph existence
- Optimizing applications by avoiding unnecessary data retrieval
- Performing lightweight existence checks in bulk operations

## Check Graph Existence

Verify if a graph exists by its unique identifier using `HEAD: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}`. This endpoint returns only HTTP status codes without any response body, making it ideal for quick existence checks.

```curl
curl --location --head 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const checkIfGraphExistsById = async () => {
  try {
    const data = await api.Graph.exists(guid);
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

def exists_graph():
    exists = litegraph.Graph.exists(guid="graph-guid")
    print(exists)

exists_graph()
```

## Response

The HEAD request returns only HTTP status codes without any response body:

- **200 OK**: The graph exists and is accessible
- **404 Not Found**: The graph does not exist or you don't have access to it
