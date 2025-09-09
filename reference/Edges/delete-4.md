---
title: Delete Edge
excerpt: Comprehensive guide for deleting individual edges, performing bulk edge deletion operations, and deleting all edges, including proper cleanup procedures, data integrity considerations, and safe deletion practices for effective edge management.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

Edge deletion operations provide the ability to remove edges from your graph database when they are no longer needed. These operations are essential for maintaining data cleanliness, removing obsolete relationships, and managing storage efficiently. Understanding edge deletion is crucial for proper edge lifecycle management and ensuring your graph structure remains organized and relevant.

Key capabilities include:

- Deleting individual edges by their unique GUID
- Performing bulk deletion of multiple edges
- Deleting all edges within a graph for complete cleanup
- Maintaining data integrity during deletion operations
- Handling cleanup of edge associations and relationships

These operations support various use cases such as relationship cleanup, edge lifecycle management, storage optimization, and maintaining data quality standards.

## Delete Single Edge

Delete a single edge using `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}`. This endpoint allows you to remove a specific edge by its unique identifier, permanently deleting it from the system and cleaning up any associated relationships.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/00000000-0000-0000-0000-000000000000' \
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

const deleteEdgeById = async () => {
  try {
    const data = await api.Edge.delete(guid, edgeGuid);
    console.log(data, "chk data");
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

def delete_edge():
    litegraph.Edge.delete(guid="edgeGuid")
    print("Edge deleted")

delete_edge()
```

## Delete Multiple Edges

Delete multiple edges in a single operation using `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/bulk`. This bulk operation allows you to efficiently remove multiple edges by providing an array of edge GUIDs, which is useful for batch cleanup operations and maintaining edge organization.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    "00000000-0000-0000-0000-000000000000"
]'
```

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteMultipleEdges = async () => {
  try {
    const data = await api.Edge.deleteBulk(guid, [edge - guid]);
    console.log(data, "chk data");
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

def delete_multiple_edge():
    litegraph.Edge.delete_multiple(guid=["edge-guid-1","edge-guid"])
    print("Edges deleted")

delete_multiple_edge()
```

## Delete All Edges

Delete all edges within a graph using `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/all`. This operation removes all edges from the specified graph, which is useful for complete graph cleanup or resetting edge relationships while preserving nodes.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/all' \
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

const deleteAllEdges = async () => {
  try {
    const data = await api.Edge.deleteAll("<graph-guid>");
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
    graph_guid="Graph-Guid",
    access_key="******",
)

def delete_all_edge():
    litegraph.Edge.delete_all()
    print("Edges deleted")

delete_all_edge()
```

## Response

Upon successful edge deletion, the API returns a `200 No Content` status code indicating the edge has been successfully removed from the system.

## Best Practices

When deleting edges, consider the following recommendations:

- **Verify Before Deletion**: Always confirm the edges you intend to delete are correct
- **Backup Important Data**: Consider backing up critical edge data before deletion
- **Check Dependencies**: Ensure no critical systems depend on the edges being deleted
- **Use Bulk Operations**: Leverage bulk deletion for multiple edges to improve performance
- **Handle Errors Gracefully**: Implement proper error handling for failed deletions
- **Monitor Impact**: Track the effects of edge deletions on related operations
- **Maintain Audit Trail**: Keep records of deletion operations for compliance and debugging

## Next Steps

After successfully deleting edges, consider these next actions:

- **Verify Deletion**: Confirm edges have been removed by attempting to read them
- **Update Dependencies**: Check if any dependent systems need to be updated
- **Clean Up References**: Remove any local references to deleted edges
- **Monitor System**: Watch for any issues that might arise from the deletions
- **Document Changes**: Maintain documentation of deletion operations
- **Optimize Storage**: Review storage usage improvements from the cleanup
