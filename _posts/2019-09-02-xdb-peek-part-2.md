---
layout: post
title: "Bonfire releases xDB Peek (Part 2)"
date: 2019-09-02
tags: [xDB, Sitecore]
reading_time: 4
---

This installment continues from Part 1, diving into the breakdown of xDB Peek's information categories and upcoming features.

## Contact Section

The contact tab houses all xConnect-related contact data, including:

**Identifiers** - A comprehensive list of assigned identifiers and merged accounts, containing source, identifier value, type, and validity status.

**IsKnown** - Indicates whether a contact has been identified using methods beyond Sitecore's default identifiers, such as through the IdentifyAs() function or direct xConnect assignment.

**ExpandOptions** - Displays available facets for xConnect interaction, functioning as a registry of known facets.

**ConcurrencyToken** - A GUID that Sitecore applies to all facets. Mismatched tokens during save operations trigger an error, preventing facet overwrites. Each object possesses a unique token.

**LastModified** - Timestamp of the most recent contact modification.

**Id** - The primary contact identifier visible in Experience Profile URLs and the Contacts table within shard databases (distinct from tracker contact IDs).

## Visit Data Section

Current interaction information specific to the active web visit:

- **BrowserInfo** - Browser identification data including major name, minor name, and version.
- **ChannelId** - Current visit's assigned channel, variable based on traffic source.
- **DeviceId** - Associated device identifier from Sitecore's device registry.
- **GeoData** - Geographic information derived from IP geolocation services (available free in Sitecore 9.x).
- **HasGeoIpData** - Boolean indicating geolocation data availability.
- **InteractionId** - Unique identifier for the specific web visit.
- **Ip** - User's IP address in hexadecimal format (requiring hex decoding).
- **Keywords** - Keywords assigned to the interaction.
- **Language** - Current visit's language designation.
- **ScreenInfo** - Device screen dimensions as Sitecore perceives them, based on browser-provided data.
- **SiteName** - Identified Sitecore site from the sites configuration node.

## Pages Section

Comprehensive listing of all pages visited during the current interaction, excluding pages from previous sessions. Contains page title, URL, and blank-window status.

## Goals Section

Records goals triggered during web visits or out-of-channel activities, displaying engagement value, title, UTC timestamp, current/past visit designation, and associated event data.

**CurrentGoals** - Goals triggered within the current session, enabling Sitecore to personalize based on present-session activity.

**PastGoals** - Goals triggered before the current visit, allowing personalization based on historical behavior. Current session goals transition to past goals upon visit closure.

## Facets Section

Lists all available contact facets populated from ExpandOptions. Example Personal facet contains birthdate, name components, gender, job title, language preference, concurrency token, and modification timestamp.

## Profiles Section

Tracks current and historical pattern card assignments based on profile scoring:

**CurrentProfiles** - Active pattern cards with profile name, score, count, and pattern details.

**PastProfiles** - Historical pattern cards with scoring frequency, totals, and individual score records by key-value pairs.
