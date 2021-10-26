---
title: Making your theme content public
description: "If you are always struggling with making your theme content public using the VTEX IO platform, learn all the necessary steps now."
date: "2020-04-28"
tags: ["theme", "public", "store", "available"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/store-management/making-your-theme-content-public.md"
---

# Making your theme content public

Once you're using VTEX IO Store Framework, making a new version of your theme public (or even the first version) can be a big challenge if any of the necessary steps are unclear.

To better understand the process, you need to remember that **your store's theme works exactly as any other platform app**.
This means that it takes on an app's default behavior, with its own versioning and deploys. 

## Step by step

If you’re comfortable with the configurations you’ve performed and want your new theme to be made available to any user, you’ll need to:

1. [**Link**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) the theme to a [Development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/) in order to test your changes;
2. [**Release**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-releasing-a-new-app-version/) the theme;
3. [**Publish**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app/) it as a release candidate version;
4. [Install](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app/) the theme in a [**Production workspace**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace/) in order to test your changes with traffic;
5. [**Validate**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app/) it as a release candidate if no more changes are needed. If changes to the theme are required, you should go back to step 1 and use a Development workspace. You must not perform changes using a production workspace.  
6. [**Deploy**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app/) it as a stable version if you are sure about all the changes you performed;
7. [Promote the Production workspace to **Master**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master/), finally making your theme public to your store's end users. 

For more details on each of these steps, you can check out the recipe on [**Making your new app version publicly available**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available/), considering that your store theme works exactly as an app, as previously mentioned. 
