---
title: Creating and using a support app
description: "Learn how to create and use apps to support other vendors"
date: "01/08/2019"
tags: ["create", "creation", "app", "creating", "publish", "support"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store/using-support-apps.md"
---

# Creating and using a support app

If you're an VTEX app developer, it is good to know that support apps exist.
They empower you to actually login and browse your clients' accounts to give support to them.
Their user experience will be a breeze: check out [how to install a support app](https://vtex.io/docs/recipes/layout/creating-a-support-app).

It is of good practice to already have a support app for your clients to install
in case you publish an app. That way, it'll be easy to debug and support your clients
if the app does not work in their workspace environment.

## Initializing a support app

Initializing a support app is just as easy as initializing a regular app.  
There is an option inside `vtex init` to create a `support app`.

## Customizing your support app

Inside your new `hello-support` folder, there'll be a `support/support.json` file.
You'll encounter a JSON-formatted list of matches of __roles__ and __policies__.

The __role__ should be an uniquely identifiable name, like the examples show. Each
different role can have different policies attached. The purpose of this is to
enable complex support to the supporter: for simpler cases, you may choose to assume
a role less 'powerful' than a case where the client's store is down.

Nevertheless, if a user installs your support app, __all__ the roles declared in the JSON
are authorized to login into the other account. This may change in the future.

The __policies__ are the same type of policies that you'd find in a `manifest.json` in
another app: a set of policies that allow the user to do or not do actions in the client's
account. For example, `read-workspace-apps` allow you to run `vtex ls` inside their account.

Now, remember to [publish your app](https://vtex.io/docs/recipes/layout/publishing-an-app) so that
others can install it!

## Using your support app

Once a client has installed your app, you have access to login to their account
__while the app is installed__. If at any time the user uninstalls the support app,
your privileges are revoked.

To login into another account as support, use the toolbelt:

![Logging in as support](https://user-images.githubusercontent.com/7110169/66005173-11ad6080-e481-11e9-99b4-b6a0b4a1816f.png)

And there you go! You're logged in to your client's account.

## Navigating the admin logged in as support

Should you need to browse the client's admin in the support session, the toolbelt's handy command
`vtex browse admin` will do all the work of authorization inside the other account's admin.
As a general tip -- it works even if you're not on a support session. `vtex browse <endpoint>` will
always bring you to your store at the desired endpoint. It has an added bonus of working
at remote support session!
