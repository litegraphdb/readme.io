---
title: In-Memory Operation
excerpt: >-
  LiteGraph allows you to run the database entirely in memory for
  high-performance, low-latency scenarios with advanced memory management and data persistence strategies.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

In-Memory Operation mode enables LiteGraph to run entirely in system memory, providing exceptional performance and ultra-low latency for high-throughput scenarios. This mode is ideal for applications requiring maximum speed, real-time processing, and temporary data storage with optional persistence capabilities.

Key benefits include:

- **Ultra-High Performance**: Maximum speed with data stored in RAM
- **Low Latency**: Minimal response times for all operations
- **Real-Time Processing**: Ideal for streaming and real-time applications
- **Temporary Storage**: Perfect for caching and session management
- **Optional Persistence**: Manual control over data persistence to disk
- **Memory Management**: Efficient memory usage and garbage collection
- **Scalability**: Enhanced performance for high-concurrency scenarios

## Configuration

For high-performance scenarios, run the database entirely in memory by configuring the following settings:

### Enable In-Memory Mode

**Configure In-Memory Operation**: Set `InMemory` to `true` in your `litegraph.json` configuration file:
   ```json
   {
     "LiteGraph": {
       "InMemory": true,
     }
   }
   ```


### Manual Flush to Disk

**Important**: When running in-memory mode, data is stored only in RAM by default. You must manually flush data to disk to ensure persistence:

```bash
curl -X POST -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     http://localhost:8701/v1.0/flush
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const flushToDisk = async () => {
  try {
    const data = await api.Admin.flush();
    console.log(data, "Data flushed to disk successfully");
  } catch (err) {
    console.log("Error flushing data:", JSON.stringify(err));
  }
};
```

## Performance Considerations

### Memory Usage

- **RAM Requirements**: Ensure sufficient system memory for your dataset
- **Memory Monitoring**: Monitor memory usage to prevent system overload
- **Data Size Limits**: Consider dataset size relative to available RAM
- **Concurrent Operations**: In-memory mode handles high concurrency efficiently

### Use Cases

**Ideal for:**
- Real-time analytics and reporting
- High-frequency trading systems
- Session management and caching
- Temporary data processing
- Development and testing environments
- High-throughput API services

**Not recommended for:**
- Large datasets exceeding available RAM
- Long-term data storage without persistence
- Systems with limited memory resources
- Production environments requiring automatic persistence

## Best Practices

When using in-memory operation mode, consider the following recommendations:

- **Memory Monitoring**: Implement monitoring to track memory usage and prevent overflow
- **Regular Flushing**: Establish a schedule for regular data flushing to disk
- **Backup Strategy**: Create backups before critical operations or system restarts
- **Error Handling**: Implement proper error handling for memory-related issues
- **Resource Planning**: Plan memory allocation based on expected data volumes
- **Testing**: Thoroughly test in-memory operations in your specific environment
- **Documentation**: Document flush procedures and memory management strategies

## Next Steps

After configuring in-memory operation, you can:

- Implement automated flush scheduling and management
- Set up memory monitoring and alerting systems
- Create data persistence strategies and procedures
- Optimize memory usage and garbage collection settings
- Develop backup and recovery procedures for in-memory data
- Implement performance monitoring and optimization
- Create comprehensive memory management documentation
