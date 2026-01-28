---
layout: post
title: "Getting Sitecore out of SQL"
date: 2016-01-18
tags: [Sitecore, SQL]
reading_time: 1
---

Accessing Sitecore data directly through SQL queries has limitations compared to using Sitecore's native API. Direct database queries bypass the caching mechanisms built into the platform.

## Practical SQL Examples

### Retrieving Items by Parent ID

```sql
SELECT
    ID,
    Name,
    TemplateID,
    Created,
    Updated
FROM Items
WHERE ParentID = '{YOUR-PARENT-ID}'
```

### Fetching Child Items

Use the same query structure, filtering the Items table by ParentID.

### Accessing Versioned Field Data

A more complex join query combining the VersionedFields and Items tables retrieves field values, language settings, and version history:

```sql
SELECT
    i.Name,
    f.Value,
    f.Language,
    f.Version
FROM VersionedFields f
INNER JOIN Items i ON f.ItemId = i.ID
WHERE f.ItemId = '{YOUR-ITEM-ID}'
```

## Important Note

Getting Sitecore data via SQL is not always faster than using the API. I recommend reserving SQL queries primarily for integration scenarios rather than regular application development.
