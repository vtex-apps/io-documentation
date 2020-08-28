---
title: Edition App
description: "Edition app concept"
date: "2020-03-17"
tags: ["edition", "edition-app", "sponsor"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/docs/en/Concepts/edition-app.md"
---

# Edition App

An Edition App consists of a bundle of settings, policies, back- and front-end apps encapsulated and exported by a [Sponsor Account](https://vtex.io/docs/concepts/sponsor-account/).

Its main objective is to facilitate the installation of numerous apps that might be considered as essential to set up one specific environment. 

![EditionApp](https://user-images.githubusercontent.com/60782333/91470034-927c0480-e86a-11ea-866e-54575f3c0975.png)

For example, consider the two Edition Apps developed by the `vtex` account:

- The Edition Business (`vtex.edition-business@0.x`) - installs all the necessary apps to build a store with our legacy [CMS](https://help.vtex.com/en/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/6OCY6S9tqBXPD5mgpbBInC).

- The Edition Store (`vtex.edition-store@2.x`) - installs all the necessary apps to develop a store with the [Store Framework](https://vtex.io/docs/getting-started/build-stores-with-store-framework/1/).

In fact, any VTEX account that meets the [requirements needed to be a Sponsor Account](https://vtex.io/docs/recipes/development/becoming-a-sponsor-account/) can develop and release their own Edition Apps.

Hence, besides the fundamental development environment set up by a `vtex` native Edition App, it's possible to extend an Edition App by creating a new and customized one that meets your account family needs. 

Notice that this is especially useful for complex account families, such as the ones under the same brand or holding.

<div class="alert alert-info">
To change the Edition App installed in an account, you must <a href ="https://help-tickets.vtex.com/smartlink/sso/login/zendesk">open a support ticket</a>. This is required to avoid critical issues that could be caused by its misconfiguration.
</div>

It's important to be aware that, despite the inherited apps - such as the ones from the `vtex` Editions, an Edition App can only contain apps exclusively developed by the same account responsible for the development of that Edition.

Also, keep in mind that, once exported, the apps and configurations that an Edition App includes cannot be changed by the sponsored accounts that had it installed. That means that only the Sponsor Account is authorized to perform modifications in the apps exported by its Edition App, but requiring, in the following, a new release of its Edition.

Summing up, by encapsulating all the necessary settings, policies, back-, and front-end apps, an Edition App provides all the essential functionalities to set up one desired environment.
