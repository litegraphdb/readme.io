---
title: Delete Tag
excerpt: >-
  Comprehensive guide for deleting individual tags and performing bulk tag
  deletion operations, including proper cleanup procedures, data integrity
  considerations, and safe deletion practices for effective tag management.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Tag deletion operations provide the ability to remove tags from your graph database when they are no longer needed. These operations are essential for maintaining data cleanliness, removing obsolete information, and managing storage efficiently. Understanding tag deletion is crucial for proper data lifecycle management and ensuring your tag system remains organized and relevant.

Key capabilities include:

* Deleting individual tags by their unique GUID
* Performing bulk deletion of multiple tags
* Maintaining data integrity during deletion operations

These operations support various use cases such as data cleanup, tag lifecycle management, storage optimization, and maintaining data quality standards.

## Delete Single Tag

Delete a single tag using `DELETE: /v1.0/tenants/{tenant-guid}/tags/{tag-guid}`. This endpoint allows you to remove a specific tag by its unique identifier, permanently deleting it from the system and cleaning up any associated relationships.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/00000000-0000-0000-0000-000000000000' \
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

const deleteTag = async () => {
  try {
    const data = await api.Tag.delete("<tag-guid>");
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Delete Multiple Tags

Delete multiple tags in a single operation using `DELETE: /v1.0/tenants/{tenant-guid}/tags/bulk`. This bulk operation allows you to efficiently remove multiple tags by providing an array of tag GUIDs, which is useful for batch cleanup operations and maintaining data organization.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/bulk' \
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

const deleteMultipleTags = async () => {
  try {
    const data = await api.Tag.deleteBulk([tagGUID1,tagGUID2]);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

### Response

Upon successful tag deletion, the API returns a `200 No Content` status code indicating the tag has been successfully removed from the system.

## Best Practices

## Next Steps

After successfully deleting tags, consider these next actions:

* **Verify Deletion**: Confirm tags have been removed by attempting to read them
* **Update Dependencies**: Check if any dependent systems need to be updated
* **Clean Up References**: Remove any local references to deleted tags
