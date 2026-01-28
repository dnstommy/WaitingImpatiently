---
layout: post
title: "What if I were to tell you the Sitecore.Kernel dll from NuGet isn't the latest?"
date: 2019-05-16
tags: [Sitecore, CI]
featured: true
reading_time: 3
---

Sitecore maintains an extensive knowledge base containing patches and updates necessary for various environments. The manner in which sites are patched carries significant importance, requiring consistency across all instances.

In Sitecore 8.2 Update 6 and 7, as well as 9.1 Update 1, the kernel contains a bug that crashes when encountering bad internal links. This malfunction can either crash the Rebuild Link Database application or bring down an entire site. When Sitecore attempts to resolve a link without proper error handling, it can fail deep within kernel code, producing a "System.FormatException: Unrecognized Guid format" error.

## The Patching Challenge

The solution involves a Sitecore knowledge base patch that completely replaces the Sitecore.Kernel dll. However, this presents a patching challenge: Sitecore does not publish hotfixes through NuGet packages; they release fixes through their knowledge base for selective implementation.

## Two Approaches

1. Include the patched kernel in builds
2. Exclude it entirely and patch servers manually

I advocate for the first option, emphasizing intentional CI builds that eliminate snowflake servers—environments with undocumented, manual patches.

## Recommended Solution

Create an Infrastructure.Patch project within Helix solutions to manage all patches centrally. This approach ensures consistency across environments and simplifies upgrades. By incorporating patches directly into build processes, organizations can achieve their goal of rebuilding production environments entirely through CI scripting.
