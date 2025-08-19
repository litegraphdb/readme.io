---
title: Read and Enumeration
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read

When reading a tenant, use the following structure:

```curl
curl --location --request GET 'http://view.homedns.org:8701/v1.0/tenants/<Tenant-GUID>' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readTenant = async () => {
  try {
    const tenant = await api.Tenant.get('<Tenant-GUID>');
    console.log(tenant);
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

<br />

## Enumeration (GET)

Enumeration via `GET` allows to enumerate response

```curl
curl --location 'http://view.homedns.org:8701/v2.0/tenants' \
--header 'Authorization: Bearer litegraphadmin'
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

## Enumeration (POST)

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