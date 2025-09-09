---
title: Get Routes
excerpt: >-
  Discover all possible routes between two nodes to analyze path connectivity
  and implement advanced graph traversal algorithms.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Get Routes endpoint allows you to discover all possible paths between two specific nodes in your graph. This operation is essential for understanding path connectivity, analyzing route options, and implementing advanced graph traversal algorithms for pathfinding and route optimization.

Key capabilities include:

* Finding all possible routes between two specific nodes
* Analyzing path connectivity and route options
* Discovering multiple path alternatives and route variations
* Building comprehensive route maps and path analysis
* Supporting advanced graph traversal and pathfinding algorithms

## Get Routes

Discover all possible routes between two specific nodes using `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/routes`. This endpoint returns all possible paths that connect the source and destination nodes, allowing you to analyze route options, path connectivity, and implement advanced pathfinding algorithms.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/routes' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "From": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
    "To": "769a880c-85b6-422e-8aa2-c6f160bd24c6"
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getRoutes = async () => {
  try {
    const data = await api.Route.getRoutes(graphGuid, fromNodeGuid, toNodeGuid);
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

def get_routes():
    routes = litegraph.Routes.routes(
        graph_guid="Graph-Guid",
        from_guid="Node-Guid",
        to_guid="Node-Guid",
    )
    print(routes)

get_routes()
```

### Response

```json
{
  "Timestamp": {
    "Start": "2025-09-09T10:11:28.588952Z",
    "End": "2025-09-09T10:11:28.605901Z",
    "TotalMs": 16.95,
    "Messages": {}
  },
  "Routes": [
    {
      "TotalCost": 10,
      "Edges": [
        {
          "TenantGUID": "00000000-0000-0000-0000-000000000000",
          "GUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
          "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
          "Name": "My test edge",
          "From": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
          "To": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
          "Cost": 10,
          "CreatedUtc": "2025-09-09T10:03:46.978477Z",
          "LastUpdateUtc": "2025-09-09T10:03:46.978477Z",
          "Data": {
            "Hello": "World"
          }
        }
      ]
    }
  ]
}
```

## Best Practices

When retrieving routes between nodes, consider the following recommendations:

* **Validate Node GUIDs**: Ensure both source and destination node GUIDs exist before making requests
* **Handle Empty Results**: Implement proper handling for cases where no routes exist between nodes
* **Analyze Route Costs**: Consider the total cost and edge costs when evaluating route options
* **Cache Results**: Consider caching route information for frequently accessed node pairs
* **Performance Monitoring**: Track response times for complex route calculations

## Next Steps

After retrieving routes between nodes, you can:

* Analyze path connectivity and route options for optimization
* Build comprehensive route maps and path analysis systems
* Implement advanced graph traversal algorithms for pathfinding
* Create route visualization interfaces and path exploration tools
* Perform route optimization and path analysis studies
* Develop route-based recommendation systems and navigation algorithms
