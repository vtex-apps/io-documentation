---
title: Creating a Production workspace
description: "Create a workspace in production mode and test your app settings in a environment ready to receive traffic."
date: "04/09/2019"
tags: ["create", "creating", "production", "workspace", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/creating-a-production-workspace.md"
---

# Creating a Production workspace

Workspaces in production mode are ready to **receive traffic**, that is, to be **accessed by other account users**. 

Once you are sure of your changes performed in the Development workspace, it is time to create a Production one in order to test them with traffic.

But notice: **the Production workspace will not inherit the changes performed in the Developer workspace**. All changes performed in the Development workspace will need to be replicated by you into the new Production workspace.

## Step by step

1. [Log into](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference#command-reference) the desired account;
2. Run the following command:

```sh
vtex use {{workspaceName}} --production
```

<div class="alert alert-warning">
  <b>Remember te replace the values between the curly brackets according to your scenario.</b>
</div>


From this point onwards, any changes to the code are <b>prohibited</b> in the workspace and you can only install new apps. This means that you are not able to <b>link</b> any app as well. If you want to change your code, work on it in a developer workspace and then copy all performed changes to a production one.

Once all configurations were tested, you can [promote the Production workspace to Master](https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master), making any changes performed available to the end user.  

<div class="alert alert-info">
  Creating a Production workspace is one of the steps to <b>making your code's new version public</b>, meaning that it will become available to your end users. For more details on the next steps and to better understand the full flow, access the recipe on <a href="https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available">Making your new app version publicly available</a>.
</div>


