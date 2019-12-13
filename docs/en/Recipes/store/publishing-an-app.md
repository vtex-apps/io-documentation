---
title: Publishing an app
description: "Publish your app’s new version so that it can be installed and tested by other users."
date: "04/09/2019"
tags: ["publishing", "publish", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/publishing-an-app.md"
---

# Publishing an app

Once a app version was released, the app **must be installed** in order to test its new settings. However, it is not possible [to install an app](https://vtex.io/docs/recipes/store/installing-an-app) that only exists in your local environment. You must publish the app so that it can be installed by yourself or by others as well.

## Command

1. Use the `vtex publish` command to turn the account version in which you were working into the app’s **release candidate version** for installment. Notice: a release candidate can **only** be installed on an account for testings if the user orders Toolbelt to install the exact version.

<div class=“alert alert-warning”>
You always must be logged into the account where you want the new app version to be published. Make sure the app’s <code>vendor</code> is <b>equal</b> to its <code>account</code>.
</div>

If your app **doesn’t** have billing options, users with access to the account in which the app was published can install it through the Admin’s Apps section. Otherwise, the app can be installed using Toolbelt, regardless of the specified [billing method](http://help.vtex.com/en/tutorial/app-pricing-models--2ZKBKxLe08Q6seA6sCi6o2).

Once the version is already installed in a production workspace, it is time to **validate your candidate release**. 

2. Test the release candidate’s **stability** by means of an [A/B test](https://vtex.io/docs/recipes/store/running-native-ab-testing).

<div class="alert alert-info">
If you are releasing a beta app version and all settings were already tested by you, you should release a non-beta version for your app, publish it, install it in a production workspace and test its stability once more in order to follow the next step. 
</div>

3. Use the `vtex validate` command to **publish the release candidate as a stable version**. By using this command, Housekeeper will automatically install the new app stable version on all accounts that use the app.

