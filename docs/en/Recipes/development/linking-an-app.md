---
title: Linking an app
description: "Sync your local files with an app and ensure that your code changes are reflected in real time in your workspace."
date: "06/09/2019"
tags: ["local-files", "linking", "link", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/linking-an-app.md"
---

# Linking an app

For development, an app can be linked to a **development workspace** so that any local code change can be automatically synced and made available in that corresponding workspace.

>⚠️ Linking an app to a [production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) is not possible.

## Step by step

1. Open the terminal and log in to your VTEX account.
  ```
  vtex login {account}
  ```
2. Change to a **development workspace**.
  ```
  vtex use {workspace}
  ```
3. Change to your app's directory.
  ```
  cd {directory}
  ```
4. Link your app to the current workspace by running the following command: 
  ```
  vtex link
  ```

Once your local files are uploaded and synced to your development environment, you should see the following message: `App linked successfully`. Use `https://{workspace}--{account}.myvtex.com`, where `workspace` is the development workspace in use and `account` is the name of your VTEX account, to check your local version of the app.

Notice that the synced app will only be available within the specified development workspace.

If you are comfortable with your changes and want to make your changes publicly available, please refer to [this](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available) guide.
