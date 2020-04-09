---
title: Workspace
description: "Workspace concept"
date: "2020-04-09"
tags: ["workspace"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Concepts/workspace.md"
---

# Workspace

Workspaces are, as the name suggests, **work spaces isolated from one another**. 

A workspace works as a version of the account, in a way that any development operation is done in a specific workspace, separate from others. If you're used to working with `git`, think of workspaces as branches.

This means that you can test your changes without any risk of interfering with live apps or with the work of other developers.

There are three types of workspaces in the platform:

- [**Development workspace**](https://vtex.io/docs/recipes/development/creating-a-development-workspace/) - Environment where you can link, develop, install and publish apps. It is a workspace in which you have more configuration freedom, but it cannot handle production level traffic, be promoted to master nor used for A/B testing.
- [**Production workspace**](https://vtex.io/docs/recipes/development/creating-a-production-workspace/) - Environment that handles production level traffic, can be used for A/B testing and can be [promoted to become the `master` workspace](https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master/). It can also have apps installed, but app links for development are not allowed.
- **Master workspace** - Unique `production` workspace in which the content reflects what is served to the store's end user. It should only be altered when you are positively certain that your code is production ready.
