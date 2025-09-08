---
title: Delete Vector
excerpt: >-
  Comprehensive guide for deleting individual vectors and performing bulk vector
  deletion operations, including proper cleanup procedures, vector index
  management, and safe deletion practices for efficient vector storage
  management.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Vector deletion operations provide the ability to remove vector embeddings from your graph database when they are no longer needed. These operations are essential for maintaining storage efficiency, removing obsolete vector data, and managing vector indexes effectively. Understanding vector deletion is crucial for proper vector lifecycle management and ensuring your vector system remains organized and performant.

Key capabilities include:

* Deleting individual vectors by their unique GUID
* Performing bulk deletion of multiple vectors
* Maintaining vector index integrity during deletion operations

These operations support various use cases such as vector data cleanup, storage optimization, model migration, and maintaining vector system performance.

## Delete Single Vector

Delete a single vector using `DELETE: /v1.0/tenants/{tenant-guid}/vectors/{vector-guid}`. This endpoint allows you to remove a specific vector by its unique identifier, permanently deleting it from the system and cleaning up any associated vector indexes and relationships.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/00000000-0000-0000-0000-000000000000' \
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

const deleteVector = async () => {
  try {
    const data = await api.Vector.delete("<vector-guid>");
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

def delete_vector():
    litegraph.Vector.delete(guid="vector-guid")
    print("Vector deleted")
```

## Delete Multiple Vectors

Delete multiple vectors in a single operation using `DELETE: /v1.0/tenants/{tenant-guid}/vectors/bulk`. This bulk operation allows you to efficiently remove multiple vectors by providing an array of vector GUIDs, which is useful for batch cleanup operations and maintaining vector storage organization.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/bulk' \
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

const deleteMultipleVectors = async () => {
  try {
    const data = await api.Vector.deleteBulk([vector - guid]);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Response

Upon successful vector deletion, the API returns a `204 No Content` status code indicating the vector has been successfully removed from the system.

## Next Steps

After successfully deleting vectors, consider these next actions:

* **Verify Deletion**: Confirm vectors have been removed by attempting to read them
* **Update Dependencies**: Check if any dependent systems need to be updated
* **Clean Up References**: Remove any local references to deleted vectors
* **Monitor System**: Watch for any issues that might arise from the deletions
* **Document Changes**: Maintain documentation of deletion operations
* **Optimize Storage**: Review storage usage improvements from the cleanup
