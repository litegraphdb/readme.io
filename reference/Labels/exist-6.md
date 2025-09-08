---
title: Check Label Existence
excerpt: >-
  Comprehensive guide for checking label existence using HEAD requests,
  including validation procedures, existence verification, and efficient label
  lookup operations for effective label management and data validation.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Label existence checking operations provide a lightweight and efficient way to verify whether specific labels exist in your graph database without retrieving their full data. This functionality is essential for validation, conditional operations, and optimizing API calls by avoiding unnecessary data transfer. Understanding label existence checking is crucial for building robust applications that need to validate label presence before performing operations.

Key capabilities include:

* Checking label existence using lightweight HEAD requests
* Validating label GUIDs before performing operations
* Optimizing API calls by avoiding full label data retrieval
* Supporting conditional logic based on label presence
* Providing fast existence verification for large label datasets

These operations support various use cases such as label data validation, conditional processing, API optimization, and building robust error handling mechanisms.

## Check Label Existence

Check if a label exists using `HEAD: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`. This endpoint performs a lightweight existence check without returning the label data, making it ideal for validation and conditional operations.

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const existsLabel = async () => {
  try {
    const data = await api.Label.exists("<label-guid>");
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

def exists_label():
    exists = litegraph.Label.exists(guid="label-guid")
    print(exists)

exists_label()
```

### Response

The API returns different status codes based on label existence:

* **200 OK**: Label exists and is accessible
* **404 Not Found**: Label does not exist or is not accessible
