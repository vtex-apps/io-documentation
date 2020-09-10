---
title: Releasing a new app version
description: "Overwrite the app's manifest.json, update the app's changelog.md and send the performed code changes to the app's repository by simply running one command in your terminal."
date: "04/09/2019"
tags: ["release", "releasing", "app", "version"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/releasing-a-new-app-version.md"
---

# Releasing a new app version

If you’re sure about all the code changes that you’ve done to your app in a **development** workspace, it’s time to release a new app version.

By the end of this step by step, you will:

- increment the version in the app’s `manifest.json` according to the SemVer (semantic versioning) best practices.
- update the app's `CHANGELOG.md`.
- create a release commit and a release tag.
- send the performed changes to the app's repository.

Notice that releasing a new app version will not create this new version in our infrastructure. That is, the app will not be publicly available yet for installing in other accounts and workspaces, neither will the new version be automatically upgraded on accounts that have this app's major installed. To do so, you need to release the app version and then [**publish**](https://vtex.io/docs/recipes/development/publishing-an-app) it.

## Step by step

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference#command-reference), log into the account responsible for the release of the new app version. Make sure the app’s `vendor` is equal to the logged account.
2. Access the app's local directory.
3. Run one of the following commands, according to your app's needs:

- `vtex release major stable` - To release a new **major** stable version.
- `vtex release minor stable` - To release a new **minor** stable version.
- `vtex release patch stable` - To release a new **patch** stable version.

- `vtex release major beta` - To release a **major** beta version.
- `vtex release minor beta` - To release a **minor** beta version.
- `vtex release patch beta` - To release a **patch** beta version.

<div class="alert alert-warning">
  <b>Remember to replace the values between the curly brackets according to your scenario.</b>
</div>

<div class="alert alert-info">
Releasing a new app version is one of the steps to <b>making your code's new version public</b>. For more details on how to make your app available to your end-users and to better understand the full procedure, access the recipe on <a href="https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available">Making your new app version publicly available</a>.
</div>
