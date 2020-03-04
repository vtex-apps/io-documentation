---
title: Promoting a workspace to master
description: "Learn in this recipe how to promote a production workspace to master and make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["production", "promoting", "promote", "workspace", "master", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/promoting-a-workspace-to-master.md"
---

# Promoting a workspace to master

Promoting a workspace to master means making any changes performed in it available to the end user, in other words, making your new store publicly available.

## Command

If your workspace is already in production mode, it can be promoted to master using using the following command:

`vtex workspace promote`

The status of a workspace in master is production true.

<div class="alert alert-warning">
<strong>You can not make changes to a master workspace</strong> because a master workspace corresponds to the version that is available to the end user. Instead, work on the new code in development workspace, switch to a production workspace and then promote it.
</div>
