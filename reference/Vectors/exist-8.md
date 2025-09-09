---
title: Check Vector Existence
excerpt: >-
  Comprehensive guide for checking vector existence using HEAD requests,
  including validation procedures, existence verification, and efficient vector
  lookup operations for effective vector management and data validation.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

Vector existence checking operations provide a lightweight and efficient way to verify whether specific vectors exist in your graph database without retrieving their full data.

These operations support various use cases such as vector data validation, conditional processing, API optimization, and building robust error handling mechanisms.

## Check Vector Existence

Check if a vector exists using `HEAD: /v1.0/tenants/{tenant-guid}/vectors/{vector-guid}`. This endpoint performs a lightweight existence check without returning the vector data, making it ideal for validation and conditional operations.

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const existsVector = async () => {
  try {
    const data = await api.Vector.exists("<vector-guid>");
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

def exists_vector():
    exists = litegraph.Vector.exists(guid="vector-guid-1")
    print(exists)

exists_vector()
```

### Response

The API returns different status codes based on vector existence:

- **200 OK**: Vector exists and is accessible
- **404 Not Found**: Vector does not exist
