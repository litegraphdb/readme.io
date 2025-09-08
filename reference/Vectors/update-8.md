---
title: Update Vector
excerpt: Comprehensive guide for updating existing vectors, including modifying vector embeddings, updating metadata, and handling vector modifications with proper validation and error handling for effective vector management.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

Vector update operations allow you to modify existing vector embeddings within your graph database. This functionality is essential for maintaining data accuracy, correcting vector embeddings, and adapting vector information as your application requirements evolve. Understanding vector update operations is crucial for effective vector management and ensuring your vector system remains current and relevant.

Key capabilities include:

- Updating vector embeddings and dimensional data
- Modifying vector metadata and properties
- Maintaining data integrity during updates
- Handling validation and error scenarios
- Preserving vector relationships and associations

These operations support various use cases such as vector refinement, metadata updates, model migration, and maintaining consistency across your vector database.

## Update Vector

Update an existing vector using `PUT: /v1.0/tenants/{tenant-guid}/vectors/{vector-guid}`. This endpoint allows you to modify the vector embeddings, metadata, and other properties of a specific vector while preserving its unique identifier and maintaining its associations with nodes or edges.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Model": "all-MiniLM-L6-v2",
    "Dimensionality": 384,
    "Content": "test",
    "Vectors": [
        0.1,
        0.2,
        0.3
    ]
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const updateVector = async () => {
  try {
    const data = await api.Vector.update({
      GUID: "<vector-guid>",
      GraphGUID: "<graph-guid>",
      NodeGUID: "<node-guid>",
      EdgeGUID: "<edge-guid>",
      Model: "all-MiniLM-L6-v2",
      Dimensionality: 388,
      Content: "test",
      Vectors: [0.5, 0.7, 0.9],
      TenantGUID: "",
      CreatedUtc: "",
      LastUpdateUtc: "",
    });
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

### Response

Upon successful vector update, the API returns a `200 OK` status code with the updated vector object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": null,
  "EdgeGUID": null,
  "Model": "all-MiniLM-L6-v2",
  "Dimensionality": 384,
  "Content": "test",
  "Vectors": [0.1, 0.2, 0.3],
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:15:42.123456Z"
}
```

## Next Steps

After successfully updating vectors, consider these next actions:

- **Verify Changes**: Read the updated vector to confirm changes were applied correctly
- **Update Dependencies**: Check if any dependent systems need to be notified of changes
- **Monitor Impact**: Track how vector updates affect related operations and queries
- **Document Changes**: Maintain documentation of vector modification history
- **Optimize Performance**: Review update patterns for potential performance improvements
