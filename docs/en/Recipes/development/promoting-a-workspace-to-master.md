---
title: Promoting a workspace to Master
description: "Learn in this recipe how to promote a production workspace to master and make your new configurations finally available to the end user."
date: "29/08/2019"
tags: ["production", "promoting", "promote", "workspace", "master", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/promoting-a-workspace-to-master.md"
---

# Promoting a workspace to Master

Promoting a workspace to Master means making your code changes usable to the end user, in other words, making them publicly available.

According to the different types of [workspaces](https://vtex.io/docs/concepts/workspace/) in the platform, **only [Production workspaces](https://vtex.io/docs/recipes/development/creating-a-production-workspace) can be promoted to Master**. [Developer workspaces], in turn,(https://vtex.io/docs/recipes/development/creating-a-development-workspace/) only must be used for code development and testings. 

## Step by step

1. Make sure you are [logged into](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference#command-reference) an VTEX account and using the desired Production workspace to be promoted;
2. Run the following command:

`vtex workspace promote`

<div class="alert alert-warning">
<strong>You can not make changes to a Master workspace</strong> because it corresponds to the version that is available to the end user. Instead, work on the new code in a Development workspace, reproduce it in a Production workspace in order to test your changes with user traffic and then promote it to Master. 
</div>

Notice the following: **whenever you promote a Production workspace to Master, other account's workspaces will also be impacted with the new changes.** 

This is due to the fact that the account's workspaces work as a copy of the version available to the end user. Therefore, the Master settings will always prevail over the settings of the other account's workspaces. 

<div class="alert alert-info">
Promoting a Master workspace is one of the steps to <b>making your code's new version public</b>, meaning that it will become available to your end users. For more details on the next steps and to better understand the full flow, access the recipe on <a href="https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available">Making your new app version publicly available</a>.
</div>
