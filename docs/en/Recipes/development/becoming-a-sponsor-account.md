---
title: Becoming a Sponsor Account
description: "Want to publish Edition apps for child accounts? Firstly know how to configure all requirements to be a Sponsor Account."
date: "2020-03-23"
tags: ["sponsor", "sponsor-account", "requirements"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/becoming-a-sponsor-account.md"
---

# Becoming a Sponsor Account

To become a [Sponsor Account](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-sponsor-account) and be able to manage apps and configurations across multiple accounts with [Edition Apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app), you must first check if your account meets the conditions described in the [Prerequisites](#prerequisites) section.

If your account is qualified to be a Sponsor Account, follow the [Step by Step](#step-by-step) section to activate this behavior on your account.

## Prerequisites

To be eligible to become a Sponsor account, make sure you have:

- Access to three or more accounts related to the same group or holding.
- An Edition App published by `vtex` installed on your account (`vtex.edition-business@0.x` or `vtex.edition-store@2.x`).

  >ℹ️ You can check the Edition App installed on your account by running `vtex edition get` in your terminal. If you see the following error `Message: Edition not set`, [open a support ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) requesting the installation of either the `vtex.edition-business@0.x` or `vtex.edition-store@2.x`. See [Edition App](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) for more information.

## Step by step

If your account meets the prerequisites described in the previous section, take the following steps to become a Sponsor Account.  

1. [Open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team expressing your desire to become a Sponsor Account and develop your own Edition Apps. Remember to include the following information in your ticket:
    - The name of the main account.
    - The names of the accounts that the main account will sponsor.
   
    The VTEX team will evaluate your request and take the necessary measures to allow your main account to sponsor others. 
2. Once you receive a successful reply from the support ticket, you must [create, deploy and release your Edition App](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-configuring-an-edition-app).
3. [Open a new ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team asking for the installation of your new Edition App on the desired accounts.

Once you receive a successful reply from your support ticket, you'll be able to have child accounts sponsored by the account you just used to develop and release your new Edition App.

## Related resources

- [Edition Apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app)
- [Sponsor Account](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-sponsor-account)
