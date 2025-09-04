---
title: Create
excerpt: Create label.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Create single label

To create single label call `PUT: /v1.0/tenants/{tenant-guid}/labels`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label"
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createLabel = async () => {
  try {
    const data = await api.Label.create({
      GraphGUID: '<graph-guid>',
      NodeGUID: '<node-guid>',
      Label: 'test',
      EdgeGUID: null,
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Create multiple label

To create multiple label call `PUT: /v1.0/tenants/{tenant-guid}/labels/bulk`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
  {
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label"
  }
]''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createMultipleLabels = async () => {
  try {
    const data = await api.Label.createBulk([
      {
        GraphGUID: '<graph-guid>',
        NodeGUID: '<node-guid>',
        EdgeGUID: '<edge-guid>',
        Label: 'label multiple',
      },
      {
        GraphGUID: '<graph-guid>',
        NodeGUID: '<node-guid>',
        EdgeGUID: '<edge-guid>',
        Label: 'label multiple 2',
      },
    ]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```
