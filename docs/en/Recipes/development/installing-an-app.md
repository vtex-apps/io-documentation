---
title: Installing an app
description: "Test your app new settings by learning how to install it in a production workspace."
date: "04/09/2019"
tags: ["install", "installing", "app", "workspace", "production"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/installing-an-app.md"
---

# Installing an app

Installing an app is a fundamental step for testing the reliability of your new code settings. 

Once your app is already [published](https://vtex.io/docs/recipes/store/publishing-an-app), you are able to install it in any workspace you may be working on.

## Step by step

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), make sure you are logged into the desired account and using the desired workspace;
2. Then, run one of the following commands according to your needs and scenario:

- `vtex install {appVendor}.{appName}` - To install the **latest version** of the app;
- `vtex install {appVendor}.{appName}@{appVersion}` - To install a **specific version** of the app;
- `vtex install` - To install the **latest version** of the app if you are currently in the **app's directory**.
