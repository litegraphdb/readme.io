---
title: Delete Node Edges (Bulk)
excerpt: >-
  Deletes all edges connected to multiple nodes within a graph. This bulk
  operation removes all edges associated with each node GUID in the provided
  list. It validates that the graph exists and that the GUIDs list is not null
  before performing the deletion.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `Delete Node Edges (Bulk)` endpoint allows you to delete all edges associated with multiple nodes within a graph. This bulk deletion operation removes the edges for all the nodes provided in the list, helping to efficiently clean up relationships for multiple nodes at once. This operation ensures that the graph exists and that the provided list of node GUIDs is valid before performing the deletion.

**Important:** This operation requires administrative privileges. Once the edges are deleted, the operation is irreversible, and all relationships connected to the nodes will be removed.

Key capabilities include:

* Deleting edges for multiple nodes in bulk.
* Validating graph existence before performing the deletion.
* Ensuring that the provided list of node GUIDs is valid.

## Delete Node Edges (Bulk)

Delete all edges connected to multiple nodes within a graph using the following `DELETE request:
DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/edges/bulk`
This operation removes all edges connected to each node GUID in the provided list for the specified graph.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",  // Replace with actual Tenant GUID
  "*******"  // Replace with authentication token
);

const EdgeDeleteNodeEdgesMany = async () => {
  try {
    const data = await api.Edge.deleteAllNodeEdges('<graph-guid>', [
      "<node-guid-1>",  // Replace with actual Node GUIDs
      "<node-guid-2>"
    ]);
    console.log(data, 'All node edges deleted in bulk');
  } catch (err) {
    console.log('Error:', JSON.stringify(err));
  }
};
```

## Response

Upon successful deletion, the API returns a **200 No Content** status code, indicating that all edges connected to the specified nodes have been successfully removed from the graph. No response body is returned for successful deletions.

* **200 No Content:** All edges for the specified nodes have been successfully deleted.
* **401 Unauthorized:** Admin authentication is required to perform this action.
* **404 Not Found:** The specified tenant, graph, or node does not exist.

## Best Practices

When deleting edges for multiple nodes, consider the following recommendations:

* **Verify Node and Graph GUIDs:** Ensure the node and graph GUIDs are correct before deletion to avoid unintended loss of data.
* **Backup Important Data:** Consider backing up critical edge data before deletion
* **Check Dependencies:** Ensure no critical systems or processes depend on the edges being deleted.
* **Handle Errors Gracefully:** Implement proper error handling in case the deletion process encounters issues.
* **Monitor Impact:** Track the effects of edge deletions on graph structure and related operations.

## Next Steps

After successfully deleting the edges for a node, consider these next actions:

* **Verify Deletion:** Confirm edges have been removed by attempting to read the edges for the node
* **Update Dependencies:** Check if any dependent systems need to be updated to reflect the changes in the node’s relationships.
* **Clean Up References:** Remove any local references to deleted edges.
* **Monitor System:** Watch for any issues that might arise from the deletions, especially related to graph structure.
* **Document Changes:** Maintain documentation of deletion operations for future reference.
* **Optimize Storage:** Review storage usage and ensure that removing the edges has optimized graph performance.
