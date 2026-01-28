---
layout: post
title: "Tracking anonymous users in xDB post 8.2 update 3"
date: 2017-08-03
tags: [Sitecore, xDB]
featured: true
reading_time: 1
---

Sitecore implemented a significant configuration change affecting xDB tracking behavior. The system now restricts tracking to identified users by default—those who have logged in, clicked ExM links, or had `Sitecore.Analytics.Tracker.Current.Session.Identify(identifier)` applied to their session.

This shift prioritizes performance and reduces index congestion, as every session previously populated xDB. The official rationale states: To improve performance and optimize indexing, we changed the default value of `ContentSearch.Analytics.IndexAnonymousContacts` setting from true to false.

## The Problem

Sites without e-commerce or subscriber bases may find this problematic. Organizations relying on anonymous behavioral signals—IP addresses, company information, location data—for personalization lose critical tracking capabilities.

## Configuration Solution

The relevant file is `Sitecore.ContentSearch.Analytics.config`. Locate the setting:

```xml
<setting name="ContentSearch.Analytics.IndexAnonymousContacts" value="false"/>
```

Changing the value to `"true"` restores full user tracking, including anonymous visitors.

I recommend implementing this patch for all instances requiring anonymous user tracking functionality.
