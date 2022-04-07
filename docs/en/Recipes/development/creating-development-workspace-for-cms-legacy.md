# Creating a Development workspace for a Legacy CMS store
In this guide, you will learn how to create a Development workspace to start developing in an IO environment. 

When working in a Development workspace, the public version of your store, that is, the one that is visible to end users, will stay stable utilizing the CMS Legacy until you are ready to transition to IO.
## Before you Start
1. [Install the VTEX IO Command-line Interface (CLI)](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference). Through the CLI, you can log in to your VTEX account, manage workspaces and develop new apps.

2. Ensure that you understand the concepts of [VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-io) and [workspaces](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace).
## Step-by-step
1. Using your terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference), log into your VTEX account by running the following command:

```
vtex login {account-name}
```
>  ℹ️        
> 
> Remember to replace the value between the brackets for the VTEX account name you desire. For example: `vtex login account-name`.

2. Create a [new Development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace).

3. [Open a ticket to the VTEX support team](https://help-tickets.vtex.com/smartlink/sso/login/zendesk?_ga=2.222513819.1487123273.1647865109-1001456323.1619912759) requesting the installation of the `vtex.edition-store@3.x` Edition app in the new Development workspace.

> ℹ️ 
> 
> The `vtex.edition-store@3.x` Edition app is responsible for enabling building elements for the front-end using the VTEX Store Framework. You can only configure and test the solution successfully after installing it.

Once the `vtex.edition-store@3.x` Edition app is installed in the Development workspace, configure the Store Framework theme you want in the Store Theme app and test it in the new Development workspace. Refer to the [Setting your store's theme](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-3-settingyourstoretheme) documentation for more details.

## Next steps
1. Make sure to configure the Store theme for the Development workspace you have created. Refer to the [Setting your store's theme](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-3-settingyourstoretheme) documentation for more details.


2. After finishing setting your Store Theme, perform A/B testing between the Development workspace in IO and the Master workspace in the CMS legacy. Refer to the [Performing A/B testing between store versions in CMS and VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-performing-ab-testing-between-legacy-and-io) guide.
