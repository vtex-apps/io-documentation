---
title: Configuring the Sponsor Account requirements
description: "Want to publish Edition apps for child accounts? Firstly know how to configure all requirements to be a Sponsor Account."
date: "2020-03-23"
tags: ["sponsor", "sponsor-account", "requirements"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/adding-new-docs/docs/en/Recipes/development/configuring-the-sponsor-account-requirements.md"
---

# Becoming a Sponsor Account

To become a [Sponsor Account](https://vtex.io/docs/concepts/sponsor-account/), meaning to be able to release the [Edition App](https://vtex.io/docs/concepts/edition-app/) used by the child accounts, you must first check if your account meets the conditions described in the [Requirements](#Requirements) section.

In the sequence, if your account is qualified to be a Sponsor Account, you can proceed to the [Step by Step](#step-by-step) section and learn how to finally become a Sponsor Account.

## Requirements

- Have a plentiful account ecosystem. That is, to have a hierarchical relationship with other accounts. For example, it could be the main VTEX account of a holding or of a brand that has many sub-brands.
- Have a `vtex` Edition App installed in your account (`vtex.edition-business@0.x` or `vtex.edition-store@2.x`)

<div class="alert alert-warning">
<p>You can check the Edition App installed in your account by running <code>vtex edition get</code> in your terminal.</p>

<p>If you see the error <code>Message: Edition not set</code>, <a href="https://help-tickets.vtex.com/smartlink/sso/login/zendesk">open a support ticket</a> requesting the installation of either `vtex.edition-business@0.x` or `vtex.edition-store@2.x`. See <a href="https://vtex.io/docs/concepts/edition-app/">this article</a> to understand the difference between them.</p>
</div>

## Step by step

If your account meets the requirements described in the previous section, you can proceed to the following step by step.  

1. [Open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team expressing your desire to become a Sponsor Account and to develop your own Edition Apps. The VTEX team will then take the necessary measures to allow your account to sponsor others. 
2. Once you receive a successful reply from the support ticket, [deploy and release your Edition App](https://vtex.io/docs/recipes/development/configuring-an-edition-app/).
3. [Open a new ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team asking for the installation of your new Edition App in the desired accounts.

That's all! Once you receive a successful reply from your support ticket, you'll start to have child accounts, sponsored by the account you just used to develop and release your new Edition App.
