---
layout: post
title: "Find size of all SQL tables"
date: 2016-01-18
tags: [SQL]
reading_time: 1
---

To find all the sizes of the SQL tables on disk, run the following query. This helps locate problematic databases and identify which tables consume the most storage resources.

```sql
SELECT
    s.Name AS SchemaName,
    t.Name AS TableName,
    p.rows AS RowCounts,
    CAST(ROUND((SUM(a.total_pages) / 128.00), 2) AS NUMERIC(36, 2)) AS Total_MB,
    CAST(ROUND((SUM(a.used_pages) / 128.00), 2) AS NUMERIC(36, 2)) AS Used_MB,
    CAST(ROUND((SUM(a.total_pages) - SUM(a.used_pages)) / 128.00, 2) AS NUMERIC(36, 2)) AS Unused_MB
FROM sys.tables t
INNER JOIN sys.indexes i ON t.OBJECT_ID = i.object_id
INNER JOIN sys.partitions p ON i.object_id = p.OBJECT_ID AND i.index_id = p.index_id
INNER JOIN sys.allocation_units a ON p.partition_id = a.container_id
INNER JOIN sys.schemas s ON t.schema_id = s.schema_id
WHERE t.NAME NOT LIKE 'dt%'
    AND t.is_ms_shipped = 0
    AND i.OBJECT_ID > 255
GROUP BY t.Name, s.Name, p.Rows
ORDER BY t.Name
```

This query joins multiple system tables to calculate table name, schema name, row counts, total space in KB, used space in KB, and unused space in KB.
