---
layout: post
title: "Getting multilist from SQL"
date: 2016-02-25
tags: [Sitecore, SQL]
reading_time: 1
---

A client requested to export site structure via SQL, and I encountered a challenge with multilist controls that reference other items. Since selected items for a multilist is the item IDs separated by the `|` character, I needed to traverse these relationships.

## The Solution

Create a SQL Split function to parse the pipe-delimited values:

```sql
CREATE FUNCTION dbo.Split(@String varchar(8000), @Delimiter char(1))
RETURNS @temptable TABLE (items varchar(8000))
AS
BEGIN
    DECLARE @idx int
    DECLARE @slice varchar(8000)

    SELECT @idx = 1
    IF len(@String)<1 OR @String IS NULL RETURN

    WHILE @idx != 0
    BEGIN
        SET @idx = charindex(@Delimiter, @String)
        IF @idx != 0
            SET @slice = left(@String, @idx - 1)
        ELSE
            SET @slice = @String

        IF(len(@slice) > 0)
            INSERT INTO @temptable(Items) VALUES(@slice)

        SET @String = right(@String, len(@String) - @idx)
        IF len(@String) = 0 BREAK
    END
    RETURN
END
```

This function can then be used with queries that join multilist values to related items tables for reporting purposes.
