---
title: Check Tag Existence
excerpt: >-
  Comprehensive guide for checking tag existence using HEAD requests, including
  validation procedures, existence verification, and efficient tag lookup
  operations for effective tag management and data validation.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Tag existence checking operations provide a lightweight and efficient way to verify whether specific tags exist in your graph database without retrieving their full data. This functionality is essential for validation, conditional operations, and optimizing API calls by avoiding unnecessary data transfer. Understanding tag existence checking is crucial for building robust applications that need to validate tag presence before performing operations.

Key capabilities include:

* Checking tag existence using lightweight HEAD requests
* Validating tag GUIDs before performing operations
* Optimizing API calls by avoiding full data retrieval
* Supporting conditional logic based on tag presence
* Providing fast existence verification for large datasets

These operations support various use cases such as data validation, conditional processing, API optimization, and building robust error handling mechanisms.

## Check Tag Existence

Check if a tag exists using `HEAD: /v1.0/tenants/{tenant-guid}/tags/{tag-guid}`. This endpoint performs a lightweight existence check without returning the tag data, making it ideal for validation and conditional operations.

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const existsTag = async () => {
  try {
    const data = await api.Tag.exists("<tag-guid>");
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

def exists_tag():
    exists = litegraph.Tag.exists(guid="tag-guid")
    print(exists)

exists_tag()
```

### Response

The API returns different status codes based on tag existence:

* **200 OK**: Tag exists and is accessible
* **404 Not Found**: Tag does not exist or is not accessible

## Next Steps

After checking tag existence, consider these next actions:

* **Conditional Operations**: Perform different actions based on existence results
* **Create Missing Tags**: Create tags that don't exist if needed
* **Update Existing Tags**: Modify tags that already exist
