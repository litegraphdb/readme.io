---
title: Create
excerpt: To create user object.
deprecated: false
hidden: false
metadata:
  robots: index
---
```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer litegraphadmin' \
--data-raw '{
    "FirstName": "Another",
    "LastName": "User",
    "Email": "another@user.com",
    "Password": "password",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createUser = async () => {
  try {
    const data = await api.User.create({
      FirstName: 'Another',
      LastName: 'User',
      Email: 'another@user.com',
      Password: 'password',
      Active: true,
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```