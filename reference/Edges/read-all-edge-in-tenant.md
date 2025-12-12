---
title: Read All Edge In Tenant
excerpt: >-
  Retrieve all edges within a tenant, with support for ordering, pagination, and
  optional inclusion of data and subordinate objects.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `Read All Edge In Tenant` endpoint allows you to retrieve a list of all edge objects within a specified tenant. This operation supports ordering, pagination (skip), and optional inclusion of additional data or subordinate objects. It’s ideal for retrieving a comprehensive list of edges when you need to manage or view the relationships between entities in the tenant.

**Important:**  The request requires a valid authentication token and appropriate permissions within the tenant to retrieve the data.

## Read All Edge In Tenant

Retrieve all edges within a tenant using the following `GET request:
GET: /v1.0/tenants/{tenant-guid}/edges/all`
This endpoint returns a list of all edge objects in the tenant, with optional query parameters for ordering, pagination, and inclusion of additional data.

**Authentication:** Admin or appropriate tenant-level authentication required.

**Parameters:**

* **Tenant GUID (required):** The unique identifier of the tenant.
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

const EdgeReadAllInTenant = async () => {
  try {
    const data = await api.Edge.readAllInTenant();
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
