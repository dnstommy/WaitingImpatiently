---
layout: post
title: "Using Identity Server and Bearer Tokens to Authenticate Sitecore"
date: 2019-01-24
tags: [Sitecore, Identity-Server]
featured: true
reading_time: 3
---

In Sitecore 9.1, the platform transitioned its authentication infrastructure from ASP.NET Membership to Identity Server 4 paired with ASP.NET Identity. This modernization shift enabled Sitecore to replace proprietary bearer token implementations with standardized OAuth authentication protocols.

For end users, the transition appeared seamless. The login interface remained unchanged, and existing role-based permissions persisted. However, the technical shift unlocked significant architectural benefits. Organizations could now leverage Sitecore's OAuth capabilities as a central authentication mechanism for single sign-on across their entire infrastructure. Additionally, the decoupling of the core database from Content Delivery servers became possible, since the ASP.NET Identity server could operate independently.

## Important Caveats

The identity server implemented for Commerce Server is NOT the same as the one for Sitecore XP/XM. Commerce utilizes a custom client profile called "postman-api" that functions exclusively with commerce APIs, not the broader Sitecore ecosystem.

A notable limitation exists in the Item API, which continues using legacy hand-rolled bearer tokens rather than the new standardized approach.

## Technical Implementation

Securing API endpoints requires the `[Authorize]` attribute on controllers. To obtain bearer tokens, developers must POST to the identity server endpoint with credentials including `grant_type`, `client_id`, `username`, `password`, and `client_secret`. The client secret is stored in the identity server's configuration file.

API calls then include the token in the HTTP Authorization header with the format: `Bearer [access_token]`.
