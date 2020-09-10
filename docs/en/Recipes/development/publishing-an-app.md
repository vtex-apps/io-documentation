---
title: Publishing an app
description: "Publish your app’s new version so that it can be installed and tested by other users."
date: "04/09/2019"
tags: ["publishing", "publish", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/publishing-an-app.md"
---

# Publishing an app

After [releasing](https://vtex.io/docs/recipes/store/releasing-a-new-app-version) an app version, you must also validate its changes by running A/B tests and trying its new settings.   

However, since it is not possible to install an app that exists only in a local environment, you must first publish it and then [install it](https://vtex.io/docs/recipes/store/installing-an-app) in the desired account to run tests.

## Step by step

1. Make sure the app you are about to publish has already been [released](https://vtex.io/docs/recipes/development/releasing-a-new-app-version).

<div class="alert alert-warning">
To publish your app, you must be logged into the account responsible for the app development. Make sure the app’s <code>vendor</code> is <b>equal</b> to the <code>account</code> you are logged into.
</div>

2. In your terminal, run the `vtex publish {appvendor}.{appname}@{appversion}` command.

<div class="alert alert-warning">
  <b>Remember to replace the values between the curly brackets according to your scenario.</b>
</div>

By performing this action, you will turn the new app version in which you were working into a candidate version, which is an app version that meets all the basic requirements to be deployed.

<div class="alert alert-info">
Notice: you can install a candidate version on an account for testings by indicating to the Toolbelt the new app's exact version.
</div>

3. Using a [Production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace), [install](https://vtex.io/docs/recipes/development/installing-an-app) the candidate version by indicating to the Toolbelt the new app's exact version.

4. Test the candidate version’s **stability** by means of an [A/B test](https://vtex.io/docs/recipes/store/running-native-ab-testing).

<div class="alert alert-info">
If you are releasing a <strong>beta</strong> version and all the app settings have already been tested, to follow to the next steps, you must release a non-beta version, publish it, install it in a production workspace, and test it once more using the A/B test.
</div>

5. Run the `vtex deploy {appvendor}.{appname}@{appversion}` command. 

<div class="alert alert-warning">
  <b>Remember to replace the values between the curly brackets according to your scenario.</b>
</div>

By performing this action, you'll publish the candidate version as a stable version. Also, Housekeeper will automatically update the new app stable version on all accounts that have the app installed.

<div class="alert alert-info">
Publishing an app is one of the steps to <b>making your code's new version public</b>. For more details on how to make your app available to your end-users and to better understand the full procedure, access the recipe on <a href="https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available">Making your new app version publicly available</a>.
</div>
