---
layout: post
title: "OH NO! Sitecore hanging after iisreset"
date: 2018-09-30
tags: [Sitecore, Debugging]
featured: true
reading_time: 3
---

I encountered a critical issue where my Sitecore site became completely unresponsive for approximately 20 minutes following any IIS reset, deployment, or configuration change. During these outages, HTML and text files remained accessible, but all .NET and Sitecore functionality failed. Once the system recovered, it operated normally.

Standard log analysis provided no useful diagnostic information. I turned to Windows debugging tools to investigate crash dumps.

## Debugging Tools Overview

Two primary options exist for analyzing crash dumps:

**WinDbg** represents the comprehensive debugging toolkit, available through Microsoft's documentation. This tool excels at analyzing unmanaged code crashes involving memory errors and disk access issues. However, it requires significant expertise and proves challenging to master during active outages.

**Debug Diagnostic Tool v2 Update 2** offers a simpler alternative. This application automates dump analysis by monitoring app pools and generating automatic dump files upon crashes. Users can load dumps directly for analysis without requiring advanced debugging knowledge.

## Root Cause and Resolution

Through the Debug Diagnostic Tool's stack trace analysis, I identified that Sitecore was processing XML serialization during item link retrieval from SQL. This XML serialization process was repeatedly crashing, causing cascading failures during system initialization.

The solution involved running the database cleanup task and rebuilding the links database across all three databases. These actions resolved the issue completely.

Accessing the crash dump's stack trace proved essential for identifying and fixing the underlying problem.
