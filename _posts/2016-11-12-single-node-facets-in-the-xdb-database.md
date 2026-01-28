---
layout: post
title: "Single node Facets in the xDB database"
date: 2016-11-12
tags: [xDB, Sitecore]
reading_time: 2
---

The xDB Mongo database collects essential data about each visitor to your Sitecore site. While it automatically tracks page clicks, time spent on pages, and user identity, its real strength lies in capturing organization-specific data.

Examples include tracking which videos users watched, viewing duration, or product preferences like leather couch colors. This custom information is stored as "facets" in xDB, which can be structured in multiple ways depending on tracking needs.

## Single Node Facets

Single node facets store data assigned once per contact, such as name or business affiliation. Creating them requires four steps:

1. Create a facet interface
2. Build a concrete implementation inheriting from Facet and your interface
3. Register the facet via Sitecore configuration
4. Add entries to contact records

## Implementation

Using capturing company contact information as an example, the interface must inherit from IFacet, while the concrete model requires serialization capabilities.

Configuration ties everything together, defining the element as "CompanyLookupModel" and registering it as the "CompanyData" facet. Once configured, developers retrieve the facet from the user's tracker and populate data.

## Data Persistence

Reading facet data mirrors the writing process—retrieve it by name or interface from the tracker. This data persists; when sessions end, information transfers to xDB. Upon return visits, the data reloads into the tracker, maintaining constant availability.
