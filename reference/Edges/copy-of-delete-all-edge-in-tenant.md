---
title: Delete Node Edges (Single)
excerpt: >-
  Deletes all edges connected to a specific node within a graph. This operation
  removes all edges (both incoming and outgoing) associated with the specified
  node GUID in the given graph. The graph is validated before the deletion
  process begins.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `Delete Node Edges` endpoint allows you to delete all edges connected to a specific node within a graph. This includes both incoming and outgoing edges associated with that node. It is useful for cleaning up all relationships for a particular node within the graph, ensuring that the node is disconnected from all other nodes in the graph.

**Important:** This operation requires valid administrative privileges. The operation checks if the graph exists before performing the deletion. Once the edges are deleted, the operation is irreversible, and the node will no longer have any connections to other nodes in the graph.

Key capabilities include:

* Deleting both incoming and outgoing edges for a node.
* Ensuring graph existence before performing the deletion.
* Maintaining the integrity of the graph by cleaning up relationships.

## Delete Node Edges

Delete all edges connected to a specific node in a graph using the following `DELETE request:
DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/edges`
This operation removes all edges (both incoming and outgoing) connected to the node, completely severing the node’s relationships with other nodes.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>", 
  "*******" 
);

const EdgeDeleteNodeEdges = async (nodeGuid, graphGuid) => {
  try {
    const data = await api.Edge.deleteNodeEdges(nodeGuid, graphGuid); 
    console.log(data, 'All edges for node deleted');
  } catch (err) {
    console.log('Error:', JSON.stringify(err));
  }
};
```

## Response

Upon successful deletion, the API returns a **200 No Content** status code, indicating that all edges connected to the node have been successfully removed from the graph. No response body is returned for successful deletions.

* **200 No Content:** All edges in the specified tenant have been successfully deleted.
* **401 Unauthorized:** Admin authentication is required to perform this action.
* **404 Not Found:** The specified tenant does not exist.

## Best Practices

When deleting edges, consider the following recommendations:

* **Verify Node and Graph GUIDs:** Ensure the node and graph GUIDs are correct before deletion to avoid unintended loss of data.
* **Backup Important Data:** Consider backing up critical edge data before deletion
* **Check Dependencies:** Ensure no critical systems or processes depend on the edges being deleted.
* **Use Appropriate Authentication:** Only authorized users should be allowed to delete edges, as this is an irreversible operation.
* **Handle Errors Gracefully:** Implement proper error handling in case the deletion process encounters issues.
* **Monitor Impact:** Track the impact of edge deletions on graph integrity and related operations.

## Next Steps

After successfully deleting the edges for a node, consider these next actions:

* **Verify Deletion:** Confirm edges have been removed by attempting to read the edges for the node
* **Update Dependencies:** Check if any dependent systems need to be updated to reflect the changes in the node’s relationships.
* **Clean Up References:** Remove any local references to deleted edges.
* **Monitor System:** Watch for any issues that might arise from the deletions, especially related to graph structure.
* **Document Changes:** Maintain documentation of deletion operations for future reference.
* **Optimize Storage:** Review storage usage and ensure that removing the edges has optimized graph performance.
