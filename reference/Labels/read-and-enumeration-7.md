---
title: Read and Enumerate Labels
excerpt: >-
  Comprehensive guide for reading individual labels, retrieving multiple labels
  by GUIDs, reading all labels, and performing enumeration operations with
  search capabilities for efficient label management and data retrieval.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Label reading and enumeration operations provide comprehensive access to label data within your graph database. These operations enable you to retrieve individual labels, fetch multiple labels by their GUIDs, read all labels in a tenant, and perform advanced enumeration with search capabilities. Understanding these operations is essential for effective label management, data analysis, and application development.

Key capabilities include:

* Reading individual labels by their unique GUID
* Retrieving multiple specific labels using comma-separated GUIDs
* Reading all labels within a tenant for comprehensive data access
* Enumerating labels with pagination support for large datasets
* Advanced search and filtering capabilities for targeted label retrieval

These operations support various use cases such as label data validation, categorization analysis, bulk operations, and integration with external systems that require label information.

## Read Individual Label

Read a single label using `GET: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`. This endpoint retrieves a specific label by its unique identifier, providing complete label information including metadata and timestamps.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readLabel = async () => {
  try {
    const data = await api.Label.read("<label-guid>");
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

def retrieve_label():
    label = litegraph.Label.retrieve(guid="label-guid")
    print(label)

retrieve_label()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
LabelMetadata response = liteGraph.Label.ReadByGuid(Guid.Parse("<tenant-guid>"), Guid.Parse("<label-guid>"));
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with the label object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": null,
  "EdgeGUID": null,
  "Label": "label",
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
}
```

## Read Multiple Labels by GUIDs

Retrieve multiple specific labels using `GET: /v1.0/tenants/{tenant-guid}/labels?guids=<label1-guid>,<label2-guid>`. This endpoint allows you to fetch multiple labels in a single request by providing comma-separated GUIDs, which is efficient for retrieving specific label sets without fetching all labels.

### Response

Upon successful retrieval, the API returns a `200 OK` status code with an array of label objects in the response body.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyLabels = async () => {
  try {
    const data = await api.Label.readMany([labelGuid]);
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

def retrieve_multiple_label():
    labels = litegraph.Label.retrieve_many(guids=["label-guid-1","label-guid-2"])
    print(labels)

retrieve_multiple_label()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<LabelMetadata> response = liteGraph.Label.ReadByGuids(Guid.Parse("<tenant-guid>"), 
                                                                  new List<Guid>()
                                                                  {
                                                                      Guid.Parse("<label-guid-1>"),
                                                                      Guid.Parse("<label-guid-2>"),
                                                                  });
```

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  },
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label2",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Read All Labels

