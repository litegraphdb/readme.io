---
title: Delete Label
excerpt: >-
  Comprehensive guide for deleting individual labels and performing bulk label
  deletion operations, including proper cleanup procedures, data integrity
  considerations, and safe deletion practices for effective label management.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Label deletion operations provide the ability to remove labels from your graph database when they are no longer needed. These operations are essential for maintaining data cleanliness, removing obsolete labels, and managing storage efficiently. Understanding label deletion is crucial for proper label lifecycle management and ensuring your label system remains organized and relevant.

Key capabilities include:

* Deleting individual labels by their unique GUID
* Performing bulk deletion of multiple labels
* Maintaining data integrity during deletion operations
* Handling cleanup of label associations and relationships
* Ensuring proper authorization and validation

These operations support various use cases such as data cleanup, label lifecycle management, storage optimization, and maintaining data quality standards.

## Delete Single Label

Delete a single label using `DELETE: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`. This endpoint allows you to remove a specific label by its unique identifier, permanently deleting it from the system and cleaning up any associated relationships.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
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

const deleteLabel = async () => {
  try {
    const data = await api.Label.delete("<label-guid>");
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

def delete_label():
    litegraph.Label.delete(guid="label-guid")
    print("Label deleted")

delete_label()
```

## Delete Multiple Labels

Delete multiple labels in a single operation using `DELETE: /v1.0/tenants/{tenant-guid}/labels/bulk`. This bulk operation allows you to efficiently remove multiple labels by providing an array of label GUIDs, which is useful for batch cleanup operations and maintaining label organization.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/bulk' \
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

const deleteMultipleLabels = async () => {
  try {
    const data = await api.Label.deleteBulk([label - guid]);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Response

Upon successful label deletion, the API returns a `200 No Content` status code indicating the label has been successfully removed from the system.

## Next Steps

After successfully deleting labels, consider these next actions:

* **Verify Deletion**: Confirm labels have been removed by attempting to read them
* **Update Dependencies**: Check if any dependent systems need to be updated
* **Clean Up References**: Remove any local references to deleted labels
* **Monitor System**: Watch for any issues that might arise from the deletions
* **Document Changes**: Maintain documentation of deletion operations
* **Optimize Storage**: Review storage usage improvements from the cleanup
