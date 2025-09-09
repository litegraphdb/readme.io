---
title: Update Tag
excerpt: >-
  Comprehensive guide for updating existing tags, including modifying tag
  key-value pairs, updating metadata, and handling tag modifications with proper
  validation and error handling for effective tag management.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

Tag update operations allow you to modify existing tags within your graph database. This functionality is essential for maintaining data accuracy, correcting errors, and adapting tag information as your application requirements evolve. Understanding tag update operations is crucial for effective data management and ensuring your tag system remains current and relevant.

Key capabilities include:

- Updating tag key-value pairs to reflect new information
- Modifying tag metadata and properties
- Maintaining data integrity during updates

These operations support various use cases such as data correction, tag refinement, metadata updates, and maintaining consistency across your graph database.

## Update Tag

Update an existing tag using `PUT: /v1.0/tenants/{tenant-guid}/tags/{tag-guid}`. This endpoint allows you to modify the key-value pair and other properties of a specific tag while preserving its unique identifier and maintaining its associations with nodes or edges.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Key": "updatedkey",
    "Value": "myvalue"
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const updateTag = async () => {
  try {
    const data = await api.Tag.update({
      GraphGUID: "<graph-guid>",
      NodeGUID: "<node-guid>",
      EdgeGUID: "<edge-guid>",
      Key: "updatedkey",
      Value: "myvalue",
      CreatedUtc: "2024-12-27T18:12:38.653402Z",
      LastUpdateUtc: "2024-12-27T18:12:38.653402Z",
      GUID: guid,
      TenantGUID: "",
    });
    console.log(data, "check data");
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

def update_tag():
    tag = litegraph.Tag.update(guid="tag-guid",key="updatedkey",value="myvalue")
    print(tag)

update_tag()
```

### Response

Upon successful tag update, the API returns a `200 OK` status code with the updated tag object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": "00000000-0000-0000-0000-000000000001",
  "EdgeGUID": null,
  "Key": "updatedkey",
  "Value": "myvalue",
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:15:42.123456Z"
}
```

## Next Steps

After successfully updating tags, consider these next actions:

- **Verify Changes**: Read the updated tag to confirm changes were applied correctly
- **Update Dependencies**: Check if any dependent systems need to be notified of changes
- **Monitor Impact**: Track how tag updates affect related operations and queries
- **Document Changes**: Maintain documentation of tag modification history
- **Optimize Performance**: Review update patterns for potential performance improvements
