---
layout: post
title: "Working with the xConnect hex identifiers"
date: 2019-06-20
tags: [Sitecore, xConnect, SQL]
featured: true
reading_time: 2
---

This article explains how to work with hexadecimal identifiers in Sitecore 9.x xConnect shard databases. Identifiers for contacts, contact facets, interactions, and interaction facets are now stored in separate tables with hexed values, unlike the Mongo structure used in Sitecore 8.2.

I needed to find a contact ID using a known email address. In the previous version, a simple Mongo query would retrieve this information. However, in 9.x, the identifiers are encoded in hexadecimal format.

Using an online hex-to-ASCII converter, I confirmed these are standard hex characters without encryption. Here are two SQL queries to work with this data:

## Query 1: Display All Email Identifiers

This query displays all email address identifiers in readable format using a CONVERT function to decode the hexadecimal values.

```sql
SELECT CONVERT(VARCHAR(100), Identifier) as Email
FROM [xdb_collection].[ContactIdentifiers]
WHERE Source = 'email'
```

## Query 2: Find Specific Email

This query finds a specific email address by converting the search term to VARBINARY format and comparing it against the stored Identifier column.

```sql
SELECT *
FROM [xdb_collection].[ContactIdentifiers]
WHERE Identifier = CONVERT(VARBINARY(100), 'user@example.com')
```

This approach allows direct database access to retrieve contact information from the xConnect shard databases.
