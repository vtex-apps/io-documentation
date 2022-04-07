# A/B testing Legacy and IO store versions
In this guide, you will learn how to perform A/B testing between store workspaces in CMS Legacy and VTEX IO to confirm which workspace has the highest conversion rate for your store.

## Before you start
1. [Install the VTEX IO Command-line Interface (CLI)](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference). Through the CLI, you can log in to your VTEX account, manage workspaces and develop new apps.

2. Ensure that you already have a Development workspace for your account. Otherwise, create and set up one following [Creating a Development workspace in IO for a CMS legacy store](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-development-workspace-for-cms-legacy) guide.

3. Ensure that your Development workspace has the `vtex.edition-store@3.x` Edition app installed. Run the `vtex edition get` in your terminal to verify the Edition App version installed on the current account. Otherwise, [Open a ticket to the VTEX support team](https://help-tickets.vtex.com/smartlink/sso/login/zendesk?_ga=2.222513819.1487123273.1647865109-1001456323.1619912759) requesting the installation of the `vtex.edition-store@3.x` Edition app in the new Development workspace.


## Step-by-step 

1. Using your terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference), log into your VTEX account by running the following command:

```
vtex login {account-name}
```
> ℹ️       
> 
> Remember to replace the value between the brackets for the VTEX account name you desire. For example: `vtex login account-name`.


2. Access the Development workspace that you have created by running:
```
vtex use {workspace} 
```
> ℹ️      
> 
> Remember to replace the value between the brackets for the Development workspace you desire. For example: `vtex login test`.

3. Run the `vtex use Master` command in your terminal to perform the steps below in the Master workspace. The Master workspace must be set to the `vtex.edition-business@0.x` [edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app).

4. Install the `vtex.colossus-legacy-proxy@@1.8.9-hkignore` app. This is an essential step to avoid that you store in production break. 

>⚠️ 
> 
> The app’s version must be `vtex.colossus-legacy-proxy@@1.8.9-hkignore`. If not, the store won’t respond to the request.

5. [Open a ticket to the VTEX support team](https://help-tickets.vtex.com/smartlink/sso/login/zendesk?_ga=2.222513819.1487123273.1647865109-1001456323.1619912759) requesting the redirection of the production workspace to be rendered in VTEX IO

>⚠️ 
> 
> If the store has a different storefront for mobile, inform this in the ticket to the VTEX support.

6. Once the Production workspace is rendering in the VTEX IO, you can enable the A/B test between the workspaces described in the [Running native A/B tests](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing) step-by-step.

### Validating if the A/B test is running

1. To ensure that the A/B test is working, make a GET response in the following API:

`http://platform.io.vtex.com/{{account}}/_abtest/parameters`

> ⚠️
>
> The Header must have `VtexIdclientAutCookie` from the account you want to get the information. For example: `VtexIdclientAutCookie: {{VtexIdclientAutCookie}}`

2. The result should be similar to the following:

```
"master": {
            "A": 9000,
            "b": 1
        },
        "wsio": {
            "A": 1000,
            "b": 1
        }

```
The result means that the `master` is with 90% of the traffic and the `wsio` is with 10%.

## Next Step    
After finishing the A/B test and want to migrate your store to IO, [open a ticket to the VTEX support team](https://help-tickets.vtex.com/smartlink/sso/login/zendesk?_ga=2.222513819.1487123273.1647865109-1001456323.1619912759)  requesting the migration of your Development workspace to the IO.
