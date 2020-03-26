---
title: Making your new app version publicly available
description: "If you want to make your new app version publicly available, linking it will not suffice. Learn in this recipe the step by step on how to make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["release", "app", "promote", "production", "master", "workspace", "public", "available", "end-user", "version", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/making-your-new-app-version-publicly-available.md"
---

# Making your new app version publicly available

If you’re comfortable with the configurations you’ve performed and want your version of the app to be made available to any user, [linking](https://vtex.io/docs/recipes/store/linking-an-app) the app in which you’re working will not suffice: you’ll also need to: 

1. **Release** it;
2. **Publish** a release candidate for it;
3. Install it in a **Production workspace**;
4. **Validate** your release candidate;
5. **Deploy** it as a stable version;
6. Promote the Production workspace to **Master**.

## Step 1 - Releasing a new app version

If you’re sure about all the changes that you’ve done to your **development** workspace, it’s time to release a new app version.

By one simple command, we will be able to increment the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, update the app's `CHANGELOG.md`, create a release commit and a release tag and finally send the performed changes to the app's repository.

Notice that **releasing a new app version will not create this new version on our infrastructure**. This means that **it will not be available yet for installing** in accounts and workspaces, neither will this new version be automatically upgraded on accounts that have this app's major installed. 

In order to do so, you first need to release the app version and then publish it.

1. Using your terminal, access the app's directory in your local files;
2. Once in it, run one of the following command according to your app's needs:

- `vtex release {major/minor/patch} stable` - To release a new **major** stable version;
- `vtex release {major/minor/patch} stable` - To release a new **minor** stable version;
- `vtex release {major/minor/patch} stable` - To release a new **patch** stable version.

<div class="alert alert-warning">
  <b>Remember te replace the values between the curly brackets according to your scenario.</b>
</div>

If you desire to release a **beta version**, you should run `vtex release {major/minor/patch} beta` in your terminal, adjusting the `{major/minor/patch}` value according to your app's needs. This command will perform the same tasks as the previous one, the difference being that you’ll be launching a beta version for your app.

<div class="alert alert-warning">
You must be logged into the account where you want the new app version to be released. Make sure the app’s <code>vendor</code> is <strong>equal</strong> to its <code>account</code>.
</div>

## Step 2 - Publishing the new app version

Once an app version was already released, it must also be **installed** in order to test its new settings. 

However, it is not possible to install an app that only exists in your local environment. Therefore, after the new app's version was released, you must publish it so that it can be installed by yourself or by others as well.

<div class="alert alert-warning">
You always must be logged into the account where you want the new app version to be published. Make sure the app’s <code>vendor</code> is <b>equal</b> to the <code>account</code> you are logged into.
</div>

Run the `vtex publish {appvendor}.{appname}@{appversion}` command to turn the new app’s version in which you were working into a **release candidate version**. 

<div class="alert alert-warning">
  <b>Remember te replace the values between the curly brackets according to your scenario.</b>
</div>


## Step 3 - Creating a Production workspace

Workspaces in production mode are ready to **receive traffic**, that is, to be **accessed by other account users**. 

Now that you candidate release version is ready to be installed, you must **create a workspace in production mode**  in order to test the app version settings and behavior. 

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), log into the desired account;
2. Once logged in, run the following command:

```sh
vtex use {{WorkspaceName}} --production
```

<div class="alert alert-warning">
From this point onwards, any changes to the code are <b>prohibited</b> in the workspace and you can only install new apps. This means that you are not able to <b>link</b> any app as well. If you want to change your code, work on it in a developer workspace and then copy all performed changes to a production one.
</div>

## Step 4 - Installing the candidate release version

A release candidate can **only** be installed on an account for testings if the user orders Toolbelt to install the exact version.

1. Make sure you still are logged into the desired account and using the Production workspace previously created. Then, run the following command:

```sh
vtex install {appvendor}.{appname}@{appversion}
```
<div class="alert alert-warning">
  <b>Remember te replace the values between the curly brackets according to your scenario.</b>
</div>

## Step 5 - Validating the candidate release version

Once the candidate release version is already installed in a production workspace, it is time to **validate** it. 

You should test the release candidate’s by means of an [**A/B test**](https://vtex.io/docs/recipes/store/running-native-ab-testing).

<div class="alert alert-warning">
  If you are releasing a <strong>beta</strong> app version and all settings were already tested by you, you should release a non-beta version for your app, publish it, install it in a production workspace and test it once more using A/B test in order to follow to the next step. 
</div>

## Step 6 - Deploying the app stable version

If all changes were already tested by you and everything is working as expected, it is time to deploy the candidate release as a stable version.

Still on the Production workspace, use the `vtex deploy {appvendor}.{appname}@{appversion}` command to **publish the release candidate as a stable version**. 

<div class="alert alert-warning">
  <b>Remember te replace the values between the curly brackets according to your scenario.</b>
</div>

Housekeeper will automatically update the new app stable version on all accounts that have the app installed.

## Step 7 - Promoting the Production workspace to Master

Promoting a workspace to Master means **making any changes performed in it available to the end user**, in other words, making them publicly available.

Once you are sure of the new app version and no further configurations are needed, you should promote to Master the Production workspace it is installed into.

<div class="alert alert-dangerous">
If you are developing a theme app, e.g. an app that is responsible for building your storefront, <b>make sure you've performed all needed changes regarding the store content</b> through your store theme code or the admin's Site Editor section.
</div>

1. Make sure you are logged into an account and using the desired Production workspace to be promoted;
2. Run the following command:

```sh
vtex workspace promote
```

<div class="alert alert-warning">
<strong>You can not make changes to a Master workspace</strong> because it corresponds to the version that is available to the end user. Instead, work on the new code in a Development workspace, reproduce it in a Production workspace and then promote it. 
</div>

**Done!** Upon completing all the steps, your app’s new version will have been released, published, tested, validated and will finally be made public for all your end users!


