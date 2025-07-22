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

# 📈 Know your users

One of the best ways to know if you're nailing the dev experience is checking out how your users are interacting with both your docs and API.

* **Documentation Metrics** let you see who's using your docs, what your best and worst pages are, what people are searching for and more!
* **API Metrics** are a bit harder to set up (I promise we do our best to make it painless!), but once you set this up you'll know *everything* that's going on with your users!

# 💬 We're here to help!

ReadMe has a *ton* of ways to make your docs the envy of any <Glossary>parliament</Glossary> (like that mouseover!). If you get stuck, [shoot us an email](mailto:support@readme.io) or use the Intercom widget on the bottom right of any page.

We're excited you're here! :blue_heart:

![This won't be fun to clean up...](https://owlbert.io/images/popper.gif)