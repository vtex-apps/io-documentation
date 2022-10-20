# Migrating your storefront from Legacy CMS Portal to Store Framework

VTEX provides different storefront solutions for you to choose from, according to your operation’s needs: Legacy CMS Portal and Store Framework. Learn more about [VTEX CMS options](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z).

If your store is already running with the Legacy CMS Portal, but you wish to use Store Framework features, it is possible to migrate it. In this guide, you will learn how to do this step by step.

## Step by step

To migrate your store from Legacy CMS Portal to [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework), follow these steps:
1. [Setup workspaces](#setup-workspaces)
2. [Develop and test](#develop-and-test)
3. [Go live](#go-live)

### Setup workspaces

[Workspaces](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) are environments isolated from one another. They can be understood as different versions of the same VTEX account.

To develop and test your store, we recommend that you create at least one [development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace) and one [production [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace). But it may be a good idea to create more workspaces according to your development needs.

#### Set workspace edition

Once you have created your workspaces, you must request the setting of the workspaces’ [edition apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app) to `vtex.edition-store@5.x`.

To do that, [open a support ticket](https://help.vtex.com/en/support) asking for the edition change. Do not forget to include the names of the workspaces you wish to use in this process.

You can confirm a given workspace’s edition by running the command `vtex edition get`. Learn more about [edition apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app).

> ⚠️
>
> Do not request the edition change for the master workspace of your store. This will make it so that your main domain displays a blank Store Framework template instead of your existing Legacy CMS Portal store.

### Step 2 - Developing and testing your storefront

At this point, it is up to your development team to plan and develop your store’s frontend experience. Check these guides to learn how to use VTEX IO to create amazing storefronts with [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-store-framework):
- [CMS IO basic concepts](https://help.vtex.com/tracks/cms--2YcpgIljVaLVQYMzxQbc3z/4yB9wSl79cArd68aRBnBZ2)
- [Storefront implementation overview](https://developers.vtex.com/vtex-developer-docs/docs/storefront-implementation)
- [Storefront apps overview](https://developers.vtex.com/vtex-developer-docs/docs/store-framework-apps)
- [Building a Store Framework theme](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3)

### Step 3 - Going live

Once you have developed and tested your new storefront and everything is ready in a production workspace, it is time to go live. This means seamlessly switching the storefront being displayed to shoppers at your store’s domain. Follow these steps to accomplish this task:

1. Promote the production workspace that is running your new storefront to master. Learn more about how to [promote a workspace to master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master).
2. Request VTEX internal DNS pointing change for Store Framework via [support ticket](https://help.vtex.com/en/support). Use the ticket to schedule the change at least three business days in advance during business hours.

> ⚠️
>
> Request VTEX internal DNS pointing change only after you have promoted your production workspace to master.
