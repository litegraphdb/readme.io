---
title: Update Node
excerpt: Update existing nodes in a graph with new properties, labels, tags, data, and vector embeddings while maintaining graph integrity and relationships.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Update Node endpoint allows you to modify existing nodes within a graph. This functionality is essential for:

- Updating node names and descriptions
- Modifying labels and tags for better categorization
- Changing node data and metadata
- Updating vector embeddings for semantic search
- Maintaining graph consistency during data evolution
- Implementing node lifecycle management

## Update Node

Update an existing node's information using `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}`. This endpoint allows you to modify node properties including name, labels, tags, data, and vector embeddings while preserving the node's unique identifier and relationships.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My test node 2",
    "Labels": [
        "test",
        "updated"
    ],
    "Tags": {
        "updated": "true"
    },
    "Data": {
        "Updated": "Data"
    }
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const updateNode = async () => {
  // Node object to update
  const node: Node = {
    TenantGUID: "<tenant-guid>",
    GUID: "<node-guid>",
    GraphGUID: "<graph-guid>",
    Name: "Sample Node",
    Data: {
      key1: "value2",
    },
    CreatedUtc: "2024-10-19T14:35:20.351Z",
    Labels: ["test"],
    Tags: {
      Type: "ActiveDirectory",
    },
    Vectors: [],
    LastUpdateUtc: "2024-10-19T14:35:20.351Z",
  };

  try {
    const updatedNode = await api.Node.update(node);
    console.log(updatedNode, "Node updated successfully");
  } catch (err) {
    console.log("Error creating node:", JSON.stringify(err));
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

def update_node():
    node = litegraph.Node.update(guid="node-guid",name="Sample Node")
    print(node)

update_node()
```

## Response

Upon successful update, the API returns a `200 OK` status code with the updated node object in the response body. The response includes all node properties with the updated values and automatically updated timestamps.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "Name": "My test node 2",
  "Labels": ["test", "updated"],
  "Tags": {
    "updated": "true"
  },
  "Data": {
    "Updated": "Data"
  },
  "Vectors": [],
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:15:42.123456Z"
}
```

## Next Steps

After successfully updating a node, you can:

- Verify the update by reading the node data
- Update related edges and relationships if needed
- Perform graph traversal to check for consistency
- Update dependent systems that reference the node
- Implement node change notifications
- Create node update history and audit logs
- Set up automated node validation and testing
- Build node management interfaces for ongoing maintenance
