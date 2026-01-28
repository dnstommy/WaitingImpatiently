---
layout: post
title: "9.1 Release of the Bonfire Analytics DTO"
date: 2019-04-09
tags: [xConnect, Sitecore]
featured: true
reading_time: 1
---

I needed to monitor what Sitecore observes about users and sessions, encompassing goals, events, profiles, patterns, pages, geographic data, marketing automation, and xConnect facets—both current and historical versions.

I originally created a JSON application for version 8.2 and have maintained it through the 9.1 release cycle.

## Key Feature: Handling Sitecore Facets

The system retrieves requested facets through ContactExpandOptions. My approach involves accessing the xConnect server configuration to obtain all KnownModels (available facet models), passing these into ContactExpandOptions to retrieve and serialize all facets.

## JSON Output Includes

The resulting JSON output includes:
- Identifiers
- Contact status
- Visited pages
- Interaction details
- Current and past goals
- Current and past events
- xConnect facets with values
- Current profile identification
- Past profile identification

Check the GitHub releases page for access to the tool.
