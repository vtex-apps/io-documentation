---
title: Sponsor Account
description: "Sponsor account concept"
date: "2020-03-17"
tags: ["sponsor", "sponsor-account", "edition"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/docs/en/Concepts/sponsor-account.md"
---

# Sponsor Account

A Sponsor Account is a VTEX account responsible for the development and release of the [**Edition App**](https://vtex.io/docs/concepts/edition-app/) installed in its child accounts.

In other words, the Sponsor Account is responsible for establishing which apps and configurations other accounts should adopt by means of an Edition App.

That implies that, in VTEX, it exists a hierarchical relationship between accounts, such as the one presented in the following Figure, established by the Edition App installed in each account.

![HierarchicalRelationship](https://user-images.githubusercontent.com/60782333/91495980-c9194580-e891-11ea-8f23-f96759a5ece8.png)

From the Figure, notice that it exists a `vtex` account, which is the Sponsor Account of every exiting account in the VTEX environment. 

That's because `vtex` is the account responsible for the development and release of the fundamental Edition Apps used to set up a [VTEX's CMS](https://help.vtex.com/tutorial/o-que-e-o-cms--EmO8u2WBj2W4MUQCS8262) (`vtex.edition-business@0.x`) or a  [VTEX IO's Store Framework](https://vtex.io/docs/getting-started/build-stores-with-store-framework/1/) (`vtex.edition-store@2.x`) development environment.

Notice also that, besides `vtex`, any VTEX account that meets the [requirements needed to become a Sponsor Account](https://vtex.io/docs/recipes/development/becoming-a-sponsor-account/) is capable of releasing its own Edition Apps. 

Being a Sponsor Account is especially useful for accounts that keep a hierarchical relationship with others, such as the main VTEX account of a holding or of a brand that has many sub-brands.

Hence, considering the great power a Sponsor Account has by defining which apps and configurations their child account should adopt, it's necessary to open a [support ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) expressing the desire to become one.

In the following, after releasing and implementing an Edition App in other accounts, the account responsible for the development of that Edition App will now be considered the Sponsor Account of the VTEX accounts that had that new Edition App installed.  
