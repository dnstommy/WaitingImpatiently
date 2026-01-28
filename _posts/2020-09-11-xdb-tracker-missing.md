---
layout: post
title: "xDB.Tracker Identifier Missing"
date: 2020-09-11
tags: [xConnect, Sitecore, xDB]
reading_time: 3
---

A persistent bug in Sitecore xConnect involves contact identifier management during merge operations. When two contacts merge, the system must select which identifiers to retain, but it frequently discards the xDB.Tracker identifier entirely.

There are two key identifier types: the Alias identifier (a random GUID assigned at contact creation) and the xDB.Tracker (assigned only during web visits). The problem occurs when merging contacts—the system fails to preserve the xDB.Tracker, leaving contacts unable to process subsequent web visits.

When affected, users encounter an error stating "Contact...must have a tracker identifier." This breaks tracking functionality until users clear their cookies, forcing them to essentially restart their session.

## The Solution

The solution involves creating a custom pipeline processor that executes before Sitecore's standard conversion process. This processor checks for missing xDB.Tracker identifiers and regenerates them via xConnect API calls when necessary. This fix resolves approximately 60 daily errors down to roughly one occurrence every 4-5 days.

This approach is a temporary workaround—hopefully the community can help reproduce the underlying issue for official Sitecore resolution.
