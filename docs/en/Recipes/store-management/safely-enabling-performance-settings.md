---
title: Safely enabling performance settings
description: "A common worry among us all: website performance. Check out how to how to safely enable performance settings in your store and benefit from a fast store."
date: "2020-11-11"
tags: ["enable", "practices", "guideline", "performance", "sales-conversion", "site"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/safely-enabling-performance-settings.md"
---

# Safely enabling performance settings

We understand that *site performance* is a common concern among e-commerce stores since it directly impacts the number of visited pages, sales conversion rate, user session time, bounce rate, and more.

Thus, to help you guarantee the success of your brand's online presence, we'll teach you, in the following step by step, how to test and implement our [recommendations for optimizing your store's performance](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-best-practices-for-optimizing-performance).

## Step by step

## Step 1: Applying changes on a production workspace

1. Using the terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/), log in to the desired account by running `vtex login {account}`.
2. Run the command `vtex use {productionWorkspace}` to create and use a **new** [Production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace/).

>⚠️ Remember to replace the values between the curly braces according to your scenario.

3. Using your browser, access the account's admin relative to that workspace.
4. From the account's admin panel, go to _Store Setup > CMS > Store > Advanced_.
5. Now, considering our documentation on [Best practices for optimizing performance](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-best-practices-for-optimizing-performance), activate the desired features, and save the changes.
6. Access your store in the current workspace that you're working in and check if the performance improvements were applied.

>ℹ️ Keep in mind that it might take some time before some changes are applied.

## Step 2: Testing and analyzing performance

1. Review and test all the main pages of your store, making sure that the changes didn't cause any side-effects, such as style inconsistencies or undesired behaviors.
2. Access [Google PageSpeed Insights.](https://developers.google.com/speed/pagespeed/insights)
3. Using the following URL pattern: `https://{account}.myvtex.com/?workspace={productionWorkspace}`, check your store's performance in the production workspace you're currently working.

>⚠️ Using the standard URL pattern `https://{workspace}--{account}.myvtex.com/` won't show the performance score of your store in the specified workspace. Thus, keep in mind: to analyze performance in a workspace, **you must use the `?workspace={productionWorkspace}` query string** as shown in Step 2.3.

>ℹ️ Before promoting your workspace to master, we recommend that you measure the performance improvements by comparing the performance score in the production and the master workspace.

## Step 3: Making your changes publicly available 

If you're happy with the results obtained in the previous steps, run `vtex promote` to promote your workspace and to benefit from a faster store.
