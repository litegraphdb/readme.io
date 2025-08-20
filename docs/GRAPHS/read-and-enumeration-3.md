---
title: Read and Enumeration
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read

Read a single graph: `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getGraphById = async () => {
  try {
    const data = await api.Graph.read(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Read graph stats

To read a single graph call `GET:/v1.0/tenants/{tenant-id}/graphs/{graph-guid}/stats `

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/stats' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readGraphStatistic = async () => {
  try {
    const data = await api.Graph.readStatistic(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Read by GUIDs

Read a multiple graph: `/v1.0/tenants/{tenant-id}/graphs?guids=<tenant1-guid>,<tenant2-guid>`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs?guids=00000000-0000-0000-0000-000000000000%2C00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readManyTenants = async () => {
  try {
    const data = await api.Tenant.readMany([tenantGuid]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Read all

To read all graphs call `GET:/v1.0/tenants/{tenant-id}/graphs `

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getGraphList = async () => {
  try {
    const data = await api.Graph.readAll();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```

## Read all tenant stats

To read all tenants call `GET:/v1.0/tenants/stats `

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants/stats' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readAllTenantStatistics = async () => {
  try {
    const data = await api.Tenant.readStatistics();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Enumeration (GET)

Enumeration via `GET:/v2.0/tenants` allows to enumerate response

```curl
curl --location 'http://view.homedns.org:8701/v2.0/tenants' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateTenants = async () => {
  try {
    const data = await api.Tenant.enumerate();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

### Response

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-08-14T13:40:37.667042Z",
        "End": "2025-08-14T13:40:37.676703Z",
        "TotalMs": 9.66,
        "Messages": {}
    },
    "MaxResults": 1000,
    "EndOfResults": true,
    "TotalRecords": 1,
    "RecordsRemaining": 0,
    "Objects": [
        {
            "GUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Default tenant",
            "Active": true,
            "CreatedUtc": "2025-01-20T02:51:11.325726Z",
            "LastUpdateUtc": "2025-01-20T02:51:11.325727Z"
        }
    ]
}
```

## Enumeration and search (POST)

Enumeration via `POST :/v2.0/tenants` allows to enumerate and search response

```curl
curl --location 'http://view.homedns.org:8701/v2.0/tenants' \
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
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateAndSearchTenants = async () => {
  try {
    const data = await api.Tenant.enumerateAndSearch({
      Ordering: 'CreatedDescending',
      IncludeData: false,
      IncludeSubordinates: false,
      MaxResults: 5,
      ContinuationToken: null,
      Labels: [],
      Tags: {},
      Expr: {},
    });
    console.log(data);
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};


```