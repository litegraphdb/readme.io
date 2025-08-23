---
title: LiteGraph Overview
excerpt: >-
  LiteGraph is a property graph database with support for graph relationships,
  tags, labels, metadata, data, and vectors. LiteGraph is intended to be a
  unified database for providing persistence and retrieval for knowledge and
  artificial intelligence applications.
hidden: false
---
# What is LiteGraph?

LiteGraph is a property graph database with support for graph relationships, tags, labels, metadata, data, and vectors. LiteGraph is intended to be a unified database for providing persistence and retrieval for knowledge and artificial intelligence applications. 

LiteGraph provides a lightweight yet powerful solution that combines the best of multiple database paradigms - graph databases for relationship modeling, vector databases for AI/ML embeddings, and document stores for flexible metadata storage.

# Key Features

* **Multi-modal Database**: Supports graph structures, relational data, vectors, and metadata in a single system
* **Property Graph Model**: Full support for nodes, edges, labels, tags, and custom data properties
* **Vector Support**: Native vector storage and similarity search capabilities for AI applications
* **Flexible Deployment**: Can be run in-process (using LiteGraphClient) or as a standalone RESTful server (using LiteGraph.Server)
* **In-Memory Operation**: Optional in-memory mode with controlled flushing to disk
* **Multi-tenancy**: Built-in support for multiple tenants and graph isolation
* **Export Capabilities**: Export graphs to GEXF format for visualization
* **No Dependencies**: Leverages SQLite for a zero-configuration embedded database

# Use Cases

## Knowledge Management

* Build knowledge graphs for organizing complex information
* Create semantic networks for content relationships
* Implement recommendation systems based on graph traversal

## Artificial Intelligence Applications

* Store and query vector embeddings from LLMs
* Build RAG (Retrieval-Augmented Generation) systems
* Implement similarity search for semantic content matching
* Create hybrid search combining graph relationships and vector similarity

## Application Development

* Embed a graph database directly into applications without external dependencies
* Build networks with detailed, rich relationships
* Model organizational hierarchies and permissions
* Track dependencies and relationships in complex systems

## Research and Analysis

* Network analysis and graph algorithms
* Pattern detection in connected data
* Path finding and route optimization
* Community detection and clustering

# Comparing LiteGraph

## vs Traditional Relational Databases

* **Native Graph Support**: First-class support for nodes, edges, and graph traversal
* **Flexible Schema**: No rigid table structures; properties can be added dynamically
* **Relationship-Centric: Optimized** for querying connected data rather than tabular data
* **Multi-modal**: Combines relational, graph, and vector capabilities

## vs Vector Databases

* **Graph Context**: Vectors are enriched with graph relationships and metadata
* **Unified Storage**: No need for separate graph and vector databases
* **Flexible Filtering**: Use labels, tags, and expressions (data filters) when performing a vector search
* **Lightweight**: Built on SQLite rather than requiring specialized infrastructure

## vs Metadata/Feature Stores

* **Relationship Modeling**: Goes beyond key-value storage to model complex relationships
* **Type Flexibility**: The Data property is an object and can be attached to any Graph, Node, or Edge. Data supports any object serializable to JSON
* **Built-in Search**: Native support for graph traversal and vector similarity search
* **Version History**: Timestamps for creation and updates on all entities

## vs Traditional Graph Databases

* **Embedded Operation**: No separate server required; runs in-process with your application
* **SQLite Foundation**: Leverages proven SQLite reliability and performance
* **Vector Integration**: Native vector support without extensions or plugins
* **Simplified Deployment**: Single file database with no complex configuration

# Getting Started

## Install via NuGet:

`dotnet add package LiteGraph`

## Basic Usage

```Text csharp
using LiteGraph;

LiteGraphClient graph = new LiteGraphClient(new SqliteRepository("litegraph.db"));
graph.InitializeRepository();

// Create a tenant
TenantMetadata tenant = graph.CreateTenant(new TenantMetadata { Name = "My tenant" });

// Create a graph
Graph graph = graph.CreateGraph(new Graph { TenantGUID = tenant.GUID, Name = "This is my graph!" });

// Create nodes
Node node1 = graph.CreateNode(new Node { TenantGUID = tenant.GUID, GraphGUID = graph.GUID, Name = "node1" });
Node node2 = graph.CreateNode(new Node { TenantGUID = tenant.GUID, GraphGUID = graph.GUID, Name = "node2" });
Node node3 = graph.CreateNode(new Node { TenantGUID = tenant.GUID, GraphGUID = graph.GUID, Name = "node3" });

// Create edges
Edge edge1 = graph.CreateEdge(new Edge { TenantGUID = tenant.GUID, GraphGUID = graph.GUID, From = node1.GUID, To = node2.GUID, Name = "Node 1 to node 2" });
Edge edge2 = graph.CreateEdge(new Edge { TenantGUID = tenant.GUID, GraphGUID = graph.GUID, From = node2.GUID, To = node3.GUID, Name = "Node 2 to node 3" });

// Find routes
foreach (RouteDetail route in graph.GetRoutes(
	SearchTypeEnum.DepthFirstSearch,
  tenant.GUID,
	graph.GUID,
	node1.GUID,
	node2.GUID))
{
  Console.WriteLine(...);
}
```

## Getting Started with Docker

Using Docker Hub Image
A Docker image is available in Docker Hub under jchristn/litegraph.

### Quick Start with Docker Compose

Navigate to the Docker directory in the repository
Use the Docker Compose start (`compose-up.sh` and `compose-up.bat`) and stop (`compose-down.sh` and `compose-down.bat`) scripts

### Manual Docker Setup

`docker pull jchristn/litegraph`

### Run with volume mounts for database and configuration

```
docker run -d \
-p 8701:8701 \
-v /path/to/litegraph.db:/app/litegraph.db \
-v /path/to/litegraph.json:/app/litegraph.json \
jchristn/litegraph
```

Ensure that you have a valid database file (e.g. `litegraph.db`) and configuration file (e.g. `litegraph.json`) exposed into your container.

## REST API Server

By default, `LiteGraph.Server` (and by consequence, the Docker image) listens on [http://localhost:8701](http://localhost:8701) and is only accessible to localhost. Modify the `litegraph.json` file to change settings including hostname and port.
