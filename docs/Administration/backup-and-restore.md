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
```

### List Backups

```bash
curl -H "Authorization: Bearer litegraphadmin" \
     http://localhost:8701/v1.0/backups
```

### Restore from Backup

Stop the server, replace the `litegraph.db` file with your backup, then restart.