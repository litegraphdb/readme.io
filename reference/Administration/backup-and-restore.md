---
title: Backup and Restore
excerpt: Manage point-in-time independent copies of your LiteGraph deployment with comprehensive backup operations, restore procedures, and data protection strategies.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Backup and Restore system provides essential data protection capabilities for your LiteGraph deployment. These operations enable you to create point-in-time snapshots of your entire database, manage backup files, and restore your system to previous states when needed.

Key capabilities include:

- Creating point-in-time database backups with custom filenames
- Listing and managing existing backup files
- Reading backup metadata and information
- Checking backup file existence and status
- Deleting old or unnecessary backup files
- Restoring the entire database from backup files
- Implementing comprehensive data protection strategies

## Create a Backup

Create a point-in-time snapshot of your entire LiteGraph database with `POST: v1.0/backups`. This operation captures the complete state of your database at the moment of backup creation, including all graphs, nodes, edges, users, tenants, and associated data.

### Request Parameters

- **Filename**: The name for the backup file (e.g., "backup-2025.db", "daily-backup.db")

```bash
curl -X POST -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     -d '{"Filename": "backup-2025.db"}' \
     http://localhost:8701/v1.0/backups
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createBackup = async () => {
  try {
    const data = await api.Backup.create({
      Filename: "backup-2025.db",
    });
    console.log(data, "Backup created successfully");
  } catch (err) {
    console.log("Error creating backup:", JSON.stringify(err));
  }
};
```

## List Backups

Retrieve a comprehensive list of all available backup files with `GET: v1.0/backups`. This operation provides information about all backup files in your system, including their names, creation dates, and file sizes.

```bash
curl -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     http://localhost:8701/v1.0/backups
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllBackups = async () => {
  try {
    const data = await api.Backup.readAll();
    console.log(data, "Backups retrieved successfully");
  } catch (err) {
    console.log("Error retrieving backups:", JSON.stringify(err));
  }
};
```

## Restore from Backup

Restore your LiteGraph database from a backup file by following these steps:

1. **Stop the LiteGraph server** to ensure no data corruption during the restore process
2. **Locate your backup file** in the backup directory
3. **Replace the current `litegraph.db` file** with your backup file
4. **Restart the LiteGraph server** to load the restored database


## Read a Backup

Retrieve detailed information about a specific backup file with `GET: v1.0/backups/{filename}`. This operation provides metadata about the backup file, including its size, creation date, and other relevant information.

### Request Parameters

- **Filename**: The name of the backup file to read (e.g., "backup-2025.db")

```bash
curl -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     http://localhost:8701/v1.0/backups/backup-2025.db
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readBackup = async () => {
  try {
    const data = await api.Backup.read("backup-2025.db");
    console.log(data, "Backup information retrieved successfully");
  } catch (err) {
    console.log("Error reading backup:", JSON.stringify(err));
  }
};
```

## Delete a Backup

Remove a specific backup file from your system with `DELETE: v1.0/backups/{filename}`. This operation permanently deletes the backup file and cannot be undone, so ensure you no longer need the backup before proceeding.

### Request Parameters

- **Filename**: The name of the backup file to delete (e.g., "backup-2025.db")

```bash
curl -X DELETE -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     http://localhost:8701/v1.0/backups/backup-2025.db
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteBackup = async () => {
  try {
    const data = await api.Backup.delete("backup-2025.db");
    console.log(data, "Backup deleted successfully");
  } catch (err) {
    console.log("Error deleting backup:", JSON.stringify(err));
  }
};
```

## Check Backup Existence

Verify whether a specific backup file exists in your system with `HEAD: v1.0/backups/{filename}`. This operation returns a simple status indicating whether the backup file is available without returning the file contents.

### Request Parameters

- **Filename**: The name of the backup file to check (e.g., "backup-2025.db")

```bash
curl -I -H "Authorization: Bearer litegraphadmin" \
     http://localhost:8701/v1.0/backups/backup-2025.db
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const existsBackup = async () => {
  try {
    const data = await api.Backup.exists("backup-2025.db");
    console.log(data, "Backup existence checked successfully");
  } catch (err) {
    console.log("Error checking backup existence:", JSON.stringify(err));
  }
};
```

## Best Practices

When managing backups and restore operations, consider the following recommendations:

- **Regular Backup Schedule**: Implement automated daily or weekly backup creation
- **Backup Verification**: Always verify backup file integrity before relying on them
- **Retention Policy**: Establish a clear backup retention policy to manage storage space
- **Testing Restores**: Regularly test restore procedures to ensure they work correctly
- **Offsite Storage**: Consider storing backups in secure, offsite locations
- **Documentation**: Maintain clear documentation of backup and restore procedures
- **Monitoring**: Implement monitoring to ensure backup operations complete successfully

## Next Steps

After setting up your backup and restore system, you can:

- Implement automated backup scheduling and management
- Set up backup monitoring and alerting systems
- Create disaster recovery procedures and documentation
- Implement backup encryption for enhanced security
- Set up backup verification and integrity checking
- Develop backup retention and cleanup automation
- Create comprehensive data protection strategies
