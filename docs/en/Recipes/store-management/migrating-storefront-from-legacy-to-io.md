# Migrating your storefront from Legacy CMS Portal to Store Framework

VTEX provides different storefront solutions for you to choose from, according to your operation’s needs: [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework) and [FastStore](https://www.faststore.dev/). However, there are still stores running the [Legacy CMS Portal](https://help.vtex.com/en/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/1oN446gRGcR2s70RvBCAmj).

> ℹ️
>
> Learn more about [VTEX CMS options](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z).

If your store runs with the Legacy CMS Portal, we strongly recommend migrating it to Store Framework. For implementation details, please refer to the following sections.

> ℹ️
>
> If you wish to migrate your store from another commerce platform, the instructions below do not apply. In this case, follow the steps in the [Go Live guide](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-go-live).

## Step by step

To migrate your store from Legacy CMS Portal to [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework), follow these steps:
1. [Setup workspaces](#step-1---setup-workspaces)
2. [Develop and test](#step-2---developing-and-testing-your-storefront)
3. [Go live](#step-3---going-live)

> ⚠️
>
> Consider planning the entire go-live process at least two weeks in advance, as some of the steps below are time-sensitive.

### Step 1 - Setup workspaces

[Workspaces](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) are environments isolated from one another. They can be understood as different versions of the same VTEX account.

To develop and test your store, we recommend that you create at least one [development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace) and one [production [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace). But it may be a good idea to create more workspaces according to your development needs.

> ⚠️
>
> Do not use subaccounts instead of [workspaces](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace). Doing this will cause two issues. The first is losing all Master Data information, including client profiles, for instance. Also, changes made to the project will take long to be displayed on the storefront due to cache unpredictability. This may even cause store down time when going live with the new storefront.

#### Set workspace edition

Once you have created your workspaces, [open a support ticket](https://help.vtex.com/en/support) requesting the installation of the `vtex.edition-store@5.x` [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) in the workspaces created previously. Do not forget to include the names of the workspaces you wish to use in this process.

You can check the Edition app installed in a workspace by running the following command: `vtex edition get`. Please refer to [Edition apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) for further information.

> ⚠️
>
> Do not request the Edition change for the master workspace of your store. This will make your main domain display a blank Store Framework template instead of your existing Legacy CMS Portal store.

### Step 2 - Developing and testing your storefront

At this point, it is up to your development team to plan and develop your store’s frontend experience. Check these guides to learn how to use VTEX IO to create amazing storefronts with [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework):
- [CMS IO basic concepts](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/4yB9wSl79cArd68aRBnBZ2)
- [Storefront implementation overview](https://developers.vtex.com/vtex-developer-docs/docs/storefront-implementation)
- [Storefront apps overview](https://developers.vtex.com/vtex-developer-docs/docs/store-framework-apps)
- [Building a Store Framework theme](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3)

### Step 3 - Going live

Once you have developed and tested your new storefront and everything is ready in a production workspace, it is time to go live. This means seamlessly switching the storefront being displayed to shoppers at your store’s domain. Follow these steps to accomplish this task:

1. Promote the production workspace that is running your new storefront to master. Learn more about how to [promote a workspace to master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master).
2. Request VTEX internal DNS pointing change for Store Framework via [support ticket](https://help.vtex.com/en/support). Use the ticket to schedule the change according to the information below, at least three business days before your planned go-live date. This last step will cause your new storefront to go live.

When opening the ticket, keep in mind that you must:

-  Request VTEX internal DNS pointing change only after you have promoted your production workspace to master.
- Make it clear that you wish to Go live in the title of the ticket.
- Indicate a time from 9 to 17 BRT (UTC-3) for the change to happen.
- Indicate whether or not your store has any [trade policy conditional rules](https://help.vtex.com/en/tutorial/criar-uma-politica-comercial--563tbcL0TYKEKeOY4IAgAE).
