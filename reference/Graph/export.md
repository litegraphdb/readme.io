---
title: Export Graph
excerpt: >-
  Export graphs to GEXF (Graph Exchange XML Format) for visualization, analysis,
  and data portability with optional data inclusion.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Graph Export endpoint allows you to export graphs in GEXF (Graph Exchange XML Format), a standard format for representing graphs and networks. This functionality is particularly useful for:

- Visualizing graphs in external tools like Gephi, Cytoscape, or NetworkX
- Creating backups of graph data in a portable format
- Sharing graph structures with other systems or collaborators
- Performing offline analysis and processing
- Migrating graph data between different platforms

## Export Graph to GEXF

Export a graph to GEXF format using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/export/gexf`. The exported GEXF string contains all nodes, edges, and their associated metadata in a standardized XML format.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/export/gexf?incldata=null' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const exportGraphToGexf = async () => {
  try {
    const data = await api.Graph.exportGexf("<graph-guid>");
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    access_key="******",
)

def export_gexf():
    gexf = litegraph.Graph.export_gexf(graph_id="graph-guid")
    print(gexf)

export_gexf()
```

## Export Parameters

The export endpoint supports the following query parameters:

- **incldata**: Include custom data fields in the exported GEXF (optional)
  - `incldata=true`: Include all custom data properties
  - `incldata=false` or omitted: Exclude custom data properties

## Response

Upon successful export, the API returns a `200 OK` status with the GEXF XML string in the response body. The GEXF format includes:

- **Graph metadata**: Name, description, and creation information
- **Nodes**: All nodes with their properties, labels, and attributes
- **Edges**: All relationships with their properties and weights
- **Attributes**: Custom attributes and data fields (if incldata=true)
- **XML structure**: Standard GEXF XML format for compatibility

```xml
<?xml version="1.0" encoding="utf-8"?>
<gexf xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xsi:schemaLocation="http://www.gexf.net/1.3 http://www.gexf.net/1.3/gexf.xsd" version="1.3" xmlns="http://www.gexf.net/1.3">
    <meta lastmodifieddate="2025-09-08T10:14:05.3162871Z">
        <creator>LiteGraph</creator>
        <description>Graph from LiteGraph https://github.com/jchristn/litegraph</description>
    </meta>
    <graph defaultedgetype="directed">
        <attributes class="node">
            <attribute id="0" title="props" type="string" />
        </attributes>
        <nodes />
        <edges />
    </graph>
</gexf>
```

<br />

## Best Practices

When exporting graphs, consider the following recommendations:

1. **Data Inclusion**: Use `incldata=true` only when custom data is needed for analysis
2. **Large Graphs**: Be aware that large graphs may generate substantial GEXF files
3. **Format Validation**: Validate the exported GEXF format before importing into other tools
4. **Backup Strategy**: Use exports as part of your data backup and recovery strategy
5. **Version Control**: Consider versioning exported graphs for change tracking

## Next Steps

After exporting a graph to GEXF format, you can:

- Import the GEXF file into visualization tools like Gephi or Cytoscape
- Use the exported data for offline analysis and processing
- Share the graph structure with collaborators or external systems
- Create backups of your graph data in a portable format
- Migrate graph data to other platforms that support GEXF format
