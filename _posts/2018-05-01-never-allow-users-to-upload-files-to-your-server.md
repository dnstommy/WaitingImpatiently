---
layout: post
title: "How to stop editors from uploading media directly to the server file system"
date: 2018-05-01
tags: [Sitecore, SQL]
featured: true
reading_time: 2
---

The core issue addressed is that Sitecore permits users to upload media files directly to server storage rather than the database. While this approach appeals to SQL administrators seeking to maintain database efficiency, it creates operational challenges when managing file distribution across multiple servers.

## The Problem

By default, Sitecore includes the `Media.UploadAsFiles` setting. When enabled, new media files are stored on disk rather than in the database, identifiable by physical file paths. However, this creates a critical vulnerability: the bulk upload dialog includes a checkbox allowing users to select "upload as files" even when administrators prefer database storage.

## The Solution

To prevent users from having this option available, implement this configuration setting across all projects:

```xml
<setting name="Upload.UserSelectableDestination" value="false"/>
```

This removes the checkbox entirely from the interface, preventing accidental disk uploads.

## Strategic Perspective

Server storage is increasingly inexpensive, making the traditional argument for disk storage obsolete. For organizations managing large media libraries, implementing a DAM (Digital Asset Management) system or CDN represents a superior approach. Database-stored media offers better disaster recovery capabilities—if a server fails, media remains intact and recoverable.

Without this preventative configuration, missing images and documents on production sites become an operational risk.
