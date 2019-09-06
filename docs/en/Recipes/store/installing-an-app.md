---
title: Installing an app
description: "Test your app new settings by learning how to install it in a production workspace."
date: "04/09/2019"
tags: ["install", "installing", "app", "workspace", "production"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/installing-an-app.md"
---

# Installing an app

Installing an app in a [production workspace](https://vtex.io/docs/recipes/store/creating-a-production-workspace) is a fundamental step for testing the reliability of your new code settings. Once your app is already [published](https://vtex.io/docs/recipes/store/publishing-an-app), you should follow the steps below

## Command

To install an app in the production workspace, simply run one of the following commands:

- `vtex install` if you are currently in the app's folder.
- `vtex install {appvendor}.{appname}` to install the latest version of the app.
- `vtex install {appvendor}.{appname}@{appversion}` to install a specific version of the app.
