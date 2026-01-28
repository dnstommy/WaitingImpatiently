---
layout: post
title: "Bonfire Profile Information API"
date: 2016-11-06
tags: [Sitecore]
reading_time: 1
---

The Bonfire team focuses on digital marketing, Sitecore Experience Platform, and customer journey tracking. I frequently need to monitor how current test users or real users progress through their experience, including questions like:

- Profile scores
- Pattern entries
- GeoIP information
- Facet triggers from login
- Engagement plan assignments
- Experience Value (EV)
- Goal completions

The original Sitecore Launch platform featured a slide-out window displaying user information. I expanded this concept into a comprehensive JSON API.

## Implementation

The implementation is available in the Bonfire.Analytics.Dto repository at GitHub. The API enables developers to examine user journeys during development and real-time analytics debugging, providing data exclusively for the current user.

The code targets Sitecore 8.1.151003 specifically, with planned updates for versions 8.0 and 8.2, as the Analytics codebase undergoes substantial modifications between releases.
