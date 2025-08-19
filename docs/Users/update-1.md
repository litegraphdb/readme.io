---
title: Update
excerpt: Update existing user.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing user call `PUT: /v1.0/tenants/{tenant-guid}/users/{user-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer ********' \
--data-raw '{
    "FirstName": "Again Updated",
    "LastName": "User",
    "Email": "anotherbbb@user.com",
    "Password": "password",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const updateUser = async () => {
  try {
    const data = await api.User.update({
      GUID: '8ac86e7e-5612-4193-95d6-2f217dbaeedf',
      FirstName: 'Again Updated',
      LastName: 'User',
      Email: 'anotherbbb@user.com',
      Password: 'password',
      Active: true,
      CreatedUtc: '2024-12-27T18:12:38.653402Z',
      LastUpdateUtc: '2024-12-27T18:12:38.653402Z',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```