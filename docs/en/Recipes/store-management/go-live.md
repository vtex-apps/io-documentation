# Going live with a new store

If you have already set up your store's [commerce features](https://help.vtex.com/tracks) and built the storefront using [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework), it is time to go live.

This article will guide you through the steps you must take to make your ecommerce available to online shoppers.

> ℹ️
>
> The steps below also apply if you are migrating your store from another ecommerce platform.

## Step by step

To go live with your VTEX store, built with [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework), follow these steps:
1. [Set account edition](#step-1---setting-the-edition-app)
2. [Register host](#step-2---registering-the-store's-domain)
3. [Request internal DNS pointing](#step-3---requesting-internal-dns-pointing)
4. [Set up regular DNS pointing](#step-4---setting-up-dns-pointing)

> ⚠️
>
> Consider planning the entire go-live process at least two weeks in advance, as some of the steps below are time-sensitive.

### Step 1 - Setting the Edition app

Open a [support ticket](https://help.vtex.com/en/support) requesting the installation of the `vtex.edition-store@5.x` [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) in your `master` [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace).

> ℹ️
>
> Once the Store Edition is installed in the master [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) of your account, all new workspaces you create will use this same Edition app. Other workspaces that existed previously will remain with the [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) they already had.

You can check the Edition app installed in any given workspace by running the following command in your terminal: `vtex edition get`. Please refer to [Edition apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) for further information.

### Step 2 - Registering the store's domain

To launch your store, you must own a [domain name](https://en.wikipedia.org/wiki/Domain_name). If you have not already, you can buy one from a domain provider.

[Configure your domain as your store's host](https://help.vtex.com/en/tutorial/configuring-domains-in-license-manager--tutorials_2450) as presented in this guide to make sure that shoppers will be directed to your new VTEX store.

### Step 3 - Requesting internal DNS pointing

VTEX provides different [storefront solutions](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z). This step ensures that the domain you [registered as your VTEX host](#step-2---registering-the-store's-domain) points users to the storefront built with Store Framework.

Request VTEX internal DNS pointing change for Store Framework via [support ticket](https://help.vtex.com/en/support). When opening your ticket keep in mind that you must:

- Make it clear that you wish to go live in the title of the ticket.
- Indicate a time from 9 to 17 BRT (UTC-3) for the internal pointing change to happen.
- Indicate whether or not your store has any [trade policy conditional rules](https://help.vtex.com/en/tutorial/criar-uma-politica-comercial--563tbcL0TYKEKeOY4IAgAE).

This process takes about three business days. Once you receive a successful reply from the support ticket, you have five days to [set up regular DNS pointing](#step-4---setting-up-dns-pointing).

### Step 4 - Setting up DNS pointing

Within five days of the confirmation of [internal DNS pointing](#step-3---requesting-internal-dns-pointing) you must set up regular DNS pointing.  Otherwise, your internal pointing will be automatically excluded and you will need to request it again, as described above.

Unlike the previous step, regular DNS pointing must be set up by you and guarantees that your domain points to VTEX so that the platform can deliver your storefront to shoppers.

To do this, follow the instructions in [Setting up DNS pointing to VTEX](https://help.vtex.com/en/tutorial/configuring-dns-pointing-to-vtex--tutorials_4280).

> ⚠️ 
>
> DNS pointing propagation takes 24-48 hours to occur completely, which means that the configured address may not be accessible to all people right after configuration. 
