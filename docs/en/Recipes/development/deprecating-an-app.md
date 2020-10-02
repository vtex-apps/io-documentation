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

For these scenarios, using the [Toolbelt](https://vtex.io/docs/concepts/toolbelt/) and the terminal, log in to the account correspondent to the `vendor` of the app going to be deprecated and run the following command:

```
vtex deprecate {appvendor}.{appname}@{appversion}
```

:warning: *Remember to replace the value in the curly brackets according to your scenario.*

Once the deprecation is completed, it might take some time, but *eventually*, the deprecated app will be uninstalled and downgraded to its latest stable version in every VTEX account.

You also have the option to *instantly* install the latest stable version of that app in an account by running the following command: 

```
vtex update {appvendor}.{appname}
```

:information_source: *Keep in mind that the deprecation won't delete the app or version from our registry, meaning that it will still be possible to manually install it in any account by running `vtex install {appvendor}.{appname}@{appversion}`.*

However, if you realize that the deprecation was unnecessary and decide to republish that given version, you can run the following command:

```
 vtex undeprecate {appvendor}.{appname}@{appversion}
```
