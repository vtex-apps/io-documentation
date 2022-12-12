# Going live with a new store

This article will guide you through the steps you must take to make your ecommerce available to shoppers if it was developed with Store Framework. To get a complete overview of the go-live process for any VTEX store, see this [Go-live guide](https://help.vtex.com/tracks/go-live-your-store--4Ns5FxIiksmjsdX2yOTduM/1iP90RcJvlrfQhnlxM54wo).

> ℹ️
>
> The steps below also apply if you are migrating your store from another ecommerce platform. You can also learn about how to [migrate your storefront from the Legacy CMS Portal to CMS Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-migrating-storefront-from-legacy-to-io).

## Before you start

There are a few things you must check to make sure you are ready to go live.
- [Account edition](#account-edition)
- [Storefront development](#storefront-development)

### Account edition

You must set your account edition to develop a storefront in Store Framework. If your storefront is ready, it is very likely you already have the correct [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) installed. You can check the Edition app installed in any given workspace by running the following command in your terminal: `vtex edition get`. Please refer to [Edition apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) for further information.

If you do not have the appropriate Edition app installed, open a [support ticket](https://help.vtex.com/en/support) requesting the installation of the `vtex.edition-store@5.x` [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) in your `master` [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace).

> ℹ️
>
> Once the Store Edition is installed in the master [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) of your account, all new workspaces you create will use this same Edition app. Other workspaces that existed previously will remain with the [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) they already had.

### Storefront development

You must develop your storefront before going live. Check these guides to learn how to use VTEX IO to create amazing storefronts with [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework):
- [CMS IO basic concepts](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/4yB9wSl79cArd68aRBnBZ2)
- [Storefront implementation overview](https://developers.vtex.com/vtex-developer-docs/docs/storefront-implementation)
- [Storefront apps overview](https://developers.vtex.com/vtex-developer-docs/docs/store-framework-apps)
- [Building a Store Framework theme](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3)

## Step by step

To go live with your VTEX store, built with [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework), follow these steps:
1. [Register host](#step-1---registering-the-store's-domain)
2. [Request internal DNS pointing](#step-2---requesting-internal-dns-pointing)
3. [Set up regular DNS pointing](#step-3---setting-up-dns-pointing)

> ⚠️
>
> Consider planning the entire go-live process at least two weeks in advance, as some of the steps below are time-sensitive.

### Step 1 - Registering the store's domain

To launch your store, you must own a [domain name](https://en.wikipedia.org/wiki/Domain_name). If you have not already, you can buy one from a domain provider.

[Configure your domain as your store's host](https://help.vtex.com/en/tutorial/configuring-domains-in-license-manager--tutorials_2450) as presented in this guide to make sure that shoppers will be directed to your new VTEX store.

### Step 2 - Requesting internal DNS pointing

VTEX provides different [storefront solutions](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z). This step ensures that the domain you [registered as your VTEX host](#step-1---registering-the-store's-domain) points users to the storefront built with Store Framework.

Request VTEX internal DNS pointing change for Store Framework via [support ticket](https://help.vtex.com/en/support). When opening your ticket keep in mind that you must:

- Make it clear that you wish to go live in the title of the ticket.
- Indicate a time from 9 to 17 BRT (UTC-3) for the internal pointing change to happen.
- Indicate whether or not your store has any [trade policy conditional rules](https://help.vtex.com/en/tutorial/criar-uma-politica-comercial--563tbcL0TYKEKeOY4IAgAE).

This process takes about three business days. Once you receive a successful reply from the support ticket, you have five days to [set up regular DNS pointing](#step-3---setting-up-dns-pointing).

### Step 3 - Setting up DNS pointing

Within five days of the confirmation of [internal DNS pointing](#step-2---requesting-internal-dns-pointing) you must set up regular DNS pointing.  Otherwise, your internal pointing will be automatically excluded and you will need to request it again, as described above.

Unlike the previous step, regular DNS pointing must be set up by you and guarantees that your domain points to VTEX so that the platform can deliver your storefront to shoppers.

To do this, follow the instructions in [Setting up DNS pointing to VTEX](https://help.vtex.com/tracks/go-live-your-store--4Ns5FxIiksmjsdX2yOTduM/12bQlMbJ68Ot0LIaO6Btkj).

> ⚠️ 
>
> DNS pointing propagation takes 24-48 hours to occur completely, which means that the configured address may not be accessible to all people right after configuration. 
