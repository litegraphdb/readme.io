---
title: Get Node Children
excerpt: Retrieve all child nodes connected to a specific parent node to analyze hierarchical relationships and tree structures in your graph.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Get Node Children endpoint allows you to discover all child nodes directly connected to a specific parent node in your graph. This operation is essential for understanding hierarchical relationships, analyzing tree structures, and building comprehensive parent-child relationship maps.

Key capabilities include:

- Finding all child nodes connected to a specific parent node
- Analyzing hierarchical relationship patterns and tree structures
- Discovering all nodes that are direct descendants of the parent node
- Building hierarchical node profiles and relationship maps
- Supporting tree traversal and hierarchical path analysis

## Get Node Children

Retrieve all child nodes connected to a specific parent node using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/children`. This endpoint returns all nodes that are direct children of the specified parent node, allowing you to analyze hierarchical relationships and understand the tree structure of your graph.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000/children' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getChildrenFromNode = async () => {
  try {
    const data = await api.Route.getChildrenFromNode(guid, nodeGuid);
    console.log(data, "check data");
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

def get_children_of_node():
    children = litegraph.RouteNodes.children(
        graph_guid="graph-guid",
        node_guid="node-guid"
    )
    print(children)

get_children_of_node()
```

### Response

```json
[
  {
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
    "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
    "Name": "My test node",
    "CreatedUtc": "2025-09-09T10:03:05.160383Z",
    "LastUpdateUtc": "2025-09-09T10:03:05.160383Z",
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

When retrieving node children, consider the following recommendations:

- **Validate Node GUID**: Ensure the parent node GUID exists before making requests
- **Handle Empty Results**: Implement proper handling for nodes with no children

After retrieving node children, you can:

- Analyze hierarchical relationship patterns and tree structures
- Build comprehensive hierarchical node profiles and relationship maps
- Implement tree traversal algorithms for hierarchical path analysis
- Create hierarchical node visualization interfaces
- Perform tree structure analysis and organizational studies
- Develop hierarchical recommendation systems and relationship discovery
