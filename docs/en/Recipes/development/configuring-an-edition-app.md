---
title: Configuring an Edition App
description: "If you already match all requirements to become a Sponsor Account, learn now how to configure your own Edition Apps for child accounts!"
date: "2020-03-23"
tags: ["sponsor", "sponsor-account", "edition", "edition-app", "configure", "configuring"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/configuring-an-edition-app.md"
---

# Configuring an Edition App

The hierarchical relationship between a [Sponsor Account](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-sponsor-account/) and its children, established by an [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app/), creates uniformity throughout an account family.

Hence, it can be advantageous for **complex account families** under the same brand or holding to have its own Edition App.

Once you [enable the Sponsor Account behavior](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-becoming-a-sponsor-account) in one of your accounts, follow the steps below to create your own Edition app and install it on your child accounts.

## Step by step

### Step 1 - Creating an Edition app

1. Using your terminal and [VTEX IO's CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference), log in to your Sponsor Account.
2. Run the `vtex init` command.
3. Choose the `edition app` option. This will create a boilerplate repository in your local files.
4. Navigate to the `edition-app` folder and open the `manifest.json` file. It should look something like this:

```json
{
  "vendor": "vtex",
  "name": "edition-hello",
  "version": "0.1.1",
  "title": "Getting Started with VTEX Edition Apps",
  "description": "A sample edition app with a blank apps.json",
  "builders": {
    "edition": "0.x"
  },
  "dependencies": {
    "vtex.edition-business": "0.x"
  },
  "$schema": "https://raw.githubusercontent.com/vtex/node-vtex-api/master/gen/manifest.schema"
}
```

5. In the `manifest.json` file, change:

   - The `vendor` field to the name of the account you are logged in.
   - The `name` field to one of your choosing. We suggest to use an `edition-` prefix in your edition name, for easy identification among app lists.

### Step 2 - Setting the Edition dependencies

1. In the `manifest.json` file, go to the `dependecies`section.
2. Change the `dependencies` declaration, according to your development needs:

>ℹ️ Notice that the Edition App being developed extends its dependency, inheriting all its apps and configurations.

- If your store was built with [VTEX legacy CMS](https://help.vtex.com/tutorial/o-que-e-o-cms--EmO8u2WBj2W4MUQCS8262) and this is your first Edition App, keep it as `"vtex.edition-business": "0.x"`.
- If your store was built with the [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework) and this is your first Edition App, change it to `"vtex.edition-store": "5.x"`.
- If you have more complex inheritance needs, change it to an Edition App you have previously developed. The dependency's `vendor` must be the same one of the Edition App being developed.

>⚠️ Every Edition app must declare a dependency and only a single Edition App can be declared as a dependency.

3. Save your changes.

### Step 3 - Declaring apps

After setting up the initial configurations needed to develop your own Edition App, you can advance to declaring the bundle of apps and configurations that your Edition App will include.

1. Open the `edition/apps.json` file.
2. In the `apps` section, add all the apps and settings you want to impose to the child accounts. For example:
```diff
{
    "apps": {
+      "vtex.vtex-graphql-service": {
+        "defaultMajor": 1,
+        "allowedMajors": [0, 2],
+        "allowsUninstall": false,
+        "settings": {}
+       }
    }
}
```
Only the `defaultMajor` (or previously `major`) is obligatory, and all the others can be omited if they don't need to be configured.
   * `defaultMajor` or `major` fields determines the major of the app that will be installed by default, when the edition is set in some account.
   * `allowedMajors` allows specifying alternative majors that can be used by any account using the edition. Those majors can be used by manually installing the alternate version of the app using VTEX IO CLI (`vtex install`). If this field is omited or empty, it means that only the default major is allowed and it cannot be changed.
   * `allowsUninstall` serves to allow users to uninstall the app from the edition as well, to be done manually using VTEX IO CLI (`vtex uninstall`). If omited will default to `false`, i.e. that the app cannot be uninstalled by the account.
   * `settings` specifies the initial app settings to be set when the app is installed in the account via the edition. If omited, which is the recommended for most of the cases, no setting changes are made when installing the app.

>⚠️ Be aware that an Edition App can only contain apps exclusively developed by the same `vendor` responsible for its release.

If any conflict arises from declaring divergent app versions, the priority is always given to the parent Edition. That means it's impossible to change any inherited app or configuration - only extend them.

3. Save your changes.

The new Edition App will consist of the union of apps and configurations inherited from its parent Edition and the entries declared in the `apps.json` file.

### Step 4 - Deploying the Edition App

Once you are sure of all the changes performed, **[publish and deploy](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app)** your Edition App.

### Step 5 - Installing the Edition App on a child account

[Open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team requesting the installation of your new Edition App on the desired accounts.

Once you receive a successful reply from the support ticket, you'll start to have child accounts sponsored by the account you just used to develop and release your new Edition App.

>ℹ️ Notice that, from the child accounts' point of view, the apps specified by the Sponsor Account are immutable. That means child accounts aren't able to perform changes nor uninstall apps installed by a Sponsor Account. Hence, if you need to modify any app or configuration of your Edition App, you'll have to **launch a new version** bearing these changes. In this case, check our documentation on [updating Edition apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-updating-edition-apps).
