---
title: Read and Enumeration
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read

Read a single user: `GET: /v1.0/tenants/{tenant-guid}/users/{user-guid}`

```curl
curl --location --request GET 'http://view.homedns.org:8701/v1.0/tenants/<Tenant-GUID>' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readUser = async () => {
  try {
    const data = await api.User.read('199eb859-5857-4313-b487-5b0a5fb2abf8');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Read all

To read all tenants call `GET:/v1.0/tenants/{tenant-guid}/users/ `

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readAllUsers = async () => {
  try {
    const data = await api.User.readAll();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Enumeration (GET)

Enumeration via `GET:/v2.0/tenants/{tenant-guid}/users/` allows to enumerate response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/users' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateUsers = async () => {
  try {
    const data = await api.User.enumerate();
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

Enumeration via `POST :/v2.0/tenants/{tenant-guid}/users/` allows to enumerate and search response

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