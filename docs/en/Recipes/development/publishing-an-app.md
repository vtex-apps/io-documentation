---
title: Publishing an app
description: "Publish your app’s new version so that it can be installed and tested by other users."
date: "04/09/2019"
tags: ["publishing", "publish", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/publishing-an-app.md"
---

# Publishing an app

After [releasing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-releasing-a-new-app-version) an app version, you must also validate its changes by running A/B tests and trying its new settings.   

However, since it is not possible to install an app that exists only in a local environment, you must first publish it and then [install it](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app) in the desired account to run tests.

## Step by step

1. Make sure the app you are about to publish has already been [released](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-releasing-a-new-app-version).

>⚠️ *To publish your app, you must be logged in to the account responsible for the app development. Make sure the app’s `vendor` is **equal** to the `account` you are logged in.*

2. In your terminal, run the `vtex publish {appvendor}.{appname}@{appversion}` command.

>⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

By performing this action, you will turn the new app version in which you were working into a **candidate version**.

>ℹ️ *A candidate version is an app version that meets all the requirements needed to be deployed.*

3. Using a [Production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace), [install](https://vtex.io/docs/recipes/development/installing-an-app) the candidate version by indicating to the Toolbelt the new app's exact version.

4. Test the candidate version’s **stability** by means of an [A/B test](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing).

>⚠️ *If you are releasing a **beta** version and have already tested all the app settings, to proceed to the next steps, you must first: release a non-beta version, publish it, install it in a production workspace, and test it once more using the A/B test.*

5. If all the app changes have already been tested and everything is working as expected, run the `vtex deploy {appvendor}.{appname}@{appversion}` command. 

>⚠️ *After publishing an app, you must wait 7 minutes to deploy it. Otherwise, you'll receive an "Invalid state transition" error from the Toolbelt. However, if you are using a Toolbelt version higher than `2.118.0` and deploying a **hotfix**, you can use the `--force` flag to instantly deploy your app version.*

By performing this action, you'll publish the candidate version as a stable version. Also, Housekeeper will automatically update the new app stable version on all accounts that have the app installed.

>ℹ️ *Publishing an app is one of the steps to **making your code's new version public**. For more details on how to make your app available to your end-users and to better understand the full procedure, access the recipe on [Making your new app version publicly available](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available).*
