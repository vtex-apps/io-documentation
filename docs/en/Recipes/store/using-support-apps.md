---
title: Installing and using support apps
description: "Learn how to install apps that allow support from other VTEX accounts"
date: "01/08/2019"
tags: ["install", "installing", "app", "workspace", "support", "create"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/using-support-apps.md"
---

# Installing and using a support app

## Introduction

Sometimes you'll need help not only from VTEX agents but from another VTEX account. 
For example, a third-party vendor created an app, you installed it in your store, 
and it is not functioning correctly on your account.

Even though VTEX can help in that situation, it is best to ask for help for the
third-party vendor, since they hold the source code and are the one that have
the best product knowledge.

With support apps, it's possible for the third-party vendor to securely
login into your account and support you.

## What are support apps?

Support apps are mostly just like any other app in VTEX. They allow agents of the vendor
of that app to use pre-determined resources on your account.

What will the agents be able to use in your account is determined __inside the support app__,
and by installing it __you are agreeing that the supporter is allowed to use such resources__.

Once the support is finished, you should uninstall the app, as that __revokes their access to your account__
instantly. You can always do that to stop the support session.

__You should not leave a support app installed after the problem is solved__, as that still allows the other
vendor to access your account.

## How do I install a support App?

It is as simple as installing any other app!

![Installing a support app](https://user-images.githubusercontent.com/7110169/65991671-17487d80-e464-11e9-8c05-fb4fcf38551b.png)

Where `foobar.support-app` is the correct vendor and app name.

Uninstalling is just as easy:

![Uninstalling a support app](https://user-images.githubusercontent.com/7110169/65995982-e751a800-e46c-11e9-8447-3202eb2ecba1.png)

This revokes access from the supporter.

## How do I create a support app?

You can read further on [creating a support app here](https://vtex.io/docs/recipes/layout/creating-a-support-app).