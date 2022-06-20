---
title: Promoting a workspace to Master
description: "Learn how to promote a production workspace to master and make your new configurations available to end-users."
date: "29/08/2019"
tags: ["production", "promoting", "promote", "workspace", "master", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/promoting-a-workspace-to-master.md"
---

# Promoting a workspace to Master

Promoting a production workspace to Master marks the final step to [making an app publicly available to end-users](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available). After launching your app as a stable version and thoroughly testing it in a production workspace, you can promote your workspace to Master to finally make your new app version publicly available to end-users.

Notice that, once promoted to Master, it's not possible to perform new code changes in your app version. Alternatively, you would need to develop your code in a [development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/) and reproduce it in a new production workspace, so you could test your changes with user traffic before making your new changes publicly available.

![Promoting a Production workspace to Master](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/Media/promoting-a-workspace-to-master.gif?raw=true)

## Before you start

Before proceeding any further, make sure the app you are about to publish has already been [deployed](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-deploying-the-app-stable-version).

Also, keep in mind that when you promote a workspace to Master, your modifications are applied to all workspaces of the logged account. Hence, if you are promoting a new version of the [Store Theme app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-3-settingyourstoretheme) to Master, make sure to perform all necessary store content adjustments in the Site Editor and your code beforehand.

Promoting a workspace to master is one of the steps to **making your new app version publicly available**. Please refer to [this](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available) guide for more information. 

## Step by step

Take the following steps to promote a Production workspace to Master. Remember to replace the values between curly braces according to your scenario.

1. Open the terminal and log in to your VTEX account.

    ```shell
    $ vtex login {accountName}
    ```

2. Change to the Production workspace to be promoted.

    ```shell
    $ vtex use {workspaceName}
    ```

3. Promote the workspace in use.

    ```shell
    $ vtex workspace promote
    ```
