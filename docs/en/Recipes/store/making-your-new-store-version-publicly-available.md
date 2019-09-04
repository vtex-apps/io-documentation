---
title: Making your store version publicly available
description: "If you want to make your new store publicly available, linking it will not suffice. Learn in this recipe the step by step on how to make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["release", "store", "promote", "production", "master", "workspace", "public", "available", "end-user", "version", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/making-your-new-store-version-publicly-available.md"
---

# Making your new store version publicly available

If you’re comfortable with the configurations you’ve performed and want your version of the store to be made available to any user, [linking]() the store theme app in which you’re working will not suffice: you’ll also need to **release** it, **publish** it, install it in a **production workspace** and promote it to **master**.

## Release

If you’re sure about all the changes that you’ve done to your development workspace, it’s time to release a new version of your store’s theme app.

We’ll use the `vtex release` command to release the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, updating its CHANGELOG.md, assigning commit tags and sending the performed changes to its repository.

You must run `vtex release major beta` in your terminal to automatically launch your new version in a beta environment. This will allow it to not only exist in your local environment but also to be installed and tested by you or other users with access to the account.

## Publish 

Once the new app version was already released, the app must be installed in order to test its new settings. However, it is not possible to install an app that only exists in its local environment. You must publish the app so that it can be installed by yourself or by others as well.

Use the `vtex publish` command to publish the app in the account in which you’re working.

<div class="alert alert-warning">
You must be logged into the account where you want the new app to be published. Make sure the app’s <code>vendor</code> is <strong>equal</strong> to its <code>account</code>.
</div>

If your app **doesn’t** have billingOptions, users with access to the account in which the app was added can install it through the Admin’s Apps section.

Otherwise, the app can be installed using Toolbelt, regardless of the specified billing method. [Click here](http://help.vtex.com/en/tutorial/app-pricing-models--2ZKBKxLe08Q6seA6sCi6o2) for more information on app billing models.

## Production workspace

In order to install and test your new store version, you must create a workspace in production mode using the following command: 

```
vtex use {{workspacename}} --production

```

<div class="alert alert-warning">
From this point onwards, any changes to the code are prohibited in the workspace, once it is ready to receive traffic, that is, to be accessed. If you want to change your code, work on it in a developer workspace and then follow the above-mentioned steps again.
</div>

To install an app in the new production workspace, simply run one of the following commands:

- `vtex install` if you are currently in the app's folder.
- `vtex install {appvendor}.{appname}` to install the latest version of the app.
- `vtex install {appvendor}.{appname}@{appversion}` to install a specific version of the app.

Once the app has been installed and tested in the production workspace, you can run `vtex release {major/minor/patch} stable` in your terminal to automatically launch your new version in a stable environment of your store. 

## Master workspace

Promoting a workspace to master means making any changes performed in it available to the end user, in other words, making your new store publicly available.

You can promote your production mode workspace to master using the following command:

`vtex workspace promote`

<div class="alert alert-info">
The status of a workspace in master is  <code>production true</code>.
</div>
