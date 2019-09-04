---
title: Releasing a new app version
description: "Overwrite the app's manifest.json, update the app's changelog.md and send the performed code changes to the app's repository by simply running one command in your terminal."
date: "04/09/2019"
tags: ["release", "releasing", "app", "version"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/tree/master/docs/en/Recipes/store"
---

# Releasing a new app version

If you’re sure about all the changes that you’ve done to your development workspace, it’s time to release a new app version.

We’ll use the `vtex release` command to release the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, updating its CHANGELOG.md, assigning commit tags and sending the performed changes to its repository.

## Command

Open your terminal and adjust the following command according to your app's needs:

`vtex release {major/minor/patch} {stable|beta}`
