---
title: Running Server from Source
excerpt: >-
  This guide explains how to build and run the LiteGraph Server from source to
  deploy a RESTful API for your LiteGraph database.  ##
deprecated: false
hidden: false
metadata:
  robots: index
---
## Prerequisites

* .NET 8.0 SDK or later
* Operating system: Windows, Linux, or macOS
* Git (for cloning the repository)
* Elevated privileges (only if listening on all network interfaces)

## Building from Source

### 1. Clone the Repository

```bash
git clone https://github.com/jchristn/LiteGraph.git
cd LiteGraph/src
```

### 2. Build the Server Project

```bash
dotnet build LiteGraph.Server/LiteGraph.Server.csproj
```

For a release build with optimizations:

```bash
dotnet build LiteGraph.Server/LiteGraph.Server.csproj -c Release
```

### 3. Navigate to the Output Directory

Debug build:

```bash
cd LiteGraph.Server/bin/Debug/net8.0
```

Release build:

```bash
cd LiteGraph.Server/bin/Release/net8.0
```

## Running the Server

### Quick Start

```bash
dotnet LiteGraph.Server.dll
```

You should see the LiteGraph logo and startup messages:

```
  _ _ _                          _
 | (_) |_ ___ __ _ _ _ __ _ _ __| |_
 | | |  _/ -_) _` | '_/ _` | '_ \ ' \
 |_|_|\__\___\__, |_| \__,_| .__/_||_|
             |___/         |_|

 LiteGraph Server
 (c)2025 Joel Christner

Using settings file './litegraph.json'
Settings file './litegraph.json' does not exist, creating
Initializing logging
| syslog://127.0.0.1:514
Creating default records in database litegraph.db
| Created tenant     : 00000000-0000-0000-0000-000000000000
| Created user       : 00000000-0000-0000-0000-000000000000 email: default@user.com pass: password
| Created credential : 00000000-0000-0000-0000-000000000000 bearer token: default
| Created graph      : 00000000-0000-0000-0000-000000000000 Default graph
Finished creating default records
Starting REST server on http://localhost:8701/
```

### Alternative: Run Directly from Project

You can also run without explicitly building first:

```bash
cd LiteGraph.Server
dotnet run
```

For release mode:

```bash
dotnet run -c Release
```

## Initial Setup

On first run, LiteGraph Server will automatically:

1. **Create a configuration file** (`litegraph.json`) with default settings
2. **Create a database file** (`litegraph.db`)
3. **Generate default records** including:
   * Default tenant (GUID: `00000000-0000-0000-0000-000000000000`)
   * Default user (email: `default@user.com`, password: `password`)
   * Default credential (bearer token: `default`)
   * Default graph (GUID: `00000000-0000-0000-0000-000000000000`)

## Configuration

### Configuration File

The `litegraph.json` file controls all server settings. Key configurations include:

#### Server Settings

```json
{
  "Rest": {
    "Hostname": "localhost",  // Change to "*" or "0.0.0.0" for external access
    "Port": 8701              // Default port
  }
}
```

#### Database Settings

```json
{
  "LiteGraph": {
    "AdminBearerToken": "litegraphadmin",  // Admin authentication token
    "GraphRepositoryFilename": "litegraph.db",  // Database file
    "InMemory": false  // Set to true for in-memory operation
  }
}
```

#### Logging Settings

```json
{
  "Logging": {
    "ConsoleLogging": true,
    "LogDirectory": "./logs/",
    "LogFilename": "litegraph.log"
  }
}
```

## Command Line Options

### Custom Configuration File

Use a different configuration file:

```bash
dotnet LiteGraph.Server.dll --config=/path/to/config.json
```

## Environment Variables

The server checks for these environment variables on startup:

* `LITEGRAPH_PORT` - Override the REST API port (must be 0-65535)
* `LITEGRAPH_DB` - Override the database filename

Example:

```bash
export LITEGRAPH_PORT=9000
export LITEGRAPH_DB=mydata.db
dotnet LiteGraph.Server.dll
```

## Network Access

### Local Access Only (Default)

By default, the server listens on `localhost:8701` and is only accessible from the local machine.

### External Access

To allow external connections:

1. Edit `litegraph.json`:
   ```json
   {
     "Rest": {
       "Hostname": "*"  // or "0.0.0.0" or specific IP
     }
   }
   ```

2. Run with elevated privileges (required for wildcard hostname):
   * **Windows**: Run as Administrator
   * **Linux/macOS**: Use `sudo`
   ```bash
   sudo dotnet LiteGraph.Server.dll
   ```

## Authentication

LiteGraph Server supports three authentication methods:

### 1. Administrator Bearer Token

Use the admin token defined in `litegraph.json` for administrative APIs:

```bash
curl -H "Authorization: Bearer litegraphadmin" http://localhost:8701/v1.0/tenants
```

### 2. User Credentials

Use email, password, and tenant GUID:

```bash
curl -H "x-email: default@user.com" \
     -H "x-password: password" \
     -H "x-tenant-guid: 00000000-0000-0000-0000-000000000000" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

