---
title: Workspace
description: "Workspace concept"
date: "2020-04-09"
tags: ["workspace"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-1/docs/en/Concepts/workspace.md"
---

# Workspace

Workspaces are environments isolated from one another. They can be understood as different versions of the same VTEX account. In practice, this means that changes performed in your own workspace do not affect your store's live version or other developers' work.

>ℹ️ If you're used to working with git, think of workspaces as branches.

There are two main types of workspaces:

- **Development workspace** - provides more development freedom: allows [linking](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app), [installing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-installing-an-app), and [publishing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app) apps. It can't handle production traffic, be promoted to master, nor be used for A/B testing.
- **Production workspace** - supports production traffic, can be [promoted to master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master) and used for [A/B testing](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing). Linking apps is forbidden.

Workspaces are accessible at `https://{workspace}--{account}.myvtex.com`.

There's also the **Master workspace**, a unique production workspace that reflects the content served to the store's end-user.

![Workspaces](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Concepts/Media/workspace.png?raw=true)