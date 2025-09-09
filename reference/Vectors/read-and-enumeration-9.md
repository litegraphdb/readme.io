---
title: Read and Enumerate Vectors
excerpt: >-
  Comprehensive guide for reading individual vectors, retrieving multiple
  vectors by GUIDs, reading all vectors, and performing enumeration operations
  with search capabilities for efficient vector management and data retrieval.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

Vector reading and enumeration operations provide comprehensive access to vector data within your graph database. These operations enable you to retrieve individual vectors, fetch multiple vectors by their GUIDs, read all vectors in a tenant, and perform advanced enumeration with search capabilities. Understanding these operations is essential for effective vector management, data analysis, and application development.

Key capabilities include:

- Reading individual vectors by their unique GUID
- Retrieving multiple specific vectors using comma-separated GUIDs
- Reading all vectors within a tenant for comprehensive data access
- Enumerating vectors with pagination support for large datasets
- Advanced search and filtering capabilities for targeted vector retrieval

These operations support various use cases such as vector data validation, similarity analysis, bulk operations, and integration with external systems that require vector information.

## Read Individual Vector

Read a single vector using `GET: /v1.0/tenants/{tenant-guid}/vectors/{vector-guid}`. This endpoint retrieves a specific vector by its unique identifier, providing complete vector information including embeddings, metadata, and timestamps.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readVector = async () => {
  try {
    const data = await api.Vector.read("<vector-guid>");
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

def retrieve_vector():
    vector = litegraph.Vector.retrieve(guid="vector-guid")
    print(vector)

retrieve_vector()
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with the vector object in the response body.

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
  "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
}
```

## Read Multiple Vectors by GUIDs

Retrieve multiple specific vectors using `GET: /v1.0/tenants/{tenant-guid}/vectors?guids=<vector1-guid>,<vector2-guid>`. This endpoint allows you to fetch multiple vectors in a single request by providing comma-separated GUIDs, which is efficient for retrieving specific vector sets without fetching all vectors.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyVectors = async () => {
  try {
    const data = await api.Vector.readMany([vectorGuid]);
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

def retrieve_multiple_vector():
    vectors = litegraph.Vector.retrieve_many(guids=["vector-guid-1","vector-guid-2])
    print(vectors)

retrieve_multiple_vector()
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with an array of vector objects in the response body.

```json
[
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
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  },
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Model": "all-MiniLM-L6-v2",
    "Dimensionality": 384,
    "Content": "test 2",
    "Vectors": [0.4, 0.5, 0.6],
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Read All Vectors

Retrieve all vectors within a tenant using `GET: /v1.0/tenants/{tenant-guid}/vectors`. This endpoint provides comprehensive access to all vector data in your tenant, useful for data analysis, backup operations, and complete vector inventory management.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllVectors = async () => {
  try {
    const data = await api.Vector.readAll();
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

def retrieve_all_vector():
    vectors = litegraph.Vector.retrieve_all()
    print(vectors)

retrieve_all_vector()
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with an array of all vector objects in the response body.

```json
[
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
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Enumeration (GET)

Perform vector enumeration using `GET: /v2.0/tenants/{tenant-guid}/vectors`. This v2.0 endpoint provides enhanced enumeration capabilities with built-in pagination support, making it ideal for handling large vector datasets efficiently and systematically browsing through vector collections.

Enumeration via `GET:/v2.0/tenants/{tenant-guid}/vectors` allows to enumerate response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateVectors = async () => {
  try {
    const data = await api.Vector.enumerate();
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

def enumerate_vector():
    vectors = litegraph.Vector.enumerate()
    print(vectors)

enumerate_vector()
```

### Response

```json
{
  "Success": true,
  "Timestamp": {
    "Start": "2025-09-08T11:37:23.166261Z",
    "End": "2025-09-08T11:37:23.174110Z",
    "TotalMs": 7.85,
    "Messages": {}
  },
  "MaxResults": 5,
  "EndOfResults": true,
  "TotalRecords": 1,
  "RecordsRemaining": 0,
  "Objects": [
    {
      "GUID": "72f9cb54-1081-4b6f-a07d-c86d9e0c5150",
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "NodeGUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
      "Model": "all-MiniLM-L6-v2",
      "Dimensionality": 384,
      "Content": "test",
      "Vectors": [0.1, 0.2, 0.3],
      "CreatedUtc": "2025-09-08T10:18:03.777113Z",
      "LastUpdateUtc": "2025-09-08T10:18:03.777113Z"
    }
  ]
}
```

## Enumeration and search (POST)

Enumeration via `POST :/v2.0/tenants/{tenant-guid}/vectors` allows to enumerate and search response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/tags' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Ordering": "CreatedDescending",
    "IncludeData": false,
    "IncludeSubordinates": false,
    "MaxResults": 5,
    "Skip": 0,
    "ContinuationToken": null,
    "Labels": [ ],
    "Tags": { },
    "Expr": { }
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateAndSearchVectors = async () => {
  try {
    const data = await api.Vector.enumerateAndSearch({
      Ordering: "CreatedDescending",
      IncludeData: false,
      IncludeSubordinates: false,
      MaxResults: 5,
      ContinuationToken: null,
      Labels: [],
      Tags: {},
      Expr: {},
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

def enumerate_with_query_vector():
    vectors = litegraph.Vector.enumerate_with_query(
        ordering="CreatedDescending",
        MaxResults=10,
        Skip=0,
        IncludeData=True,
        IncludeSubordinates=True,
        Expr=litegraph.ExprModel(
            Left="Name",
            Operator="Equals",
            Right="Test"
        )
    )
    print(vectors)

enumerate_with_query_vector()
```

### Response

```json
{
  "Success": true,
  "Timestamp": {
    "Start": "2025-09-08T11:37:23.166261Z",
    "End": "2025-09-08T11:37:23.174110Z",
    "TotalMs": 7.85,
    "Messages": {}
  },
  "MaxResults": 5,
  "EndOfResults": true,
  "TotalRecords": 1,
  "RecordsRemaining": 0,
  "Objects": [
    {
      "GUID": "72f9cb54-1081-4b6f-a07d-c86d9e0c5150",
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "NodeGUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
      "Model": "all-MiniLM-L6-v2",
      "Dimensionality": 384,
      "Content": "test",
      "Vectors": [0.1, 0.2, 0.3],
      "CreatedUtc": "2025-09-08T10:18:03.777113Z",
      "LastUpdateUtc": "2025-09-08T10:18:03.777113Z"
    }
  ]
}
```

<br />
