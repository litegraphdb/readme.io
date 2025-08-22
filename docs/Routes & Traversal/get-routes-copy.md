---
title: Get routes (COPY)
excerpt: Get all possible routes between two nodes.
deprecated: false
hidden: false
metadata:
  robots: index
---
To find all route between nodes call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/routes`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/routes' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "From": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
    "To": "769a880c-85b6-422e-8aa2-c6f160bd24c6"
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getRoutes = async () => {
  try {
    const data = await api.Route.getRoutes(graphGuid, fromNodeGuid, toNodeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```

### Response

```json
{
    "Timestamp": {
        "Start": "2025-08-22T12:22:07.954584Z",
        "End": "2025-08-22T12:22:07.973688Z",
        "TotalMs": 19.1,
        "Messages": {}
    },
    "Routes": [
        {
            "TotalCost": 0,
            "Edges": [
                {
                    "TenantGUID": "00000000-0000-0000-0000-000000000000",
                    "GUID": "1223b43a-701f-45d5-901c-149a69ce7a1f",
                    "GraphGUID": "00000000-0000-0000-0000-000000000000",
                    "Name": "new one3434",
                    "From": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
                    "To": "769a880c-85b6-422e-8aa2-c6f160bd24c6",
                    "Cost": 0,
                    "CreatedUtc": "2025-08-22T12:22:03.485904Z",
                    "LastUpdateUtc": "2025-08-22T12:22:03.485904Z",
                    "Data": {}
                }
            ]
        },
        {
            "TotalCost": 0,
            "Edges": [
                {
                    "TenantGUID": "00000000-0000-0000-0000-000000000000",
                    "GUID": "35dc5401-b17d-4725-abea-5b60654b1f73",
                    "GraphGUID": "00000000-0000-0000-0000-000000000000",
                    "Name": "ew",
                    "From": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
                    "To": "3e991338-d247-4811-80d6-bf54be601686",
                    "Cost": 0,
                    "CreatedUtc": "2025-08-21T13:23:27.028795Z",
                    "LastUpdateUtc": "2025-08-21T13:23:27.028795Z",
                    "Data": {}
                },
                {
                    "TenantGUID": "00000000-0000-0000-0000-000000000000",
                    "GUID": "e42ad05e-dd73-4fe8-a7a7-feeb37f67598",
                    "GraphGUID": "00000000-0000-0000-0000-000000000000",
                    "Name": "234234",
                    "From": "3e991338-d247-4811-80d6-bf54be601686",
                    "To": "769a880c-85b6-422e-8aa2-c6f160bd24c6",
                    "Cost": 0,
                    "CreatedUtc": "2025-08-21T13:22:25.419977Z",
                    "LastUpdateUtc": "2025-08-21T13:22:25.419977Z",
                    "Data": {}
                }
            ]
        }
    ]
}
```