### 3. Security Token

Generate a temporal token (valid for 24 hours):

```bash
curl -H "x-email: default@user.com" \
     -H "x-password: password" \
     -H "x-tenant-guid: 00000000-0000-0000-0000-000000000000" \
     http://localhost:8701/v1.0/token
```

Then use the token:

```bash
curl -H "x-token: [generated-token]" http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

## Testing the Server

### Check Server Status

```bash
curl -I http://localhost:8701/
```

### Get All Graphs (with authentication)

```bash
curl -H "Authorization: Bearer default" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

### Create a New Node

```bash
curl -X PUT \
     -H "Authorization: Bearer default" \
     -H "Content-Type: application/json" \
     -d '{"Name": "Test Node", "Data": {"type": "example"}}' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes
```

## In-Memory Operation

For high-performance scenarios, run the database entirely in memory:

1. Set `InMemory` to `true` in `litegraph.json`:
   ```json
   {
     "LiteGraph": {
       "InMemory": true
     }
   }
   ```

2. **Important**: When running in-memory, you must manually flush data to disk:
   ```bash
   curl -X POST -H "Authorization: Bearer litegraphadmin" \
        http://localhost:8701/v1.0/flush
   ```

## Backup and Restore

### Create a Backup

```bash
curl -X POST -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     -d '{"Filename": "backup-2025.db"}' \
     http://localhost:8701/v1.0/backups
```

### List Backups

```bash
curl -H "Authorization: Bearer litegraphadmin" \
     http://localhost:8701/v1.0/backups
```

### Restore from Backup

Stop the server, replace the `litegraph.db` file with your backup, then restart.

## Troubleshooting

### Build Errors

* Ensure .NET 8.0 SDK is installed: `dotnet --version`
* Restore NuGet packages: `dotnet restore`
* Clean and rebuild: `dotnet clean` then `dotnet build`

### Server Won't Start

* Check if port 8701 is already in use: `netstat -an | grep 8701`
* Verify file permissions for database and log directories
* Check for configuration file syntax errors

### Cannot Access from External Machine

* Ensure `Hostname` is not set to `localhost` in configuration
* Check firewall settings for port 8701
* Verify the server is running with appropriate privileges
* Test with telnet: `telnet [server-ip] 8701`

### Authentication Failures

* Verify bearer token matches configuration
* Check user credentials are correct
* Ensure tenant GUID exists
* Review authentication headers are properly formatted

### Database Issues

* Check database file permissions
* Verify disk space availability
* For in-memory mode, ensure sufficient RAM
* Check database file isn't corrupted

## Performance Tuning

### Configuration Options

```json
{
  "LiteGraph": {
    "MaxConcurrentOperations": 4,  // Adjust based on CPU cores
    "InMemory": true               // For maximum performance
  },
  "Caching": {
    "Enable": true,
    "Capacity": 1000,
    "EvictCount": 100
  }
}
```

### Monitoring

Enable detailed logging for debugging:

```json
{
  "Debug": {
    "DatabaseQueries": true,
    "Requests": true,
    "Exceptions": true
  }
}
```

## API Documentation

For complete API documentation, refer to:

* `REST_API.md` - Detailed endpoint documentation
* Postman collection: `LiteGraph.postman_collection.json`

Import the Postman collection for easy API testing:

1. Open Postman
2. Import → File → Select `LiteGraph.postman_collection.json`
3. Configure variables for your environment

## Default Endpoints

Once running, the server provides RESTful endpoints at:

* Base URL: `http://localhost:8701`
* API version: `/v1.0`
* Health check: `HEAD /`
* Graphs: `/v1.0/tenants/[tenant-guid]/graphs`
* Nodes: `/v1.0/tenants/[tenant-guid]/graphs/[graph-guid]/nodes`
* Edges: `/v1.0/tenants/[tenant-guid]/graphs/[graph-guid]/edges`

## Stopping the Server

Press `Ctrl+C` to gracefully shut down the server.

**Important**: If running in-memory mode, ensure you flush data to disk before stopping:

```bash
curl -X POST -H "Authorization: Bearer litegraphadmin" http://localhost:8701/v1.0/flush
```

## Next Steps

* Review `REST_API.md` for complete API documentation
* Import and explore the Postman collection
* Configure SSL/TLS for production deployments
* Set up proper authentication tokens and remove defaults
* Configure syslog servers for centralized logging
* Implement backup strategies for your database