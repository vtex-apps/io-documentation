---
title: Publishing an app
description: "Publish your app’s new version so that it can be installed and tested by other users."
date: "04/09/2019"
tags: ["publishing", "publish", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/publishing-an-app.md"
---

# Publishing an app

Once an app's version was already [released](https://vtex.io/docs/recipes/store/releasing-a-new-app-version) by you, the app **must also be installed** in order to test its new settings. However, it is not possible [to install an app](https://vtex.io/docs/recipes/store/installing-an-app) that only exists in your local environment. Therefore, after the new app's version was released, you must publish it that it can be installed by yourself or by others as well.

## Command

Use the `vtex publish` command to publish the new app’s version in which you are working. 

<div class=“alert alert-warning”>
You always must be logged into the account where you want the new app version to be published. Make sure the app’s <code>vendor</code> is <b>equal</b> to its <code>account</code>.
</div>

If your app **doesn’t** have billing options, users with access to the account in which the app was published can install it through the Admin’s Apps section. Otherwise, the app can be installed using Toolbelt, regardless of the specified [billing method](http://help.vtex.com/en/tutorial/app-pricing-models--2ZKBKxLe08Q6seA6sCi6o2).
