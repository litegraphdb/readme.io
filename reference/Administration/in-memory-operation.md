---
title: In-Memory Operation
excerpt: >-
  LiteGraph allows you to run the database entirely in memory for
  high-performance, low-latency scenarios.  
deprecated: false
hidden: false
metadata:
  robots: index
---
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
