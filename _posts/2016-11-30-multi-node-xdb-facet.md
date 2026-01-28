---
layout: post
title: "Multi-node xDB Facet"
date: 2016-11-30
tags: [xDB, Development]
reading_time: 3
---

A previous post covered creating single-node facets for xDB to track contact information like name, company, and location. This article extends that concept to multi-entity facets using arrays, enabling tracking of repeated user actions such as "Products Viewed" or "Videos Watched."

Sitecore offers two facet array types:

## IElementCollection

This structure stores one-to-many elements as indexed arrays within the xDB Contact document. New elements are accessed by their numerical position rather than by name, with each entry receiving an incrementing integer identifier.

## IElementDictionary

This approach resembles IElementCollection but uses string-based identifiers instead of numeric indices. This enables retrieving specific nodes by name rather than array position. The xDB contact element predominantly uses IElementDictionary.

## Implementation Steps

**Data Object Creation**
Develop an interface inheriting from IElement and IValidatable to define the data structure.

**Container Development**
Build a new interface extending IFacet, IElement, and IValidatable with an IElementDictionary property holding your data object type. The property name "Entries" is conventional but flexible.

**Concrete Implementations**
Create serializable classes: one for the data object (inheriting from Element and related interfaces) and another for the container (inheriting from Facet and implementing EnsureDictionary in its constructor).

**Configuration**
The config file ties components together by mapping interfaces to concrete classes and defining facets within the xDB contact structure.

## Practical Application

Once configured, developers populate the facet by accessing it through its interface and name, then filling in the relevant data. This architecture supports numerous use cases including product views, watched videos, and downloaded resources.
