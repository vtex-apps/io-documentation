---
title: Promoting a workspace to Master
description: "Learn in this recipe how to promote a production workspace to master and make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["production", "promoting", "promote", "workspace", "master", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/promoting-a-workspace-to-master.md"
---

# Promoting a workspace to Master

Promoting a workspace to Master means making any changes performed in it available to the end user, in other words, making them publicly available.

Only a [Production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace) can be promoted to Master. 

## Command

If your workspace is already in production mode, it can be promoted to master using using the following command:

`vtex workspace promote`

**Notice**: you must be currently logged into an account and using the desired Production workspace to run the command stated above.

<div class="alert alert-warning">
<strong>You can not make changes to a master workspace</strong> because a master workspace corresponds to the version that is available to the end user. Instead, work on the new code in development workspace, reproduce it in a production workspace and then promote it. 
</div>
