---
title: Configuring the Sponsor Account requirements
description: "Want to publish Edition apps for child accounts? Firstly know how to configure all requirements to be a Sponsor Account."
date: "2020-03-23"
tags: ["sponsor", "sponsor-account", "requirements"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/adding-new-docs/docs/en/Recipes/development/configuring-the-sponsor-account-requirements.md"
---

# Configuring the Sponsor Account requirements

Configuring Edition apps and defining a model for apps and configurations that need to be followed by child accounts is **only** possible if you're a [**Sponsor Account**](https://vtex.io/docs/concepts/sponsor-account/).

The are only two **prerequisites** that must be met in order for an account become a Sponsor Account of others: 
- Have a **plentiful account ecosystem**; 
- Have an **Edition App already installed** by its parent account, i.e. the account's own Sponsor Account.

As every VTEX account is necessarily a child of the `vtex` root Sponsor Account and the latter already has two published Edition Apps, any account can become a Sponsor Account simply by being part of the Sponsor Account framework. That can be done by setting one of the Editions made available by `vtex`:

 - `vtex.edition-business@0.x`
 - `vtex.edition-store@2.x`

Those Editions and the process for setting them are explained in detail below.

## Step by step

1. Using your terminal and the [VTEX IO Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), log into the account you wish to become the Sponsor of other child accounts;
2. Execute `vtex edition` to check whether any Edition is already installed on your account or not. If your account is new enough, an Edition App may have already come installed on your account creation process. If this is your case, go to the step **4**. 

In scenarios where no Edition app is installed, one of the Edition Apps available in the `vtex` registry must be manually installed by our product team. Presently, they are:

-   `vtex.edition-business@0.x`: for stores whose front-end is on VTEX's [CMS](https://help.vtex.com/tutorial/what-is-cms--EmO8u2WBj2W4MUQCS8262);
-   `vtex.edition-store@2.x`: for stores whose front-end is on VTEX IO's [Store Framework](https://vtex.io/docs/getting-started/build-stores-with-store-framework/1).

3. In case no Edition is found, [open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team asking for the most suitable Edition installment and also asking for becoming a Sponsor Account. The VTEX team will then install the suitable Edition app for you account in a Production workspace and also include your VTEX account in the Sponsor Accounts list. 

<div class="alert alert-warning">
When installing the suitable Edition App, a bundle of apps and configurations will automatically be installed in your account's <a href="https://vtex.io/docs/concepts/workspace/">Production workspace</a>. Notice that you can uninstall it, since it was set by your account's Sponsor Account (<code>vtex</code>). Then, if everything is working as expected, you can <a href="https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master/">promote the workspace to Master</a>.
</div>

<div class="alert alert-info">
If you have access to the <code>vtex</code> account, you will be able to install the Edition app that most fits to your store's account scenario using the following Toolbelt commands: <code>vtex edition set vtex.edition-store@3.x</code> or <code>vtex edition set vtex.edition-business@0.x</code>. 
</div>

4. If you already have an Edition app installed, [open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team asking for becoming a Sponsor Account. The VTEX team will then include your VTEX account in the Sponsor Accounts allowed list. 

Once the Edition is installed and the VTEX team already included your VTEX account in the Sponsor Account allowed list, your account is ready to [**configure Editions Apps**](https://vtex.io/docs/recipes/development/configuring-an-edition-app/) for its child accounts.
