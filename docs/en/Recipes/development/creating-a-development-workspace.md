---
title: Creating a Development workspace
description: "Build your app settings in an isolated environment, ready to receive your development. Create now your Development Workspace!"
date: "2020-04-09"
tags: ["create", "creating", "development", "workspace", "develop"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/creating-a-production-workspace.md"
---

# Creating a Development workspace

Workspaces in development mode can [link](https://vtex.io/docs/recipes/development/linking-an-app/), [publish](https://vtex.io/docs/recipes/development/publishing-an-app/) and [install](https://vtex.io/docs/recipes/development/installing-an-app/) apps. These workspaces enjoy **greater development freedom**, since **they do not handle traffic** from any user except yourself. 

Because development workspace do not have any level of user traffic, they cannot be promoted to master nor used for A/B testing. Only Production workspaces can.
 
## Step by step

1. Log into the desired account;
2. Run the following command:
  
```sh
vtex use {workspaceName}
```

<div class="alert alert-warning">
<b>Remember to replace the values between the curly brackets according to your scenario and needs.</b>
</div>

Once you are sure of the changes performed in the Development workspace, it is time to [create a Production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace) in order to test your changes with user traffic.

But be aware: **the Production workspace will not inherit the changes performed in the Development workspace**. All changes performed in the Development workspace will need to be replicated in the new Production workspace.

<div class="alert alert-info">
Creating a Development workspace is one of the steps to <b>making your code's new version public</b>, meaning that it will become available to your end users. For more details on the next steps and to better understand the full flow, access the recipe on <a href="https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available">making your new app version publicly available</a>.
</div>
