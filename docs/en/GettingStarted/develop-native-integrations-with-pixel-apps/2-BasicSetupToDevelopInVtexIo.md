# Setting up your development environment

Any development in the VTEX IO platform begins and ends with the **VTEX IO CLI**. 

It's the communication gateway between your VTEX store and the VTEX IO development platform, allowing you to login, install new apps on the account and manage those already installed, for example.

Follow the instructions to install VTEX IO CLI in your machine and get familiar with it accessing the [VTEX IO CLI installation and command reference](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/) documentation.

## Step 1 - Logging in to your VTEX account

Once VTEX IO’s CLI is installed, you can log in to your VTEX account by running in your terminal the following command:

```sh
$ vtex login accountName
```
>⚠️ Remember to replace `accountName` with the name of the VTEX account in which you are working.

By running the command, a browser window will open and ask for your credentials.

![toobelt-login](https://user-images.githubusercontent.com/52087100/97626236-500caa80-1a08-11eb-9abb-7e03e7fe609c.png)

## Step 2 - Creating your own workspace

When using VTEX IO, any interaction with an account happens in a [**workspace**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace/). 

It works as a version of the account in which you are logged in, in a way that any development operation done using such a workspace will be isolated, separate from other workspaces and the public version of the account itself (called Master). 

>ℹ️ If you're used to working with Git, think of workspaces as **branches**.

As you log in to a VTEX store using VTEX IO, you are automatically in its master workspace, meaning you are in the version available to the end user.

>ℹ️ To confirm this, you can run the `vtex whoami` command in your terminal to find out which **account** and **workspace** is being used by the VTEX IO CLI for your login.

To start performing the desired changes in your storefront, you will need to create a [**Development workspace**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace/). 

Use the `vtex use` command in order to start developing in the VTEX IO platform. For example:

```sh
$ vtex use exampleworkspace
```

>⚠️ Remember to replace `exampleworkspace`  with a name of your choosing that will be given to the workspace in which you will develop.

Following our example above, the command will change your login to the  `exampleworkspace` workspace if it exists. If it does not, VTEX IO CLI will create it: 

![VTEX IO CLI-workspace](https://user-images.githubusercontent.com/52087100/97626248-5438c800-1a08-11eb-9f0d-76753ef5c39a.png)

>ℹ️ The `vtex use` command makes all your operations run in the workspace specified in the command, which means you can shift your operations to Master simply by running `vtex use master` in VTEX IO CLI, for example.

## Step 3 - Accessing your store using a workspace

Having created your own development workspace in VTEX IO, you can now go to your store by accessing `https://exampleworkspace--accountName.myvtex.com`, where:

- `exampleworkspace` should be replaced with the name of the workspace that you've just created. 
- `accountName` should be replaced with the name of the VTEX account in which you are working.

>ℹ️ You can run `vtex browse` in your terminal to automatically open your browser using the workspace and account in which you are working.

Done! Your VTEX account is now connected to the VTEX IO platform and you are technically ready to start developing your Pixel app!
