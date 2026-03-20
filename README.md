Real-life Oracle SQL performance tuning case study on large datasets
## Oracle PL/SQL Performance Optimization – High Volume Order Processing

### Business Context
### Processing Flow (Before Optimization)

External Feed → Staging Table → Cursor Loop Processing → Sequential Sorting → Order Number Assignment → Reporting Tables

### Processing Flow (After Optimization)

External Feed → Staging Table → Set-Based Analytic Processing (RANK) → Asynchronous Trigger Handling → Fast Order Assignment → Reporting Tables
### Performance Bottleneck Analysis
Detailed analysis revealed that:

- Nearly **30 minutes were spent reading records through a cursor loop**
- Repeated function calls inside the procedure caused unnecessary context switching
- Inefficient ordering logic increased sorting overhead
- Synchronous table triggers were adding additional processing latency
- Redundant reads were executed due to procedural design limitations

### Optimization Strategy
To resolve the performance issues, the following improvements were implemented:

- Replaced cursor-based sequential processing with **analytic functions (RANK / window functions)** for bulk ordering logic
- Moved repeated procedural function calls directly into the cursor query to reduce context switching
- Eliminated redundant reads and unnecessary data fetch operations
- Refactored procedural flow to improve set-based processing efficiency
- Converted table trigger execution to **asynchronous processing** to reduce transaction wait time
- Improved SQL execution plan stability and reduced sorting overhead

### Results
- Batch processing time reduced from **~60 minutes to ~5 minutes**
- Cursor read phase reduced from **~30 minutes to a few seconds**
- Significant reduction in I/O operations and CPU utilization
- Improved batch window reliability and downstream system readiness
- Increased scalability for future growth in order volume

### Key Technologies
Oracle Database, PL/SQL, Analytic Functions (RANK), Batch Optimization, High-Volume Data Processing, Trigger Optimization
