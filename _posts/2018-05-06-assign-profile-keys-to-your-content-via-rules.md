---
layout: post
title: "Assign profile keys to your content via RULES!"
date: 2018-05-06
tags: [Sitecore, Personalization, Rules]
featured: true
reading_time: 2
---

At Bonfire we developed a solution to automate profile key assignment in Sitecore. The core challenge addressed was that editors lacked time to manually assign profile cards to each content item—a significant barrier to effective personalization.

## The Solution

The solution involved creating a custom **RunRules processor** for the ProcessItem pipeline. This allowed rules to be executed at the item level, enabling automatic profile card assignments based on predefined logic rather than manual editor work.

Key implementation steps included:

- Establishing a new rules container under `/sitecore/system/Settings/Analytics/Rules`
- Creating a rules macro allowing users to select profile keys for assignment
- Calculating and assigning profile cards when rules conditions were met

## How It Works

The rule engine can evaluate multiple parameters including:
- Item hierarchy
- URLs
- Item metadata (category, taxonomy)
- User facet data

Once rules execute successfully, profile keys are assigned and pattern cards calculated.

## Results

The practical outcome allowed organizations to score thousands of items efficiently using targeted rules, enabling profiling and user data analysis without extensive manual effort.

**Next Steps:** Integrate Mark Stiles' Machine Learning repository to automate profile card determination further.
