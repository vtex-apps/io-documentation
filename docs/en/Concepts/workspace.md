---
title: Workspace
description: "Workspace concept"
date: "2020-04-09"
tags: ["workspace"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Concepts/workspace.md"
---

# Workspace

Workspaces are environments isolated from one another. They can be understood as different versions of the same VTEX account. In practice, changes performed in a particular workspace do not affect your store's live version or other developers' work.

>ℹ️ If you're used to working with git, think of workspaces as branches.

There are three main types of workspaces:

- **Development workspace** - is mainly used by software developers to draft, build or extend VTEX IO apps and storefront themes. These workspaces provide more development freedom. They allow [linking](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app), [installing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app), and [publishing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app) VTEX IO apps. They can't handle production traffic, be promoted to master, nor be used for A/B testing.
- **Production workspace** - is mainly used by the quality assurance and development teams to validate VTEX IO apps. These workspaces support production traffic and can be used for [A/B testing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing), but linking apps is forbidden. If desired, these workspaces can be [promoted to master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master) to become publicly available for all end-users.
- **Master workspace** - a **unique** production workspace that reflects the content served to the end-users of a store.

Development and production workspaces can be accessed at `https://{workspace}--{account}.myvtex.com`.

![Workspaces](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Concepts/Media/workspace.png?raw=true)
