---
title: Making your new app version publicly available
description: "If you want to make your new app version publicly available, linking it will not suffice. Learn in this recipe the step by step on how to make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["release", "app", "promote", "production", "master", "workspace", "public", "available", "end-user", "version", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/making-your-new-app-version-publicly-available.md"
---

# Making your new app version publicly available

If you’re comfortable with the configurations you’ve performed and want your version of the app to be made available to any user, [linking](https://vtex.io/docs/recipes/store/linking-an-app) the app in which you’re working will not suffice: you’ll also need to **release** it, install it in a **production workspace** and promote it to **master**.

## Release

If you’re sure about all the changes that you’ve done to your development workspace, it’s time to release a new version of your app.

We’ll use the `vtex release` command to release the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, updating its CHANGELOG.md, assigning commit tags and sending the performed changes to its repository.

You must run `vtex release major beta` in your terminal to automatically make an app beta version. This will allow it to not only exist in your local environment but also to be installed and tested by you or other users with access to the account.

<div class="alert alert-warning">
You must be logged into the account where you want the new app version to be released. Make sure the app’s <code>vendor</code> is <strong>equal</strong> to its <code>account</code>.
</div>

<div class="alert alert-info">
You can use the <code>vtex publish</code> command to make your app beta version ready for installation. However, it will not perform some automatic steps the way <code>vtex release</code> does, such as updating the app's CHANGELOG.md and ensure the correct version of the code is implemented.  
</div>

## Production workspace

In order to install and test your beta app version, you must create a workspace in production mode using the following command:

```sh
vtex use {{workspacename}} --production
```

<div class="alert alert-warning">
From this point onwards, any changes to the code are prohibited in the workspace, once it is ready to receive traffic, that is, to be accessed. If you want to change your code, work on it in a developer workspace and then follow the above-mentioned steps again.
</div>

To install an app in the new production workspace, simply run one of the following commands:

- `vtex install` if you are currently in the app's folder.
- `vtex install {appvendor}.{appname}` to install the latest version of the app.
- `vtex install {appvendor}.{appname}@{appversion}` to install a specific version of the app.

Once the **beta** app has been installed and tested in the production workspace, you can run `vtex release {major/minor/patch} stable` in your terminal to automatically make an app **stable** version ready for installation.

Having completed the above, simple follow the app installation steps to finally install the app **stable** version in your production workspace.

## Master workspace

Promoting a workspace to master means making any changes performed in it available to the end user, in other words, making your new app version publicly available.

You can promote your production mode workspace to master using the following command:

```sh
vtex workspace promote
```

<div class="alert alert-info">
The status of a workspace in master is <code>production true</code>.
</div>
