---
layout: post
title: "Parsing the __Tracker object for indexing"
date: 2016-01-25
tags: [Sitecore]
reading_time: 3
---

This article addresses performance challenges when indexing Sitecore profile data. Martin Davies discussed in a presentation how the TrackingField object in Sitecore performs excessive processing beyond indexing needs.

## The Problem

The standard approach using TrackingField involves significant overhead:

```csharp
TrackingField field = new TrackingField(i.Fields["__Tracking"]);
ContentProfile[] profiles = field.Profiles;
```

Davies suggested parsing XML directly would be faster, but didn't provide implementation examples.

## The Solution

I created a utility class called `TrackingConverter` that parses the tracking field's XML directly. The XML structure contains profile elements with associated key-value pairs representing user profile data.

I built POCO classes (`XdbProfile` and `XdbProfileKey`) to structure the parsed data, allowing developers to extract and manipulate profile information efficiently.

## Implementation

The solution integrates into a computed index field, replacing the TrackingField approach with direct XML parsing.

## Performance Results

| Method | Time to Index Master |
|--------|---------------------|
| TrackingField | 68 seconds |
| XML parsing | 46 seconds |
| **Improvement** | **12 seconds** |

Note: This improvement was measured across just 4 items with profile data. The difference scales significantly with larger datasets.

This approach significantly improves indexing performance when working with Sitecore profile data.
