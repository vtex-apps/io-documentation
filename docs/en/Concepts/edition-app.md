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

Being built of top of a **hierarchical relationship between accounts**, the Edition App (and the apps and configurations that it exports) can never be changed by the child accounts. Only its Sponsor Account is authorized to make any changes.

Each account can only have a single Edition App installed, defined by its Sponsor Account. However, each account is able to **publish** multiple Edition Apps to their registry, which means that children from the same Sponsor Account can have different apps and configurations from each other.

Being hierarchical in nature, any child account can also define their own Edition Apps for their child accounts themselves, the only restriction being that these Edition Apps must "extend" exactly one Edition App from their respective Sponsor. This extension is specified through a single dependency in the Edition App's `manifest.json` file.
