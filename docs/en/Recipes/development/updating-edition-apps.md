---
title: Updating Edition apps
description: "Publish a new version of an Edition app and learn how it us updated in each child account."
date: "2020-03-23"
tags: ["update", "updating", "edition", "edition-apps", "sponsor", "sponsor-account"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/adding-new-docs/docs/en/Recipes/development/updating-edition-apps.md"
---

# Updating Edition apps

After an [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) is [configured](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-configuring-an-edition-app), you can launch new versions of it, either by **defining new required apps for child accounts** or by **changing the Edition initial settings**.

To do this, follow the walk-through below:

## Step by step

1. Using a code editor of your preference, open the Edition App folder and access the `apps.json` file;
2. Make the desired apps and settings changes in the file;

>⚠️ In a scenario in which an app that is already installed on the account is added to the Edition, the type of installation of that app will become `edition` and it can no longer be removed from the accounts or undergo any changes in major version since it is now enforced by the Edition. In the same way, removing apps from the `apps.json` will automatically uninstall them from all child accounts with this Edition. If an removed app is still needed in some of the child accounts, it will need to be manually and individually installed again in each desired child account.

3. Save and commit your changes;
4. [Publish and deploy](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app) the new Edition version.

After the new version is published, **the Edition is automatically updated in all accounts by Housekeeper**. This automatic update is done asynchronously, periodically and individually in each child account.

Notice that **Housekeeper only updates an Edition version as long as the major has not been changed**, meaning it is not a breaking change for the child accounts consuming that Edition. 

In case bumping the major version is necessary due to the changes performed, the Edition update must be made manually and individually for each child account as well.

>ℹ️ In addition to updating the Edition itself, Housekeeper is also responsible for enforcing to child accounts all required apps exported by the Edition. This means that you don't have to worry about installing the new apps defined by the edition, as Housekeeper will do the job for you when the Edition App is updated.