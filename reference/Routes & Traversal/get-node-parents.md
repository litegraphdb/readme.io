---
title: Get Node Parents
excerpt: Retrieve all parent nodes connected to a specific child node to analyze hierarchical relationships and tree structures in your graph.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Get Node Parents endpoint allows you to discover all parent nodes directly connected to a specific child node in your graph. This operation is essential for understanding hierarchical relationships, analyzing tree structures, and building comprehensive parent-child relationship maps.

Key capabilities include:

- Finding all parent nodes connected to a specific child node
- Analyzing hierarchical relationship patterns and tree structures
- Discovering all nodes that are direct ancestors of the child node
- Building hierarchical node profiles and relationship maps
- Supporting tree traversal and hierarchical path analysis

## Get Node Parents

Retrieve all parent nodes connected to a specific child node using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/parents`. This endpoint returns all nodes that are direct parents of the specified child node, allowing you to analyze hierarchical relationships and understand the tree structure of your graph.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000/parents' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getParentsFromNode = async () => {
  try {
    const data = await api.Route.getParentsFromNode(graphGuid, nodeGuid);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err), err);
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

def get_parents_of_node():
    parents = litegraph.RouteNodes.parents(
        graph_guid="graph-guid",
        node_guid="node-guid"
    )
    print(parents)

get_parents_of_node()
```

### Response

```json
[
    {
        "TenantGUID": "00000000-0000-0000-0000-000000000000",
        "GUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
        "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
        "Name": "My test node",
        "CreatedUtc": "2025-09-08T10:18:03.776249Z",
        "LastUpdateUtc": "2025-09-08T10:18:03.776249Z",
        "Data": {
            "Hello": "World",
            "Foo": {
                "Data": "hello"
            }
        }
    }
]
```

## Best Practices

When retrieving node parents, consider the following recommendations:

- **Validate Node GUID**: Ensure the child node GUID exists before making requests
- **Handle Empty Results**: Implement proper handling for nodes with no parents


## Next Steps

After retrieving node parents, you can:

- Analyze hierarchical relationship patterns and tree structures
- Build comprehensive hierarchical node profiles and relationship maps
- Implement tree traversal algorithms for hierarchical path analysis
- Create hierarchical node visualization interfaces
- Perform tree structure analysis and organizational studies
- Develop hierarchical recommendation systems and relationship discovery
