---
title: Creating a Development workspace
description: "Build your app settings in an isolated environment, ready to receive your development. Create now your Development Workspace!"
date: "2020-04-09"
tags: ["create", "creating", "development", "workspace", "develop"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/creating-a-production-workspace.md"
---

# Creating a Development workspace

[Workspaces](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace/) in development mode can [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/), [publish](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app/) and [install](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app/) apps. These workspaces enjoy **greater development freedom**, since **they do not handle traffic** from any user except yourself. 

Because development workspace do not have any level of user traffic, you should use them whenever you want to perform changes in your code. But notice: they cannot be [promoted to Master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master/) nor used for [A/B testing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing/) - only [Production workspaces](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace/) can.
 
## Step by step

1. [Log into](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installment-and-command-reference#command-reference) the desired VTEX account;
2. Run the following command:
  
```sh
vtex use {workspaceName}
```

> ⚠️ 
> 
> Remember to replace the value in the curly brackets according to your store's scenario and needs.

Once created, the Developer workspace has no expiration date, which means that settings will remain stored in it unless there is any conflict with the store's Master workspace configurations. In these cases, **the Master settings will always prevail over the settings of the other account's workspaces**, including the Developer one in which you are working, since the account's workspaces work as a copy of the version available to the end-user. 

Stick to the list of workspaces created for your account. It is important to keep a shortlist for two reasons:

- Your organization.

- Spare platform infrastructure resources. 

Currently, no service is responsible for automatically deleting unused workspaces from an account. This means that you must manually delete workspaces that are no longer being used by running `vtex workspace delete {workspaceName}`.

> ⚠️
> 
> Be aware: once you **delete a workspace**, it is **not possible to restore it** and its content.

## Next Step

Once you are sure of the changes performed in the Development workspace, it is time to [create a Production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace) to test your changes with some user traffic.

> ⚠️
> 
> **The Production workspace will not inherit the changes performed in the Development workspace**. All changes performed in the Development workspace will need to be replicated in the new Production workspace.


Creating a Development workspace is one of the steps to making your code's new version public, meaning that it will become available to your end-users. For more details on the next steps and to better understand the complete flow, access the recipe on [making your new app version publicly available.](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available)
