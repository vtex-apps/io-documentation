---
title: Making your new app version publicly available
description: "If you want to make your new app version publicly available, linking it will not suffice. Learn in this recipe the step by step on how to make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["release", "app", "promote", "production", "master", "workspace", "public", "available", "end-user", "version", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/making-your-new-app-version-publicly-available.md"
---

# Making your new app version publicly available

If you developed a new app version and are comfortable with the changes you performed, it is time to make it publicly available. For that, you'll need to take the following steps:

1. [**Release** it](#step-1---releasing-a-new-app-version).
2. [**Publish** a candidate version for it](#step-2---publishing-the-new-app-version).
3. [Install it in a **Production workspace**](#step-3---installing-the-cadidate-version-in-a-production-workspace).
4. [**Validate** the candidate version](#step-4---validating-the-candidate-version).
5. [**Deploy** it as a stable version](#step-5---deploying-the-app-stable-version).
6. [Promote the Production workspace to **Master**](#step-6---promoting-the-production-workspace-to-master).

&nbsp;
![public](https://user-images.githubusercontent.com/60782333/92799699-61332680-f38a-11ea-8a06-a342607070d9.png)
&nbsp;

## Step by step

Before you begin, open the terminal and use the [VTEX IO CLI](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference#command-reference) to log in to the account responsible for promoting the new app version, i.e., **the account specified as the app's vendor in the [Manifest](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-manifest) file.** During all the following steps, make sure you're logged into this account.

### Step 1 - Releasing a new app version

If you’re sure about all the changes that you performed in your development workspace, it’s time to release a new app version.

1. Open the terminal and change to your app local directory.
3. Run one of the following commands, according to your app's needs:

- `vtex release major stable` - To release a new **major** stable version.
- `vtex release minor stable` - To release a new **minor** stable version.
- `vtex release patch stable` - To release a new **patch** stable version.

- `vtex release major beta` - To release a **major** beta version.
- `vtex release minor beta` - To release a **minor** beta version.
- `vtex release patch beta` - To release a **patch** beta version.

>⚠️ *Replace the values between the curly brackets according to your scenario.*

By performing any of these actions, you will:

- Increment the app’s version in its `manifest.json` file, according to the SemVer (semantic versioning) best practices.
- Update the app's `CHANGELOG.md` file.
- Create a release commit and a release tag.
- Send the performed changes to the app's repository.

>ℹ️ *Notice that releasing a new app version doesn't mean saving this new version in our infrastructure. Consequently, the app will not be publicly available for installing in other accounts and workspaces yet, neither will the new version be automatically upgraded on accounts that have this major installed. To do so, you'll need to publish this app version.*

### Step 2 - Publishing the new app version

Until now, your app version exists only in a local environment. To make it possible to install it in specific accounts and run tests, you must first turn it into a **candidate version** by running the following command in your app directory:

```
vtex publish
```

>ℹ️ A candidate version of an app is one that meets all requirements needed for deployment.

### Step 3 - Installing the candidate version in a Production workspace

Before deploying your app's candidate version, make sure to install it in a **new Production workspace** to perform tests and check its behavior.

>ℹ️ [Production workspaces](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) are ready to **receive traffic**, that is, to be **accessed by other account users**. 

1. Create a Production workspace by running the following command:

```sh
vtex use {workspaceName} --production
```

2. Install the candidate version indicating the app's exact version as in the following:

```sh
vtex install {appvendor}.{appname}@{appversion}
```

Notice that, from this point onwards, you cannot link any app or make changes to your app code. Hence, if you need to perform any changes in your app, you must retreat and work on it in a development workspace.

>⚠️ *If you are developing a new store theme major, follow the steps in the [Migrating CMS settings after a theme major update](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-migrating-cms-settings-after-major-update) documentation before proceeding any further, since this could lead to undesired consequences, such as losing the admin's page template settings.*

### Step 4 - Validating the candidate version

Once the candidate version is installed in a Production workspace, it is time to **validate** it by running an [**A/B test**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing).

Notice that, if you are releasing a **beta** version of your app and have already tested all the app settings, you must take the following steps before proceeding any further: release a non-beta version, publish it, install it in a Production workspace, and test it once more using the A/B test.

### Step 5 - Deploying the app stable version

If you have already tested your app and everything is working as expected, run the following command to deploy the candidate version as a **stable version**:

```sh
vtex deploy {appvendor}.{appname}@{appversion}
```

By performing this action, all accounts that have your app installed will be automatically updated with this new stable version.

>⚠️ After publishing an app, you must wait 7 minutes to deploy it. Otherwise, you'll receive the following error: **Invalid state transition**. If you are deploying a **hotfix**, you can use the **`--force`** flag to deploy your app version instantly. This flag is available only for VTEX IO CLI versions higher than `2.118.0.`

### Step 6 - Promoting the Production workspace to Master

Once you are sure of your changes, it's time to make them publicly available to end-users by promoting to master the Production workspace used to deploy your app:

```sh
vtex workspace promote
```

>ℹ️ *You can not perform code changes in an app when using the `master` workspace because it corresponds to the version available to the end-user. Hence, if you want to perform any changes in the app code, you must retreat and work on the new code in a development workspace, then reproduce it in a Production workspace and promote it.*

**That's all!** Upon completing all the steps, your app’s new version will have been released, published, tested, validated, and will finally be made public for all your end-users!
