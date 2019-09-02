---
title: Making your store publicly available
description: "If you want to make your new store publicly available, linking it will not suffice. Learn in this recipe the step by step on how to make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["release", "store", "promote", "production", "master", "workspace", "public", "available", "end-user", "version", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/MakingYourNewStorePubliclyAvailable.md"
---

# Making your new store publicly available

If you’re comfortable with the configurations you’ve performed and want your version of the store to be made available to any user, [linking]() the store theme app in which you’re working will not suffice: you’ll also need to **release** it, install it in a **production workspace** and promote it to **master**.

## Release

If you’re sure about all the changes that you’ve done to your development workspace, it’s time to release a new version of your store’s theme app.

We’ll use the `vtex release` command to release the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, updating its CHANGELOG.md, assigning commit tags and sending the performed changes to its repository.

You must run `vtex release major beta` in your terminal to automatically launch your new version in a beta environment and publish it in the account in which you’re working. This will allow it to not only exist in your local environment but also to be installed and tested by you or other users with access to the account.

## Production workspace

In order to install and test your new store version, you must create a workspace in production mode using the following command: 

```
vtex use {{workspacename}} --production

```

<div class=“alert alert-warning”>
From this point onwards, any changes to the code are prohibited in this workspace, once it is ready to receive traffic and be accessed. If you want to change your code, work on it in a developer workspace and then follow the above-mentioned steps again.
</div>

Once the app has been installed and tested in the production workspace, you can run `vtex release {major/minor/patch} stable` in your terminal to automatically launch your new version in a stable environment of your store. 

## Master workspace

Promoting a workspace to master means making any changes performed in it available to the end user, in other words, making your new store publicly available.

You can promote your production mode workspace to master using the following command:

`vtex workspace promote`

<div class=“alert alert-info”>
The status of a workspace in master is  <code>production true</code>.
</div>
