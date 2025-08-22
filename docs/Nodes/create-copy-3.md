---
title: Create
excerpt: Create node.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Create single node

To create single node call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My test node",
    "Labels": [
        "test",
        "hello"
    ],
    "Tags": {
        "Foo": "Bar",
        "Bar": "Baz"
    },
    "Data": {
        "Hello": "World",
        "Foo": {
            "Data": "hello"
        }
    },
    "Vectors": [
        {
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [ 0.1, 0.2, 0.3 ]
        }
    ]
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createNode = async () => {
  // Node object to create
  const node = {
    GUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
    GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
    Name: 'Sample Node',
    Data: {
      key1: 'value2',
    },
    CreatedUtc: '2024-10-19T14:35:20.351Z',
  };
  try {
    const createdNode = await api.Node.create(node);
    console.log(createdNode, 'Node created successfully');
  } catch (err) {
    console.log('err: ', err);
    console.log('Error creating node:', JSON.stringify(err));
  }
};

```

## Create multiple node

To create multiple node call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    {
        "Name": "Active Directory",
        "Labels": [
            "test"
        ],
        "Tags": {
            "Type": "ActiveDirectory"
        },
        "Data": {
            "Name": "Active Directory"
        }
    },
    {
        "Name": "Website",
        "Labels": [
            "test"
        ],
        "Tags": {
            "Type": "Website"
        },
        "Data": {
            "Name": "Website"
        }
    }
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';
import { NodeCreateRequest} from 'litegraphdb/dist/types/types';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const crateMultipleNodes = async () => {
  const newMultipleNodes: NodeCreateRequest[] = [
    {
      Name: 'Active Directory',
      Labels: ['test'],
      Tags: {
        Type: 'ActiveDirectory',
      },
      Data: {
        Name: 'Active Directory',
      },
      GraphGUID: '8e72e2b7-86fe-4f94-8483-547c23c8a833',
    },
    {
      Name: 'Website',
      Labels: ['test'],
      Tags: {
        Type: 'Website',
      },
      Data: {
        Name: 'Website',
      },
      GraphGUID: '8e72e2b7-86fe-4f94-8483-547c23c8a833',
    },
  ];

  try {
    const createdNode = await api.Node.createBulk(guid, newMultipleNodes);
    console.log(createdNode, 'Node created successfully');
  } catch (err) {
    console.log('err: ', err);
    console.log('Error creating node:', JSON.stringify(err));
  }
};

```