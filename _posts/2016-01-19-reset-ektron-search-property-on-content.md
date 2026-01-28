---
layout: post
title: "Reset Ektron Search Property on Content"
date: 2016-01-19
tags: [Ektron, SQL]
reading_time: 1
---

This article addresses a limitation in Ektron's content management system. When administrators modify the searchability checkbox on a folder, the change applies only to newly created content. Previously existing items retain their original searchable status.

## The Solution

To resolve this inconsistency, use a SQL solution that updates all existing content within folders to inherit the parent folder's search property setting.

```sql
DECLARE @folderid BIGINT
DECLARE @searchable INT

DECLARE folder_cursor CURSOR FAST_FORWARD FOR
    SELECT folder_id, Searchable
    FROM content_folder_tbl

OPEN folder_cursor
FETCH NEXT FROM folder_cursor INTO @folderid, @searchable

WHILE @@FETCH_STATUS = 0
BEGIN
    UPDATE content_tbl
    SET searchable = @searchable
    WHERE folder_id = @folderid

    FETCH NEXT FROM folder_cursor INTO @folderid, @searchable
END

CLOSE folder_cursor
DEALLOCATE folder_cursor
```

This script systematically applies the parent folder's setting to legacy content that wasn't affected by the initial checkbox modification.
