---
title: Backup and Restore
excerpt: Manage point-in-time independent copies of your LiteGraph deployment.
deprecated: false
hidden: false
metadata:
  robots: index
---
### Create a Backup

```bash
curl -X POST -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     -d '{"Filename": "backup-2025.db"}' \
     http://localhost:8701/v1.0/backups
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const createBackup = async () => {
  try {
    const data = await api.Backup.create({
      Filename: 'test2.db',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### List Backups

```bash
curl -H "Authorization: Bearer litegraphadmin" \
 		 -H "Content-Type: application/json" \
     -d '{"Filename": "backup-2025.db"}' \
     http://localhost:8701/v1.0/backups
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const readAllBackups = async () => {
  try {
    const data = await api.Backup.readAll();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Restore from Backup

Stop the server, replace the `litegraph.db` file with your backup, then restart.

### Read a Backup

```bash
curl -H "Authorization: Bearer litegraphadmin" \
 		 -H "Content-Type: application/json" \
     -d '{"Filename": "backup-2025.db"}' \
     http://localhost:8701/v1.0/backups
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const readBackup = async () => {
  try {
    const data = await api.Backup.read('my-backup.db');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Delete a Backup

```bash
curl -H "Authorization: Bearer litegraphadmin" \
 		 -H "Content-Type: application/json" \
     -d '{"Filename": "backup-2025.db"}' \
     http://localhost:8701/v1.0/backups
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const deleteBackup = async () => {
  try {
    const data = await api.Backup.delete('my-backup.db');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Exist

```bash
curl -H "Authorization: Bearer litegraphadmin" \
 		 -H "Content-Type: application/json" \
     -d '{"Filename": "backup-2025.db"}' \
     http://localhost:8701/v1.0/backups
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const existsBackup = async () => {
  try {
    const data = await api.Backup.exists('my-backup.db');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
