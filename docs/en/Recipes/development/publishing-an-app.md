---
title: Publishing an app
description: "Publish your app’s new version so that it can be installed and tested by other users."
date: "04/09/2019"
tags: ["publishing", "publish", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/publishing-an-app.md"
---

# Publishing an app

Once an app version was already [released](https://vtex.io/docs/recipes/store/releasing-a-new-app-version), it must also be **installed** in order to test its new settings. 

However, it is not possible to [install an app](https://vtex.io/docs/recipes/store/installing-an-app) that only exists in your local environment. Therefore, after the new app's version was released, you must publish it so that it can be installed by yourself or by others as well.

## Step by step

1. Make sure the app you are about to publish already has been [released](https://vtex.io/docs/recipes/development/releasing-a-new-app-version);

<div class="alert alert-warning">
You always must be logged into the account where you want the new app version to be published. Make sure the app’s <code>vendor</code> is <b>equal</b> to the <code>account</code> you are logged into.
</div>

2. Use the `vtex publish {appvendor}.{appname}@{appversion}` command to turn the new app’s version in which you were working into a **release candidate version**. Notice: a release candidate can **only** be installed on an account for testings if the user orders Toolbelt to install the exact version.

<div class="alert alert-warning">
  <b>Remember te replace the values between the curly brackets according to your scenario.</b>
</div>

3. Using a [Production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace), [install](https://vtex.io/docs/recipes/development/installing-an-app) the release candidate. 

<div class="alert alert-warning">
A Release Candidate can <b>only</b> be installed in an account for testings if the users orders Toolbelt to install the exact app version of it. 
</div>

4. Test the release candidate’s **stability** by means of an [A/B test](https://vtex.io/docs/recipes/store/running-native-ab-testing).

<div class="alert alert-info">
If you are releasing a <code>beta app version</code> and all settings were already tested by you, you should release a non-beta version for your app, publish it, install it in a production workspace and test its stability once more in order to follow the next step. 
</div>

5. Use the `vtex deploy` command to **publish the release candidate as a stable version**. By using this command, Housekeeper will automatically update the new app stable version on all accounts that have the app installed.


