---
layout: post
title: "See your xDB marketing data in session"
date: 2018-05-20
tags: [Sitecore, xDB, Digital Marketing]
featured: true
reading_time: 2
---

At Sugcon EU I inquired about how developers and marketers access their xDB data during active sessions. This involves viewing facets, patterns, profile calculations, marketing automation activities, and other metrics in real-time to test personalization strategies.

I manage multiple facets containing valuable visitor data collected throughout user interactions. My development workflow requires constant visibility into current visitor and visit structure to verify my code functions correctly.

## The Bonfire Analytics DTO Tool

Seeking detailed analytical data, I created the Bonfire Analytics DTO tool, which provides comprehensive JSON output including:

- **Contact** information with xDB facets (email, phone numbers)
- **Session** data distinguishing current visits from cumulative visitor history
- **KeyBehaviorCache** containing goals, page events, channels, outcomes, campaigns
- **BehaviorProfiles** tracking
- **Tracker status** (IsActive)
- **CurrentPage** information
- **Interaction details** (geo, browser data from Mongo database)
- **Campaign** information
- **VisitCount** metrics
- **PagesViewed** during current session
- **GoalsList** and **EventsList** from the session

The tool is available on GitHub in two versions (Sitecore 8.2 and 9.0).
