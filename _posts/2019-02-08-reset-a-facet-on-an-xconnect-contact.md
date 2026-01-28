---
layout: post
title: "Reset a facet on an xConnect contact"
date: 2019-02-08
tags: [xDB, xConnect, Sitecore, Facets]
featured: true
reading_time: 2
---

This article addresses a technical challenge in Sitecore 9.x regarding facet management on xConnect contacts. In the earlier 8.2 version, developers could use a `.Reset()` extension method to clear facets, but this functionality was removed in 9.x.

## The Problem

When attempting to replace an existing facet with a new instance, developers encounter the error "Facet already exists on the contact." This occurs because xConnect tracks facets using a `ConcurrencyToken` to maintain data integrity and prevent unauthorized overwrites.

## The Solution

Rather than manually resetting each property to its default value, I created a custom extension method. The extension creates a fresh facet instance while preserving the original `ConcurrencyToken` through reflection:

```csharp
public static T GetFacetWithDefaultValues<T>(this T facet) where T : Facet, new()
{
    var newFacet = new T();
    var concurrencyTokenProperty = typeof(Facet).GetProperty("ConcurrencyToken");
    var originalToken = concurrencyTokenProperty.GetValue(facet);
    concurrencyTokenProperty.SetValue(newFacet, originalToken);
    return newFacet;
}
```

This approach copies the concurrency token from the existing facet to a newly instantiated facet, allowing xConnect to accept the replacement without triggering integrity validation errors.

The solution also includes functionality for cases where developers want to swap in a pre-populated facet while maintaining the concurrency token.
