---
layout: post
title: "Order of Pipelines for the Analytics Tracker"
date: 2016-02-22
tags: [Sitecore, xDB]
reading_time: 1
---

I encountered challenges while developing a Tracker modification for Sitecore's marketplace. The core issue involved determining which pipeline stage to use for custom code that calls an external API to gather user details.

## The Problem

Initial attempts to place the custom code in the `startTracking` and `initializeTracker` pipelines resulted in the code executing on every page load. This was problematic since each of these API calls cost a little money.

## The Solution

Move the code to the `createVisit` pipeline—the stage responsible for populating tracker data with user information such as browser type, screen size, and IP address. This placement ensures the custom code executes only once per visit rather than repeatedly.

While this approach makes logical sense in retrospect, up until that point it was confusing me greatly.

## Reference

Martin Davies's blog post on Sitecore request processing helped clarify the pipeline execution sequence during the development process.
