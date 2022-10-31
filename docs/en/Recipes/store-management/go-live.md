# Going live with Store Framework

If you have already set up your store's [commerce features](https://help.vtex.com/tracks) and built the storefront using [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework) it is time to go live.

This article will guide you through the steps you must take to make your ecommerce available to online shoppers.

## Go live scenarios

When it comes to the VTEX ecosystem, there are a few different scenarios in which you may wish to launch a new store or storefront.

If you are Launching a new store built with Store Framework or migrating from another ecommerce platform, follow the [instructions below](#step-by-step).

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
4. [Set up DNS pointing](#step-4---set-up-dns-pointing)

> ⚠️
>
> Some of the steps below are time sensitive. Plan the complete go live process in advance taking that into consideration.

### Setp 1 - Set account edition

When developing with Store Framework, you must request the installation of the `vtex.edition-store@5.x` [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) to be able to test and go live. To do this [open a support ticket](https://help.vtex.com/en/support).

> ℹ️
>
> Once you have installed the appropriate edition app in the master [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) of your account, other workspaces you create will be created with the same edition app.

You can check the Edition app installed in a workspace by running the following command: `vtex edition get`. Please refer to [Edition apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) for further information.

### Step 2 - Register host

### Step 3 - Request internal DNS pointing

### Step 4 - Set up DNS pointing
