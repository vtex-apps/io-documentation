---
title: Making your new app version publicly available
description: "If you want to make your new app version publicly available, linking it will not suffice. Learn in this recipe the step by step on how to make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["release", "app", "promote", "production", "master", "workspace", "public", "available", "end-user", "version", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/making-your-new-app-version-publicly-available.md"
---

# Making your new app version publicly available

If you are comfortable with the changes you performed and want to make your version of the app publicly available, [linking the app](https://vtex.io/docs/recipes/store/linking-an-app) will not suffice, you’ll also need to:

1. [**Release** it](#step-1---releasing-a-new-app-version).
2. [**Publish** a candidate version for it](#step-2---publishing-the-new-app-version).
3. [Install it in a **Production workspace**](#step-3---creating-a-production-workspace).
4. [**Validate** the candidate version](#step-5---validating-the-candidate-version).
5. [**Deploy** it as a stable version](#step-6---deploying-the-app-stable-version).
6. [Promote the Production workspace to **Master**](#step-7---promoting-the-production-workspace-to-master).

&nbsp;
![public](https://user-images.githubusercontent.com/60782333/92799699-61332680-f38a-11ea-8a06-a342607070d9.png)
&nbsp;

## Step by Step

## Step 1 - Releasing a new app version

If you’re sure about all the changes that you performed in your development workspace, it’s time to release a new app version.

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference#command-reference), log in to the account responsible for the release of the new app version. Make sure the app’s `vendor` is equal to the logged account.
2. Access the app's local directory.
3. Run one of the following commands, according to your app's needs:

- `vtex release major stable` - To release a new **major** stable version.
- `vtex release minor stable` - To release a new **minor** stable version.
- `vtex release patch stable` - To release a new **patch** stable version.

- `vtex release major beta` - To release a **major** beta version.
- `vtex release minor beta` - To release a **minor** beta version.
- `vtex release patch beta` - To release a **patch** beta version.

>⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

By performing one of these actions, you will:

- Increment the app’s version in its `manifest.json` file, according to the SemVer (semantic versioning) best practices.
- Update the app's `CHANGELOG.md` file.
- Create a release commit and a release tag.
- Send the performed changes to the app's repository.

>ℹ️ *Notice that releasing a new app version doesn't mean saving this new version in our infrastructure. Consequently, the app will not be publicly available for installing in other accounts and workspaces yet, neither will the new version be automatically upgraded on accounts that have this major installed. To do so, you'll need to publish this app version.*

## Step 2 - Publishing the new app version

Until now, your app version exists only in a local environment. Hence, to try the new settings of the released app version, you must first publish it and then install it in the desired account to run tests.

>⚠️ *To publish your app, you must be logged in to the account responsible for the app development. Hence, make sure the app’s `vendor` is equal to the account you are logged in.*

In your terminal, run the `vtex publish {appvendor}.{appname}@{appversion}` command.

>⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

By performing this action, you will turn the new app version in which you were working into a **candidate version.**

>ℹ️ *A candidate version is an app version that meets all the requirements needed to be deployed.*

## Step 3 - Creating a Production workspace

Workspaces in production mode are ready to **receive traffic**, that is, to be **accessed by other account users**. 

Now that your candidate version is ready to be installed, you must **create a workspace in production mode**  to test the app version settings and behavior. 

1. Using your terminal, log into the desired account.
2. Run the following command:

```sh
vtex use {{WorkspaceName}} --production
```

>⚠️ *From this point onwards, code changes are prohibited, meaning that you can only install new apps. That also means that you are not able to link any app. Hence, if you want to perform any changes in the app code, you must retreat and work on it in a development workspace.*

## Step 4 - Installing the candidate version

To perform tests, you must install the candidate version by indicating to the Toolbelt the new app's exact version.

1. Make sure you still are logged into the desired account and using the Production workspace previously created. 
2. Run the following command:

```sh
vtex install {appvendor}.{appname}@{appversion}
```

>⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

## Step 5 - Validating the candidate version

Once the candidate version is installed in a production workspace, it is time to **validate** it. 

We recommend you to test it by means of an [**A/B test**](https://vtex.io/docs/recipes/store/running-native-ab-testing).

>⚠️ *If you are releasing a **beta** version and have already tested all the app settings, to proceed to the next steps, you must first: release a non-beta version, publish it, install it in a production workspace, and test it once more using the A/B test.*

## Step 6 - Deploying the app stable version

If all the app changes have already been tested and everything is working as expected, it is time to deploy the candidate version as a stable version.

>⚠️ *After publishing an app, you must wait 7 minutes to deploy it. Otherwise, you'll receive an "Invalid state transition" error from the Toolbelt. However, if you are using a Toolbelt version higher than `2.118.0` and deploying a **hotfix**, you can use the `--force` flag to instantly deploy your app version.*

1. Make sure you still are logged into the desired account and using the Production workspace previously created. 
2. Run the following command:

```sh
vtex deploy {appvendor}.{appname}@{appversion}
```

>⚠️ *Remember to replace the values between the curly brackets according to your scenario.*

By performing this action, you'll **publish the candidate version as a stable version**. Also, Housekeeper will automatically update the new app stable version on all accounts that have the app installed.

## Step 7 - Promoting the Production workspace to Master

Once you are sure of the new app version and no further configurations are needed, you must promote to Master the Production workspace used to deploy your app.

Promoting a workspace to Master means making any changes performed in it available to the end-user, in other words, making them publicly available.

>ℹ️ *If you are developing a theme app, e.g. an app that is responsible for building your storefront, **make sure you've performed all needed changes regarding the store content** through your store theme code or the admin's Site Editor section.*

1. Make sure you still are logged into the desired account and using the Production workspace to be promoted.
2. Run the following command:

```sh
vtex workspace promote
```

>ℹ️ *You can not perform code changes in an app when using a Master workspace because it corresponds to the version that is available to the end-user. Hence, if you want to perform any changes in the app code, you must retreat and work on the new code in a development workspace, then reproduce it in a Production workspace and promote it.*

**That's all!** Upon completing all the steps, your app’s new version will have been released, published, tested, validated, and will finally be made public for all your end-users!
