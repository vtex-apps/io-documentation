# Going live

If you have already set up your store's [commerce features](https://help.vtex.com/tracks) and built the storefront using [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework), it is time to go live.

This article will guide you through the steps you must take to make your ecommerce available to online shoppers.

## Go live scenarios

When it comes to the VTEX ecosystem, there are a few different scenarios in which you may wish to launch a new store or storefront.

If you are launching a new store built with Store Framework or migrating from another ecommerce platform, follow the [instructions below](#step-by-step).

If you already have an active VTEX store running the [Legacy CMS Portal](https://help.vtex.com/en/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/1oN446gRGcR2s70RvBCAmj) and wish to migrate your storefront to Store Framework, see the guide on [migrating from Legacy CMS Portal to Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-migrating-storefront-from-legacy-to-io).

We do not recommend launching a new VTEX store using [Legacy CMS Portal](https://help.vtex.com/en/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/1oN446gRGcR2s70RvBCAmj). However, if that is your case, see this article on [setting up DNS pointing](https://help.vtex.com/en/tutorial/configuring-dns-pointing-to-vtex). Consider [migrating to Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-migrating-storefront-from-legacy-to-io).

> ℹ️
>
> Learn more about [VTEX CMS options](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z).

## Step by step

To go live with your VTEX store, built with [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework), follow these steps:
1. [Set account edition](#step-1---set-account-edition)
2. [Register host](#step-2---register-host)
3. [Request internal DNS pointing](#step-3---request-internal-pointing)
4. [Set up regular DNS pointing](#step-4---set-up-dns-pointing)

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

Before Setting up DNS pointing register your domain as your store's host. Learn more about how to [configure your store's host](https://help.vtex.com/en/tutorial/configuring-domains-in-license-manager--tutorials_2450).

### Step 3 - Requesting internal DNS pointing

Once you have registered your store's main domain as described above, you must request VTEX internal DNS pointing change for Store Framework via [support ticket](https://help.vtex.com/en/support). When opening your ticket keep in mind that you must:

- Make it clear that you wish to go live in the title of the ticket.
- Indicate a time from 9 to 17 BRT (UTC-3) for the internal pointing change to happen.
- Indicate whether or not your store has any [trade policy conditional rules](https://help.vtex.com/en/tutorial/criar-uma-politica-comercial--563tbcL0TYKEKeOY4IAgAE).

This process takes about three business days. Once you receive a successful reply from the support ticket, you have five days to [set up regular DNS pointing](#step-4---set-up-dns-pointing). Otherwise, your internal pointing will be automatically excluded and you will need to request it again, as described above.

### Step 4 - Setting up DNS pointing

Within five days of the confirmation of [internal DNS pointing](#step-4---set-up-dns-pointing) you must set up regular DNS pointing. To do this, follow the steps in [Setting up DNS pointing to VTEX](https://help.vtex.com/en/tutorial/configuring-dns-pointing-to-vtex--tutorials_4280).

> ⚠️ 
>
> DNS pointing propagation takes 24-48 hours to occur completely, which means that the configured address may not be accessible to all people right after configuration. 
