---
title: Creating a Production workspace
description: "Create a workspace in production mode and test your app settings in a environment ready to receive traffic."
date: "04/09/2019"
tags: ["create", "creating", "production", "workspace", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/creating-a-production-workspace.md"
---

# Creating a Production workspace

Workspaces in production mode are ready to **receive traffic**, that is, to be **accessed by other account users**. 

Once you are sure of your changes performed in the Development workspace, it is time to create a Production one in order to test them with traffic.

But notice: a Production workspace is created from scratch, meaning it does not inherit the code changes performed in a Developer workspace. All changes performed in a Development workspace need to be replicated by you into your new Production workspace. 

## Step by step

1. [Log into](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference#command-reference) the desired VTEX account;
2. Run the following command:

```sh
vtex use {workspaceName} --production
```

<div class="alert alert-warning">
<b>Remember te replace the value in the curly brackets according to your store scenario and needs.</b>
</div>

From this point onwards, **any changes to the code are prohibited in the Production workspace and you can only install new apps in it**. This means that you are not able to link any app as well. If you want to change your code, work on it using a [Developer workspace](https://vtex.io/docs/recipes/development/creating-a-development-workspace/) and then copy all performed changes to a Production one.

Once created, the Production workspace has no expiration date, which means that settings will remain stored in it unless there is any conflict with the configurations of the store’s Master workspace. 

In these cases, **the Master settings will always prevail over the settings of the other account's workspaces**, including the Production one in which you are working.

<div class="alert alert-info">
Stick to the list of workspaces created for your account. It is important to keep a short list, not only for your own organization but also to spare platform infrastructure resources. Currently, <strong>there is no service responsible for automatically deleting unused workspaces from an account</strong>. This means that you must manually delete workspaces that are no longer being used by running <code>vtex workspace delete {workspaceName}</code>.
</div>

Once all configurations were tested, you can [promote the Production workspace to Master](https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master), making your code changes finally available to the end user.  

<div class="alert alert-info">
Creating a Production workspace is one of the steps to <b>making your code's new version public</b>, meaning that it will become available to your end users. For more details on the next steps and to better understand the full flow, access the recipe on <a href="https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available">Making your new app version publicly available</a>.
</div>


