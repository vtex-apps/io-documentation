---
title: Promoting a workspace to Master
description: "Learn how to promote a production workspace to master and make your new configurations available to end-users."
date: "29/08/2019"
tags: ["production", "promoting", "promote", "workspace", "master", "production-mode"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/promoting-a-workspace-to-master.md"
---

# Promoting a workspace to Master

Promoting a workspace to Master marks the final step to make an app publicly available to end-users.

After you launch your app as a stable version and thoroughly test it in a particular [Production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace), you can promote this workspace to Master.

>⚠️ Whenever you promote a workspace to Master, all workspaces of the logged account are updated with your changes.

![Promoting a Production workspace to Master](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/Media/promoting-a-workspace-to-master.gif?raw=true)

Once promoted to Master, you won't be able to perform new code changes in that workspace. Alternatively, you will need to develop your code in a [Development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/) and reproduce it in a new Production workspace, so you can test your changes with user traffic and make your new changes publicly available.

>ℹ️ Notice that you cannot make changes directly to the Master workspace nor promote a Development workspace to Master.

## Step by step

Take the following steps to promote a Production workspace to Master. Remember to replace the values between curly braces according to your scenario.

1. Log in to your VTEX account.

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

>⚠️ When promoting a new version of the [store theme app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-3-settingyourstoretheme) to Master, first make sure to perform all the necessary changes in the store content through the Site Editor or your store theme code.

---

💡 Promoting a Master workspace is one of the steps to [making your new app version publicly available to end-users.](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available)
