---
title: "Best practices for installing apps in live stores"
description: "Without a clear visibility of their potential impact, performing changes that directly affect your store's operation becomes extremely risky. But it doesn't have to be. Learn now the best practices to install apps in live stores."
date: "2020-04-02"
tags: ["ab-tests", "install", "apps", "best-practices"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/store/installing-apps-in-live-stores-best-practices.md"
---

# Installing apps in live stores

Once a store is live, worries and uncertainties about security, stability and performance begin to grow.

Without a clear visibility of their potential impact, performing changes that directly affect your store's operation, such as installing new apps, becomes extremely risky. **But it doesn't have to be**.

You can follow best practices to mitigate any loss your store may face - from stability to sales conversion.

Check out some of the best practices below that can and should be adhered to when installing new apps in live stores:

## Best practices

### Running A/B tests

A best practice you certainly must adopt is **A/B testing**.

On VTEX IO, A/B tests are designed entirely for **ecommerce businesses** seeking to improve their conversion rates by comparing and overlaying metrics from two different workspaces.

When installing a new app in your store, we strongly recommend you to install it in a Production workspace and then compare this workspace with the Master workspace by [running an A/B test](https://vtex.io/docs/recipes/development/running-native-ab-testing).

But note: during the A/B test configuration, it is strongly recommended that you **manually set traffic for each workspace**.

<div class="alert alert-warning">
The VTEX IO A/B test allows traffic to be directed either manually or automatically. In the latter scenario, the platform initially segments your store's total traffic and directs 50% of it to the Production workspace undergoing testing and the remaining 50% to the Master workspace. While it has considerable advantages for the store's conversion rate, automatically segmenting traffic may also pose greater operational risks by potentially impacting a greater number of users. 
</div>

### Performing manual tests

In addition to the platform's A/B test, you can also manually adopt best practices for testing new apps in Development workspaces using the `vtex link` command.

Before installing a new app in a store's Production or Master workspace, go through the steps described below:

1. Firstly, [install](https://vtex.io/docs/recipes/development/installing-an-app) the desired app in the account you are working in using a Development workspace;
2. [Link](https://vtex.io/docs/recipes/development/linking-an-app) your local files with the VTEX IO platform;
3. Access the store in which you are working from the Development workspace in which the app was installed. For example: `{developmentWorkspaceName}--{accountName}.myvtex.com`;
4. Navigate the store and test to see whether its behavior is as expected after installing the new app;
5. You can also access the store from its master workspace (`{accountName}.myvtex.com`) to check for any behavioral regression while the app is not yet installed;
6. Once all was tested, install the app in a [Production workspace](https://vtex.io/docs/recipes/development/creating-a-production-workspace);
7. Finally, [promote the Production workspace to Master](https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master) and make the new configurations public for all your users.
