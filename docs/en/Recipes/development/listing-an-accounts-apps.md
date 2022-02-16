---
title: Listing an account’s apps
description: "List all account's apps running a single VTEX IO CLI command"
date: "10/18/2019"
tags: ["list", "listing", "account", "apps", "account-app"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/listing-an-accounts-apps.md"
---

# Listing an account’s apps 

While developing in an account, we should be aware of all its installed or linked apps. With VTEX IO CLI, access to the app list is made easy by running a single command.

## Step by step

1. Using your terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installment-and-command-reference#command-reference), log into the desired account;
2. Once logged in, run the following command:

`vtex list`

VTEX IO CLI will then display a table containing the account’s installed and linked apps, in addition to their respective version, as shown in the example below: 

![listing-apps](https://user-images.githubusercontent.com/52087100/67044546-dfe3fd00-f102-11e9-83d7-936f229b7b26.png)

<div class=“alert alert-warning”>
Note that the table is divided into apps related to an <b>Edition</b>, apps independently <b>installed</b> and <b>linked</b> apps.
</div>


