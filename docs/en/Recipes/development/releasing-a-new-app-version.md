---
title: Releasing a new app version
description: "Overwrite the app's manifest.json, update the app's changelog.md and send the performed code changes to the app's repository by simply running one command in your terminal."
date: "04/09/2019"
tags: ["release", "releasing", "app", "version"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/releasing-a-new-app-version.md"
---

# Releasing a new app version

If you’re sure about all the changes that you’ve done to your **development** workspace, it’s time to release a new app version.

By one simple command, we will be able to increment the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices, update the app's `CHANGELOG.md`, create a release commit and a release tag and finally send the performed changes to the app's repository.

Notice that **releasing a new app version will not create this new version on our infrastructure**. This means that **it will not be available yet for installing** in accounts and workspaces, neither will this new version be automatically upgraded on accounts that have this app's major installed. 

In order to do so, you first need to release the app version and then [**publish**](https://vtex.io/docs/recipes/development/publishing-an-app) it.

## Step by step

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