Retrieve all labels within a tenant using `GET: /v1.0/tenants/{tenant-guid}/labels`. This endpoint provides comprehensive access to all label data in your tenant, useful for data analysis, backup operations, and complete label inventory management.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllLabels = async () => {
  try {
    const data = await api.Label.readAll();
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

def retrieve_all_label():
    labels = litegraph.Label.retrieve_all()
    print(labels)

retrieve_all_label()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<LabelMetadata> response = liteGraph.Label.ReadMany(Guid.Parse("<tenant-guid>"), 
                                                               Guid.Parse("<graph-guid>"),
                                                               Guid.Parse("<node-guid>"),
                                                               Guid.Parse("<edge-guid>"),
                                                               label:"label");
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with an array of all label objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Read All Label In Tenant

Retrieves all label metadata within a tenant using `GET: /v1.0/tenants/{tenant-guid}/labels/all`. Returns a list of all label metadata objects in the specified tenant, with support for ordering and pagination.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const LabelReadAllInTenant = async () => {
  try {
    const data = await api.Label.readAllInTenant();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Response

Upon successful retrieval, the API returns a 200 OK status code with an array of all label metadata objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000000",
    "Label": "label",
    "CreatedUtc": "2025-12-11T02:31:04.257088Z",
    "LastUpdateUtc": "2025-12-11T02:31:04.257088Z"
  }
]

```

## Read All Label In Graph

Retrieves all label metadata within a specific graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/labels/all`. Returns a list of all label metadata objects in the specified graph, with support for ordering and pagination. Validates that the graph exists before returning results.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const LabelReadAllInGraph = async () => {
  try {
    const data = await api.Label.readAllInGraph('<graph-guid>');
    console.log(data, 'all label in graph retrieved');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Response

Upon successful retrieval, the API returns a 200 OK status code with an array of all label metadata objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000000",
    "Label": "label",
    "CreatedUtc": "2025-12-11T02:31:04.257088Z",
    "LastUpdateUtc": "2025-12-11T02:31:04.257088Z"
  }
]

```

## Read graph-level labels

Retrieves label metadata associated with a specific graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/labels`. Returns label metadata objects that are directly associated with the graph entity. Validates that the graph exists before returning results.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const LabelReadManyGraph = async (tenantGuid, graphGuid) => {
  try {
    const data = await api.Label.readGraphLevelLabels('<graph-guid>);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Response

Upon successful retrieval, the API returns a 200 OK status code with an array of all label metadata objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000000",
    "Label": "label",
    "CreatedUtc": "2025-12-11T02:31:04.257088Z",
    "LastUpdateUtc": "2025-12-11T02:31:04.257088Z"
  }
]

```

## Read many node

Retrieves label metadata associated with a specific node using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/labels`. Returns label metadata objects that are directly associated with the specified node GUID within a graph. Validates that the graph exists before returning results.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const LabelReadManyNodeLabels = async (tenantGuid, graphGuid, nodeGuid) => {
  try {
    const data = await api.Label.readManyNodeLabels('<graph-guid>', '<node-guid>);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Response

Upon successful retrieval, the API returns a 200 OK status code with an array of all label metadata objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000000",
    "Label": "label",
    "CreatedUtc": "2025-12-11T02:31:04.257088Z",
    "LastUpdateUtc": "2025-12-11T02:31:04.257088Z"
  }
]
```

## Read Many Edge

Retrieves label metadata associated with a specific edge. Returns label metadata objects that are directly associated with the specified edge GUID within a graph. Validates that the graph exists before returning results.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const LabelReadManyEdgeLabels = async (tenantGuid, graphGuid, edgeGuid) => {   
  try {
    const data = await api.Label.readManyEdgeLabels('<graph-guid>', '<edge-guid>');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Response

Upon successful retrieval, the API returns a 200 OK status code with an array of all label metadata objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000000",
    "Label": "label",
    "CreatedUtc": "2025-12-11T02:31:04.257088Z",
    "LastUpdateUtc": "2025-12-11T02:31:04.257088Z"
  }
]
```

## Enumeration (GET)

Perform label enumeration using `GET: /v2.0/tenants/{tenant-guid}/labels`. This v2.0 endpoint provides enhanced enumeration capabilities with built-in pagination support, making it ideal for handling large label datasets efficiently and systematically browsing through label collections.

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/labels' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateLabels = async () => {
  try {
    const data = await api.Label.enumerate();
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

def enumerate_label():
    labels = litegraph.Label.enumerate()
    print(labels)

enumerate_label()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
EnumerationResult<LabelMetadata> response = liteGraph.Label.Enumerate();
```

### Response

```
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-08T12:15:55.555337Z",
        "End": "2025-09-08T12:15:55.560048Z",
        "TotalMs": 4.71,
        "Messages": {}
    },
    "MaxResults": 1000,
    "EndOfResults": false,
    "TotalRecords": 2,
    "RecordsRemaining": 2,
    "Objects": [
        {
            "GUID": "463a4c91-6c58-41cf-8421-e694019476d6",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "72f9cb54-1081-4b6f-a07d-c86d9e0c5150",
            "Label": "updated",
            "CreatedUtc": "2025-09-08T10:47:03.877150Z",
            "LastUpdateUtc": "2025-09-08T10:47:03.877154Z"
        },
        {
            "GUID": "c18aba31-117d-4323-9ecc-d6500f73bdb7",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "00000000-0000-0000-0000-000000000000",
            "Label": "test",
            "CreatedUtc": "2025-09-08T10:46:32.767393Z",
            "LastUpdateUtc": "2025-09-08T10:46:32.767397Z"
        },
    ]
}
```

<br />

## Enumeration and Search (POST)

Perform advanced label enumeration with search capabilities using `POST: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/labels`. This powerful endpoint combines enumeration with sophisticated filtering, sorting, and search functionality, allowing you to find specific labels based on various criteria while maintaining efficient pagination for large result sets.

### Search Parameters

The POST endpoint supports various search and filtering parameters:

* **Ordering**: Sort results by creation time (`CreatedAscending`, `CreatedDescending`)
* **IncludeData**: Include full label data in response (boolean)
* **IncludeSubordinates**: Include related subordinate data (boolean)
* **MaxResults**: Maximum number of results per page (integer)
* **Skip**: Number of results to skip for pagination (integer)
* **ContinuationToken**: Token for continuing pagination (string)
* **Labels**: Filter by specific labels (array)
* **Tags**: Filter by tag key-value pairs (object)
* **Expr**: Advanced expression-based filtering (object)

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/labels' \
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

const enumerateAndSearchLabels = async () => {
  try {
    const data = await api.Label.enumerateAndSearch({
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

def enumerate_with_query_label():
    labels = litegraph.Label.enumerate_with_query(
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
    print(labels)

enumerate_with_query_label()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
EnumerationResult<LabelMetadata> response = liteGraph.Label.Enumerate(new EnumerationRequest()
{
    Ordering = EnumerationOrderEnum.CreatedDescending,
    IncludeData = true,
    IncludeSubordinates = true,
    MaxResults = 5,
    Skip = 0,
    ContinuationToken = null,
    Labels = new List<string>(),
    Tags = null,
    Expr = null
});
```

### Response

```json
{
  "Success": true,
  "Timestamp": {
    "Start": "2025-09-08T12:15:55.555337Z",
    "End": "2025-09-08T12:15:55.560048Z",
    "TotalMs": 4.71,
    "Messages": {}
  },
  "MaxResults": 1000,
  "EndOfResults": false,
  "TotalRecords": 2,
  "RecordsRemaining": 2,
  "Objects": [
    {
      "GUID": "463a4c91-6c58-41cf-8421-e694019476d6",
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "NodeGUID": "72f9cb54-1081-4b6f-a07d-c86d9e0c5150",
      "Label": "updated",
      "CreatedUtc": "2025-09-08T10:47:03.877150Z",
      "LastUpdateUtc": "2025-09-08T10:47:03.877154Z"
    },
    {
      "GUID": "c18aba31-117d-4323-9ecc-d6500f73bdb7",
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "NodeGUID": "00000000-0000-0000-0000-000000000000",
      "Label": "test",
      "CreatedUtc": "2025-09-08T10:46:32.767393Z",
      "LastUpdateUtc": "2025-09-08T10:46:32.767397Z"
    }
  ]
}
```

<br />

## Best Practices

When reading and enumerating labels, consider the following recommendations:

* **Use Appropriate Endpoints**: Choose the right endpoint based on your needs (individual read vs. enumeration vs. search)
* **Implement Pagination**: Use MaxResults and ContinuationToken for large datasets to avoid memory issues
* **Optimize Queries**: Use specific GUIDs when possible instead of reading all labels
* **Cache Results**: Implement caching for frequently accessed label data
* **Handle Errors**: Implement proper error handling for network issues and invalid GUIDs
* **Monitor Performance**: Track response times and optimize queries for better performance
* **Use Search Filters**: Leverage search parameters to reduce data transfer and improve relevance
