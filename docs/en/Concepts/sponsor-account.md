---
title: Sponsor Account
description: "Sponsor account concept"
date: "2020-03-17"
tags: ["sponsor", "sponsor-account", "edition"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/docs/en/Concepts/sponsor-account.md"
---

# Sponsor Account

Sponsor Account is an account that is able to define which apps and configurations other accounts should adopt by means of an [**Edition App**](https://vtex.io/docs/concepts/edition-app/).

Thinking of a genealogical tree, a Sponsor Account would be the **parent account** responsible for [configuring Edition apps](https://vtex.io/docs/recipes/development/configuring-an-edition-app/) for its child accounts.

These child accounts, in turn, can also become Sponsor Accounts themselves by owning child accounts and configuring edition apps for them.

This means that any VTEX account that matches the [requirements needed to be a Sponsor Account](https://vtex.io/docs/recipes/development/configuring-the-sponsor-account-requirements/) is able to configure an Edition app for another account.
