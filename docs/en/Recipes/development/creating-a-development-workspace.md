---
title: Creating a Development workspace
description: "Build your app settings in an isolated environment, ready to receive your development. Create now your Development Workspace!"
date: "2020-04-09"
tags: ["create", "creating", "development", "workspace", "develop"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/creating-a-production-workspace.md"
---

# Creating a Development workspace

[Workspaces](https://vtex.io/docs/concepts/workspace/) in development mode can [link](https://vtex.io/docs/recipes/development/linking-an-app/), [publish](https://vtex.io/docs/recipes/development/publishing-an-app/) and [install](https://vtex.io/docs/recipes/development/installing-an-app/) apps. These workspaces enjoy **greater development freedom**, since **they do not handle traffic** from any user except yourself. 

Because development workspace do not have any level of user traffic, you should use them whenever you want to perform changes in your code. But notice: they cannot be [promoted to Master](https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master/) nor used for [A/B testing](https://vtex.io/docs/recipes/development/running-native-ab-testing/) - only [Production workspaces](https://vtex.io/docs/recipes/development/creating-a-production-workspace/) can.
 
## Step by step

1. [Log into](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference#command-reference) the desired VTEX account;
2. Run the following command:
  
```sh
vtex use {workspaceName}
```

<div class="alert alert-warning">
<b>Remember to replace the value in the curly brackets according to your store's scenario and needs.</b>
</div>

Once you are sure of the changes performed in the Development workspace, it is time to [create a Production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace) in order to test your changes with some user traffic.

But be aware: **the Production workspace will not inherit the changes performed in the Development workspace**. All changes performed in the Development workspace will need to be replicated in the new Production workspace.

Once created, the Developer workspace has no expiration date, which means that settings will remain stored in it unless there is any conflict with the configurations of the store’s Master workspace. 

In these cases, **the Master settings will always prevail over the settings of the other account's workspaces**, including the Developer one in which you are working.

<div class="alert alert-info">
Stick to the list of workspaces created for your account. It is important to keep a short list, not only for your own organization but also to spare platform infrastructure resources. Currently, <strong>there is no service responsible for automatically deleting unused workspaces from an account</strong>. This means that you must manually delete workspaces that are no longer being used by running <code>vtex workspace delete {workspaceName}</code>.
</div>

<div class="alert alert-info">
Creating a Development workspace is one of the steps to <b>making your code's new version public</b>, meaning that it will become available to your end users. For more details on the next steps and to better understand the full flow, access the recipe on <a href="https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available">making your new app version publicly available</a>.
</div>
