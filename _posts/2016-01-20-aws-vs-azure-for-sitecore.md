---
layout: post
title: "AWS vs Azure for Sitecore"
date: 2016-01-20
tags: [Sitecore, AWS, Azure]
reading_time: 5
---

This article examines infrastructure options for Sitecore deployments, focusing on virtual machine configurations rather than PaaS solutions.

## Azure Server Tiers

Azure offers four server levels:

- **Basic** servers lack autoscaling and load balancing capabilities, suitable only for minimal-traffic single farms.
- **Standard** servers provide better performance at affordable rates with load balancing support.
- **D-Series** represents modern Xeon-based infrastructure with SSD temporary storage—recommended as the starting point for serious Sitecore deployments.
- **Dv2-Series** delivers the latest processors (Xeon E5-2673 v3 or better) with similar storage configurations.

Azure pricing operates on pay-as-you-go terms without long-term discount options.

| Tier | Cost per Core | Cost per GB RAM (monthly) |
|------|---------------|---------------------------|
| Basic | $56.21 | $32.12 |
| Standard | $65.70 | $37.54 |
| D-Series | $102.20 | $29.20 |
| Dv2-Series | $133.52 | $32.43 |

## AWS EC2 Approach

Amazon uses M-series for production workloads. Unlike Azure's direct-attached storage, AWS utilizes SAN-based drives, allowing customers to choose disk types (magnetic, SSD, optimized) and quantity independently.

On-demand M-series pricing: approximately $89.70 per core, ~$22.42 per GB RAM.

Reserved instances dramatically reduce costs:

| Commitment | Cost per Core | Cost per GB RAM |
|------------|---------------|-----------------|
| 1-year | $58.00 | ~$14.37 |
| 3-year | ~$44.60 | ~$11.17 |

Three-year AWS reserved instances undercut Azure's cheapest offerings while providing modern server specifications.
