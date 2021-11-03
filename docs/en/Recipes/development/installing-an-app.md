---
title: Installing an app
description: "Learn how to correctly install a new app in your VTEX account."
date: "04/09/2019"
tags: ["install", "installing", "app", "workspace", "production"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/installing-an-app.md"
---

# Installing an app

In the VTEX IO platform, all code configuration is bundled in what we call *apps*. 

Therefore, when using the VTEX Store Framework, you will need to install several applications to your VTEX account in order to properly build the desired storefront.

In addition to that, if you are developing a new project, installing an app is a fundamental step for testing the reliability of your new code settings. Once your app is already [published](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app), you are able to install it in any workspace you may be working on.

>ℹ️ Remember the following: private apps (apps without the `billingOptions` field in its `manifest.json` file) can only be installed in the VTEX account where it was published. Public apps with free `billingOptions` can be installed in any VTEX account by any admin user. Lastly, public apps with billable `billingOptions` can only be installed by admin users with the License Manager's `BuyApp` permission. Once this installation takes place, the app will be charged by the end of every month in the accounts that installed it.


## Step by step

1. Using your terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference), make sure you are logged into the desired account and using the desired workspace.
2. Then, run one of the following commands according to your needs and scenario:

- `vtex install {appVendor}.{appName}` or `vtex install {appVendor}.{appName}@x` - To install the **latest stable version** of the app;
- `vtex install {appVendor}.{appName}@{appVersion}` - To install a **specific version** of the app;
- `vtex install {appVendor}.{appName}@ˆ{appVersion}` - To install any available version from the `{appVersion}` onwards. 

When specifying the `{appVersion}`, bear in mind the permitted structures:

- `@8.0.10`
- `@8.0.10-beta.3`
- `@8.x`
- `@^8.0.10`
- `@^8.0.10-beta.1`

>⚠️ VTEX IO CLI only interprets installation commands with ranges by majors. This means minors and patches can only be specified in scenarios where one of the structures stated above is being used. App versions as `@8.0.x` or `@8.2` are no longer allowed.
