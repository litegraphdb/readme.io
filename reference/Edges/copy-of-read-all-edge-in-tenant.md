---
title: Read All Edge In Graph
excerpt: >-
  Retrieve all edges within a specific graph, with support for ordering,
  pagination, and optional inclusion of data and subordinate objects. This
  operation validates that the graph exists before returning results.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `Read All Edge In Graph` endpoint allows you to retrieve a list of all edge objects within a specified graph in a tenant. It supports ordering, pagination (skip), and optional inclusion of additional data or subordinate objects. Additionally, it validates that the specified graph exists before returning the results.

**Important:**  The request requires a valid authentication token and appropriate permissions within the tenant to retrieve the data. The graph must exist for the operation to proceed.

## Read All Edge In Graph

Retrieve all edges within a graph using the following `GET request:
GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/all`
This endpoint returns a list of all edge objects in the graph, with optional query parameters for ordering, pagination, and inclusion of additional data.

**Authentication:** Admin or appropriate tenant-level authentication required.

**Parameters:**

* **Tenant GUID (required):** The unique identifier of the tenant.
* **Graph GUID (required):** The unique identifier of the graph within the tenant.
* **Order (optional):** The order in which to return the edges (e.g., ascending, descending).
* **Skip (optional, for pagination):** The number of results to skip for pagination.
* **IncludeData (optional):** Whether to include additional data with each edge.
* **IncludeSubordinates (optional):** Whether to include subordinate objects related to the edges.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>", 
  "*******"  
);

const EdgeReadAllInGraph = async () => {
  try {
    const data = await api.Edge.readAllInGraph('<graph-guid>');  
    console.log(data, 'All edges data');
  } catch (err) {
    console.log('Error:', JSON.stringify(err));
  }
};

```

## Response

The GET request returns a list of edge objects or an error if the request is not successful.

* **200 OK:** A list of edges in the tenant is returned in the response body.
* **401 Unauthorised:** Admin authentication is required to perform this action.
* **404 Not Found:** The specified tenant does not exist.

<br />
