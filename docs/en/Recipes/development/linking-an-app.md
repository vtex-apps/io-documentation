---
title: Linking an app
description: "Sync your local files with an app and ensure that your code changes are reflected in real time in your workspace."
date: "06/09/2019"
tags: ["local-files", "linking", "link", "app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/linking-an-app.md"
---

# Linking an app

When linking an app, your computer's local files sync to our cloud development environment. This means that any change done locally in the code you are working on will be sent to the cloud and then reflected in the workspace in which you are working.

In practice, you will be able to actually verify your changes by accessing the account you are logged in using the workspace you are using to develop.

## Step by step

To link your app and start seeing your changes in real time, follow the instructions below:

1. Make sure you already are logged into the desired account and using a workspace of your own;
2. Using your terminal, acess the app's directory in your local files;
3. Once in the accurate directory, type the following command in the terminal: 

`vtex link`

After that, IO performs a series of tasks on its own until the following message is displayed in the terminal, once everything is OK: `App linked successfully` 

From then on, every change can be seen in your browser in real time. But remember: the changes remain in your local files and can only be seen using the workspace you are workingon. 

If you are confortable with your changes and want to **make your changes publicly available** , verify our [documentation](https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available) for it.
