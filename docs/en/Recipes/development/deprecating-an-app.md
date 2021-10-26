---
title: Deprecating an app
description: "Something went wrong? Learn how to deprecate an app."
date: "02/10/2020"
tags: ["deprecate", "version", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/deprecating-an-app.md"
---

# Deprecating an app

A deprecated version of an app or a deprecated app is one that developers discourage its use. It can be because it leads to errors or because a better alternative exists.

If you have any doubts if you should deprecate an app version or not, take the following example: imagine that you develop the app `mystore.store-theme`, which latest version published is `mystore.store-theme@1.0.1`. You developed a new feature and want to release the new version `mystore.store-theme@1.2.0`. 

You publish the app, but later that day, you realize there's a bug in it. 

There are two options to deal with it:

1. Release a new version with the bug fix.
2. Deprecate the app version with the bug and downgrade it to the latest stable version.

If the bug is simple, it's not affecting sales, and you know how to solve it, the first option might be the best one.

However, if the bug is critical or if you need a lot of time to fix it, we recommend that you go with the second option. 

By deprecating the app version with the issue, you will be opting for re-establishing the store. In this scenario, it will uninstall `mystore.store-theme@1.2.0` and fallback to the previous released version, `mystore.store-theme@1.0.1`.

Once the store is working fine, you'll have time to work on the fix without affecting sales and users.

For this scenario, check the following step by step. 

## Step by Step

Using the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) and the terminal, log in to the account correspondent to the `vendor` of the app going to be deprecated and run the following command:

```
vtex deprecate {appvendor}.{appname}@{appversion}
```

>⚠️ Remember to replace the value in the curly brackets according to your scenario.

Once the deprecation is completed, it might take some time, but *eventually*, the deprecated app will be uninstalled and downgraded to its latest stable version in every VTEX account.

You also have the option to *instantly* install the latest stable version of that app in an account by running the following command:

```
vtex update {appvendor}.{appname}
```

> ℹ *Keep in mind that the deprecation won't delete the app or version from our registry, meaning that it will still be possible to manually install it in any account by running `vtex install {appvendor}.{appname}@{appversion}`.*

However, if you realize that the deprecation was unnecessary and decide to republish that given version, you can run the following command:

```
 vtex undeprecate {appvendor}.{appname}@{appversion}
```
