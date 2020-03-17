---
title: Sponsor Account
description: "Sponsor account concept"
date: "2020-03-17"
tags: ["sponsor", "sponsor-account", "edition"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/concepts/docs/en/Concepts/sponsor-account.md"
---

# Sponsor Account

Sponsor Account is an account that is able to define which apps and configurations other accounts should adopt by means of an [**Edition App**](https://github.com/vtex/io-platform-documentation/blob/master/docs/concepts/edition-app.md).

Thinking of a genealogical tree, a Sponsor Account would be the **parent account** responsible for [configuring Edition apps](https://github.com/vtex/io-platform-documentation/blob/master/docs/recipes/configuring-an-edition-app.md) for its child accounts.

These child accounts, in turn, can also become Sponsor Accounts themselves, by creating (or already owning) child accounts and configuring edition apps for them.

This means that any VTEX account that [configure the Sponsor Account requirements](https://github.com/vtex/io-platform-documentation/blob/master/docs/recipes/edition-apps/configuring-the-sponsor-account-requirements.md), that is, any account with an already installed Edition App and a complex enough account family is able to configure an Edition app for another account.
