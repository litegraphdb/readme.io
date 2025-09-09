---
title: Check Node Existence
excerpt: Check if a specific node exists in a graph using lightweight HEAD requests for efficient existence validation without data transfer.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Check Node Existence endpoint allows you to verify whether a specific node exists in a graph without retrieving the actual node data. This functionality is essential for:

## Check Node Existence

Verify if a specific node exists in the graph using `HEAD: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}`. This lightweight operation returns only HTTP status codes without transferring node data, making it ideal for existence validation.

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const checkIfNodeExistsById = async () => {
  try {
    const data = await api.Node.exists(graphGuid, nodeGuid);
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
    graph-guid="Graph-Guid",
    access_key="******",
)

def exists_node():
    exists = litegraph.Node.exists(guid="node-guid")
    print(exists)

exists_node()
```

## Response

The HEAD request returns only HTTP status codes without any response body:

- **200 OK**: The node exists and is accessible
- **404 Not Found**: The node does not exist or you don't have access to it

## Next Steps

After checking node existence, you can:

- Proceed with node operations if the node exists
- Create the node if it doesn't exist and creation is needed
- Handle missing nodes gracefully in your application logic
