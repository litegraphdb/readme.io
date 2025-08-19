---
title: Read
excerpt: Read and read all tenants.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read

To read a single tenant call `GET:/v1.0/tenants/{{tenant-id}} `

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
const readTenant = async () => {
  try {
    const data = await api.Tenant.read('00000000-0000-0000-0000-000000000000');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```