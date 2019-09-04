---
title: Creating a production workspace
description: "Create a workspace in production mode and test your app settings in a environment ready to receive traffic."
date: "04/09/2019"
tags: ["create", "creating", "production", "workspace", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/creating-a-production-workspace.md"
---

# Creating a production workspace

Workspaces in production mode are ready to receive traffic, that is, to be accessed by other account users. Once you are sure of your changes to the code, it is time to create one.  

## Command

You can create a production workspace simply using the following command: 

```
vtex use {{workspacename}} --production
```

<div class="alert alert-warning">
From this point onwards, any changes to the code are prohibited in the workspace. If you want to change your code, work on it in a developer workspace and then switch to a production one.
</div>
