---
title: Releasing a new app version
description: "Overwrite the app's manifest.json, update the app's changelog.md and send the performed code changes to the app's repository by simply running one command in your terminal."
date: "04/09/2019"
tags: ["release", "releasing", "app", "version"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/releasing-a-new-app-version.md"
---

# Releasing a new app version

If you’re sure about all the changes that you’ve done to your development workspace, it’s time to release a new app version.

We’ll use the `vtex release {major/minor/patch}` command to increment the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, update the app's `CHANGELOG.md`, create a release commit and a release tag and finally send the performed changes to the app's repository.

Notice that the `vtex release` command will not create this new version on our infrastructure, and your app's new version will not be available yet for installing in accounts and workspaces, neither will this new version be automatically upgraded on accounts that have this app's major installed. 

## Command

Open your terminal and adjust the following command according to your app's needs:

`vtex release {major/minor/patch} {stable|beta}`
