---
title: Making your new app version publicly available
description: "If you want to make your new app version publicly available, linking it will not suffice. Learn in this recipe the step by step on how to make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["release", "app", "promote", "production", "master", "workspace", "public", "available", "end-user", "version", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/making-your-new-app-version-publicly-available.md"
---

# Making your new app version publicly available

If you’re comfortable with the configurations you’ve performed and want your version of the app to be made available to any user, [linking](https://vtex.io/docs/recipes/store/linking-an-app) the app in which you’re working will not suffice: you’ll also need to **release** it, **publish** a release candidate, install it in a **production workspace**, **validate** your release candidate and promote it to **master**.

## Releasing

If you’re **sure about all the changes** that you’ve done to your development workspace, it’s time to **release** a new version of your app.

We’ll use the `vtex release {major/minor/patch}` command to release the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, updating the app's CHANGELOG.md, assigning commit tags and sending the performed changes to the app's repository.

If you desire to release a beta version, you should run `vtex release {major/minor/patch} beta` in your terminal. This command will perform the same activities as the previous one, the difference being that you’ll be launching the app’s beta version.

<div class="alert alert-warning">
You must be logged into the account where you want the new app version to be released. Make sure the app’s <code>vendor</code> is <strong>equal</strong> to its <code>account</code>.
</div>

## Publishing

Once a app version was released, the app **must be installed** in order to test its new settings. However, it is not possible to install an app that only exists in your local environment. You must **publish** the app so that it can be installed by yourself or by others as well.

Use the `vtex publish` command to turn the account version in which you were working into the app’s **release candidate version** for installment. Notice: a release candidate can **only** be installed on an account for testings if the user orders Toolbelt to install the exact version.

<div class=“alert alert-warning”>
You always must be logged into the account where you want the new app version to be published. Make sure the app’s <code>vendor</code> is <b>equal</b> to its <code>account</code>.
</div>

If your app **doesn’t** have billing options, users with access to the account in which the app was published can install it through the Admin’s Apps section. Otherwise, the app can be installed using Toolbelt, regardless of the specified [billing method](http://help.vtex.com/en/tutorial/app-pricing-models--2ZKBKxLe08Q6seA6sCi6o2).

## Production workspace

Now that you candidate release version is ready to be installed, you must **create a workspace in production mode** using the following command in order to test the app version settings:

```sh
vtex use {{WorkspaceName}} --production
```

<div class="alert alert-warning">
From this point onwards, any changes to the code are prohibited in the workspace, once it is ready to receive traffic, that is, to be accessed. If you want to change your code, work on it in a developer workspace and then follow the above-mentioned steps again.
</div>

### Instaling the candidate release version

To install the candidate release in the new production workspace, simply run one of the following commands:

```sh
`vtex install {appvendor}.{appname}@{appversion}` to install a specific version of the app.
```

<div class="alert alert-info">
  If you are releasing a <strong>beta</strong> app version and all settings were already tested by you, you should release a non-beta version for your app, publish it and install it in a production workspace, as stated previously. 
</div>

## Validating

Once the version is already installed in a production workspace, it is time to **validate your candidate release**. 

1. Test the release candidate’s **stability** by means of an [A/B test](https://vtex.io/docs/recipes/store/running-native-ab-testing).

<div class="alert alert-info">
  If you are releasing a <strong>beta</strong> app version and all settings were already tested by you, you should release a non-beta version for your app, publish it, install it in a production workspace and test its stability once more in order to follow the next step. 
</div>

2. Use the `vtex validate` command to **publish the release candidate as a stable version**. By using this command, Housekeeper will automatically install the new app stable version on all accounts that use the app.

## Master workspace

Promoting a workspace to **master** means making any changes performed in it available to the end user, in other words, making your **new app version publicly available**.

You can promote your production mode workspace to master using the following command:

```sh
vtex workspace promote
```

<div class="alert alert-info">
The status of a workspace in master is <code>production true</code>.
</div>

---

**Done**! Upon completing all the steps, your app’s new version will have been released, published, tested, validated and will finally be made public for all your end users!
