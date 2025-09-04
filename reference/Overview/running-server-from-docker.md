---
title: Running Server from Docker
excerpt: This guide explains how to run LiteGraph Server using Docker containers.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Docker Hub

The official LiteGraph Docker image is available at:

* Docker Hub: [https://hub.docker.com/r/jchristn/litegraph](https://hub.docker.com/r/jchristn/litegraph)
* Repository: [https://github.com/litegraphdb/LiteGraph](https://github.com/litegraphdb/LiteGraph)

## Prerequisites

* Docker installed and running
* Docker Compose (optional, for compose deployment)
* Basic understanding of Docker volumes and networking

## Quick Start with Docker Run

### Basic Run Command

```bash
docker run -d \
  -p 8701:8701 \
  -v $(pwd)/litegraph.json:/app/litegraph.json \
  -v $(pwd)/litegraph.db:/app/litegraph.db \
  jchristn/litegraph:v4.0.0
```

### Interactive Mode with Full Persistence

```bash
docker run \
  -p 8701:8701 \
  -t \
  -i \
  -e "TERM=xterm-256color" \
  -v ./litegraph.json:/app/litegraph.json \
  -v ./litegraph.db:/app/litegraph.db \
  -v ./logs/:/app/logs/ \
  -v ./backups/:/app/backups/ \
  jchristn/litegraph:v4.0.0
```

## Using the Provided Scripts

LiteGraph includes helper scripts for running the container:

### Linux/macOS (run.sh)

```bash
# Run with default tag (v3.1.0)
./run.sh

# Run with specific tag
IMG_TAG=v4.1.0 ./run.sh
```

### Windows (run.bat)

```batch
REM Run with specific tag
run.bat v4.1.0
```

## Docker Compose Deployment

### Using Docker Compose

The repository includes a `compose.yaml` file for easy deployment:

```yaml
services:
  litegraph:
    container_name: 'litegraph'
    image: 'jchristn/litegraph:v4.1.0'
    network_mode: 'host'
    stdin_open: true
    tty: true
    volumes:
      - ./litegraph.json:/app/litegraph.json
      - ./litegraph.db:/app/litegraph.db
      - ./logs/:/app/logs/
      - ./backups/:/app/backups/
    healthcheck:
      test: curl --fail http://localhost:8701
```

### Start with Docker Compose

**Linux/macOS:**

```bash
./compose-up.sh
```

**Windows:**

```batch
compose-up.bat
```

Or manually:

```bash
docker compose -f compose.yaml up -d
```

### Stop with Docker Compose

**Linux/macOS:**

```bash
./compose-down.sh
```

**Windows:**

```batch
compose-down.bat
```

Or manually:

```bash
docker compose -f compose.yaml down
```

## Volume Mounts

LiteGraph requires several volumes for persistence:

| Local Path         | Container Path        | Purpose            |
| ------------------ | --------------------- | ------------------ |
| `./litegraph.json` | `/app/litegraph.json` | Configuration file |
| `./litegraph.db`   | `/app/litegraph.db`   | SQLite database    |
| `./logs/`          | `/app/logs/`          | Log files          |
| `./backups/`       | `/app/backups/`       | Database backups   |

**Important:** Ensure these files/directories exist before running the container, especially `litegraph.json`.

## Initial Setup

### 1. Create Configuration File

If you don't have a `litegraph.json` file, create one, or refer to the default `litegraph.json` in the `docker` folder in the Github repository:

```json
{
  "Logging": {
    "ConsoleLogging": true,
    "LogDirectory": "./logs/",
    "LogFilename": "litegraph.log"
  },
  "Rest": {
    "Hostname": "*",
    "Port": 8701
  },
  "LiteGraph": {
    "AdminBearerToken": "litegraphadmin",
    "GraphRepositoryFilename": "litegraph.db",
    "InMemory": false
  }
}
```

### 2. First Run

On first run with a new database, the container will create default records:

* Default tenant: `00000000-0000-0000-0000-000000000000`
* Default user: `default@user.com` / `password`
* Default credential bearer token: `default`
* Default graph: `00000000-0000-0000-0000-000000000000`

## Networking Options

### Host Network Mode (Default in compose.yaml)

```yaml
network_mode: 'host'
```

The container uses the host's network directly. Access at `http://localhost:8701`.

### Bridge Network Mode

```bash
docker run -d \
  -p 8701:8701 \
  jchristn/litegraph:v4.0.0
```

Maps container port 8701 to host port 8701.

### Custom Port Mapping

```bash
docker run -d \
  -p 9000:8701 \
  jchristn/litegraph:v4.0.0
```

Access at `http://localhost:9000`.

## Health Checks

The Docker Compose configuration includes a health check:

```yaml
healthcheck:
  test: curl --fail http://localhost:8701
```

Check container health:

```bash
docker ps
docker inspect litegraph --format='{{.State.Health.Status}}'
```

## Container Management

### View Logs

```bash
# Follow logs
docker logs -f litegraph

# Last 100 lines
docker logs --tail 100 litegraph
```

### Access Container Shell

```bash
docker exec -it litegraph /bin/bash
```

### Stop Container

```bash
docker stop litegraph
```

### Remove Container

```bash
docker rm litegraph
```

## Environment Variables

The container respects environment variables for configuration:

```bash
docker run -d \
  -e TERM=xterm-256color \
  -p 8701:8701 \
  jchristn/litegraph:v4.0.0
```

## Updating the Image

### Pull Latest Version

```bash
docker pull jchristn/litegraph:v4.1.0
```

### Update Running Container

1. Stop and remove the existing container:

```bash
docker stop litegraph
docker rm litegraph
```

2. Run with the new image:

```bash
docker run -d \
  -p 8701:8701 \
  -v $(pwd)/litegraph.json:/app/litegraph.json \
  -v $(pwd)/litegraph.db:/app/litegraph.db \
  jchristn/litegraph:v4.1.0
```

## Production Considerations

### Data Persistence

Always mount volumes for:

* Configuration (`litegraph.json`)
* Database (`litegraph.db`)
* Logs (`./logs/`)
* Backups (`./backups/`)

## Troubleshooting

### Container Won't Start

Check logs:

```bash
docker logs litegraph
```

Verify volume mounts:

```bash
ls -la litegraph.json litegraph.db
```

### Cannot Access from Host

Verify port mapping:

```bash
docker port litegraph
```

Check if service is running:

```bash
docker exec litegraph curl -I http://localhost:8701
```

### Permission Issues

Ensure proper file permissions:

```bash
chmod 644 litegraph.json
chmod 644 litegraph.db
chmod 755 logs/ backups/
```

### Database Locked

If database is locked, stop all containers accessing it:

```bash
docker stop litegraph
# Wait a moment
docker start litegraph
```

## Testing the Deployment

### Health Check

```bash
curl -I http://localhost:8701/
```

### API Test with Default Credentials

```bash
curl -H "Authorization: Bearer default" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

### Create Test Data

```
curl -X PUT \
     -H "Authorization: Bearer default" \
     -H "Content-Type: application/json" \
     -d '{"Name": "Docker Test Node"}' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes
```

<br />
