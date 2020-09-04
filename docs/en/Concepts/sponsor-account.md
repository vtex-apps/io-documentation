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

This is especially useful for accounts that keep a hierarchical relationship with others, such as the main VTEX account of a holding or of a brand that has many sub-brands.

The image below illustrates how this account hierarchy manifests itself.

![HierarchicalRelationship](https://user-images.githubusercontent.com/60782333/91495980-c9194580-e891-11ea-8f23-f96759a5ece8.png)

In the first level, the `vtex` account sponsors all accounts with Edition Apps. That's because `vtex` is the account responsible for the development and release of the Edition Apps all others derive from:

- *Edition Business* (`vtex.edition-business@0.x`): used by stores built with our [legacy CMS](https://help.vtex.com/tutorial/o-que-e-o-cms--EmO8u2WBj2W4MUQCS8262)

- *Edition Store* (`vtex.edition-store@2.x`): user by stores built with our [Store Framework](https://vtex.io/docs/getting-started/build-stores-with-store-framework/1/) based on [VTEX IO](https://developers.vtex.com/docs/vtex_io-documentation_what-is-vtex-io)

In the second level of this hierarchy, accounts meeting the [requirements needed to become a Sponsor Account](https://vtex.io/docs/recipes/development/becoming-a-sponsor-account/) (e.g. `account2`) are capable of releasing their own derivative Edition App and use it to control the apps and configurations that should be set up in their children accounts (e.g. `account4`, `account5`, `account6`).

Being a Sponsor Account is especially useful for accounts that keep a hierarchical relationship with others, such as the main VTEX account of a holding or of a brand that has many sub-brands.

Hence, considering the great power a Sponsor Account has by defining which apps and configurations their child account should adopt, it's necessary to open a [support ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) expressing the desire to become one.

In the following, after releasing and implementing an Edition App in other accounts, the account responsible for the development of that Edition App will now be considered the Sponsor Account of the VTEX accounts that had that new Edition App installed.  
