---
layout: post
title: "MediaCachePath for Multisite Site configs"
date: 2017-06-12
tags: [Multisite]
reading_time: 2
---

A client organization extended Sitecore to maximize platform value by transforming several parent sites into hundreds of child/member sites. This architecture provides member sites with inherited content from parent sites plus access to comprehensive product catalogs containing thousands of images.

## The Problem

The critical issue emerges in how Sitecore handles media caching across multisite configurations. When users request images, Sitecore extracts them from SQL and stores them in the App_Data/MediaCache folder. Resized or mobile-optimized versions are also cached.

The problem: this process repeats independently for every site. A single 2MB image used across 600 sites consumes 1.2GB of storage—multiply this across thousands of images and disk space becomes unsustainable.

## Understanding Media Cache Paths

The default media cache path follows this pattern: `{Media Cache Folder}/{Site Name}/{Hash of media item}`. The site name component creates separate caches per site, which makes sense when sites have different image processing logic. However, when 600 sites share identical image logic, this design wastes storage.

The `Sitecore.Resources.Media.MediaCacheRecord` class contains the `GetRootFolder()` function that determines media paths. When requests originate from defined sites, it returns the MediaCachePath from that site's configuration.

## The Solution

Configure the `mediaCachePath` attribute in site configurations to point multiple sites toward a shared cache folder:

```xml
<site name="site1"
      mediaCachePath="/App_Data/MediaCache/ParentSite"
      ... />
```

By configuring multiple sites to use the same cache folder path, duplicate images no longer consume excessive disk space across the multisite infrastructure.
