---
title: Configuring an Edition App
description: "If you already match all requirements to become a Sponsor Account, learn now how to configure your own Edition Apps for child accounts!"
date: "2020-03-23"
tags: ["sponsor", "sponsor-account", "edition", "edition-app", "configure", "configuring"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/adding-new-docs/docs/en/Recipes/development/configuring-an-edition-app.md"
---

# Configuring an Edition App

Using an [Edition app](https://vtex.io/docs/concepts/edition-app) is very advantageous for **complex account families** under the same brand or holding.

Such a hierarchical relationship between a [Sponsor Account](https://vtex.io/docs/concepts/sponsor-account) and its children with a Edition Apps provides **uniformity** throughout the account family, which can share some similar apps and settings base configuration.

Any VTEX account is able to configure an Edition app and thereby define apps and settings for other accounts. Simply follow the steps detailed below. 

## Step by step

### Step 1 - Becoming a Sponsor account

The first step to configuring an Edition app is to **become a Sponsor Account**.

Any account can become a Sponsor Account, including those that are children of another account i.e. have a Sponsor themselves.

To become a Sponsor Account and be able to configure child account Editions, go through our documentation on [configuring the Sponsor Account requirements](https://vtex.io/docs/recipes/development/configuring-the-sponsor-account-requirements).

### Step 2 - Creating an Edition app

Once the Sponsor Account requirements are configured, you'll need to create and **publish Edition apps** of your own, as follows:

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), log into the Sponsor Account;
2. Run the `vtex init` command;
3. Choose the `edition app` option and accept the actions required by Toolbelt;

<div class="alert alert-info">
After selecting <code>edition app</code>, a <b>template repository</b> will be automatically copied to your local files. This is a working edition but defined with some default configurations. Your new Edition will be created by editing the apps and configurations declared in the template repository files.
</div>

4. Open the recently created folder for the Edition app using any code editor of your preference;
5. In the `manifest.json` file, change:
   - The `vendor` field to the name of the account you are logged in;
   - The `name` field to one of your choosing, which will be your new Edition's name. We suggest to use an `edition-` prefix in your edition name, for easy identification among app lists.

### Step 3 - Configuring the new Edition's parent

In the `manifest.json` file, take a look at the app's current dependency: `vtex.edition-store`.

An Edition App must always **declare a single other Edition app as a dependency** in order to **inherit** all the apps and configurations from that *parent* Edition.

<div class="alert alert-info">
This depended edition app must be published by the Edition App vendor i.e. the Sponsor Account. <b>Notice</b>: the Edition App declared as the parent of the new edition <code>does not</code> necessarily need to be the the Edition installed in the account you are logged in. <b>The dependency can be set for any Edition App that exists in the Sponsor Account's registry</b>.
</div>

### Step 4 - Declaring the apps and configurations model

After declaring an Edition app parent as a dependency in `manifest.json` file, let's focus on the `edition/apps.json` file to perform the desired app and configuration changes.

It is time to add all apps and settings you want to impose to the child accounts. 

Notice that **the new Edition app will result in a union of apps and configurations inherited from the parent Edition and the entries you will add to the Edition's own** `apps.json` **file**.

Should any conflict arise from this, for example if both Edition's declare the same app on different majors, **priority is always given to the parent Edition**, which means that it's impossible to change any inherited installation or app's configuration - only *extend* them.

### Step 4 - Deploying the app

Once you are sure of all changes performed, it is time to [**publish and deploy**](https://vtex.io/docs/recipes/store/publishing-an-app) the new Edition app.

### Step 5 - Installing it in a child account

Once the Edition app is already published and deployed by the Sponsor Account, it's time to install it in the desired child account(s). 

This means that the accounts that will necessarily adopt the apps and configurations present in the Edition.

1. Install the `vtex.tenant-provisioner` app in the account you are logged in, granting it access to the Edition installation APIs in the desired child accounts;
2. Switch your login to the child account you want to change the edition of. Use the `vtex switch` command with the name of the desired child account, such as: `vtex switch {childAccountName}`;
3. Once logged in the child account, [create a production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace);
4. Run `vtex edition set` adding the name and version of the Edition app that was published in the previous step. e.g.: `vtex edition set vtex.edition-example@1.x`;
5. If everything is working as expected, [promote the production workspace to master](https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master).

<div class="alert alert-info">
An app's billing options do not interfere in the Edition's architecture. Whether public or private, Edition apps will be automatically installed in all child accounts as long as the app vendors are the same as the Sponsor account's.
</div>

After your Edition App is installed in the child account's master workspace, no further actions are required: the child account configuration with an Edition App is **done**!

You may want to **launch new versions** bearing changes in the apps and configurations list, for which you'll need to check out our documentation on [updating Edition apps](https://vtex.io/docs/recipes/development/updating-edition-apps).
