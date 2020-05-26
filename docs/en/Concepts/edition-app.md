---
title: Edition App
description: "Edition app concept"
date: "2020-03-17"
tags: ["edition", "edition-app", "sponsor"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/docs/en/Concepts/edition-app.md"
---

# Edition App

An Edition App is an app responsible for **exporting an apps and configurations model** that a [Sponsor Account](https://vtex.io/docs/concepts/sponsor-account/) (also called parent account) sets for their child accounts to adopt.

Being built on top of a **hierarchical relationship between accounts**, each account can only have a single Edition App installed, and the apps and configurations that it exports can never be changed. Only the account's Sponsor Account is authorized to make any changes.

In VTEX platform, there are **two native Edition Apps** available to be installed. Presently, they are:

- `vtex.edition-business@0.x`: for stores whose front-end is built using [VTEX's CMS](https://help.vtex.com/tutorial/o-que-e-o-cms--EmO8u2WBj2W4MUQCS8262);
- `vtex.edition-store@2.x`: for stores whose front-end is built using [VTEX IO's Store Framework](https://vtex.io/docs/getting-started/build-stores-with-store-framework/1/).

You can check out which Edition App is installed in your VTEX account by running the `vtex edition` command using [Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/). 
