# Basic setup to develop in VTEX IO

You may not realize it, but once you've implemented [**VTEX Store Framework**](https://vtex.io/docs/introduction/what-is-vtex-store-framework/) in your store, you'll be developing in [VTEX IO](https://vtex.io/docs/introduction/what-is-vtex-io/) on a certain scale.

That's because **our e-commerce components are in fact native apps to the VTEX IO development platform**. In practice this means that you'll need to install such apps and configure them in order to properly function on your storefront.

## Step 1 - Installing the VTEX IO Toolbelt

Any development in the VTEX IO platform begins and ends with the **Toolbelt**, our CLI (Command Line Interface). 

It's the communication gateway between your VTEX store and the VTEX IO development platform, allowing you to login, install new apps on the account and manage those already installed, for example.

Follow the instructions to install Toolbelt in your machine and get familiar with it accessing the [VTEX IO CLI installation and command reference](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/) documentation.

## Step 2 - Logging in to your VTEX account

Once VTEX IO’s CLI is installed, you can log in to your VTEX account using your terminal the following command to connect to the platform (replacing `{account}`  with the name of the VTEX account in which you are working):

```sh
$ vtex login {account}
```

By running the command, a browser window will open and ask for your credentials.

## Step 3 - Creating your own workspace

When using VTEX IO, any interaction with an account happens in a [workspace](https://vtex.io/docs/concepts/workspace/). 

It works as a version of the account in which you are logged in, in a way that any development operation done using such a workspace will be isolated, separate from other workspaces and the public version of the account itself (called Master). 

<div class="alert alert-info">
  If you're used to working with GitHub, think of workspaces as <strong>branches</strong>.
</div>

As you log in to a VTEX store using VTEX IO, you are automatically in its master workspace, meaning you are in the version available to the end user.

To confirm this, you can run the `vtex whoami` command in your terminal to find out which **account** and **workspace** is being used by Toolbelt for your login: 

![toolbelt-whoami](https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png)

To start performing the desired changes in your storefront, we will need to create a [Development workspace](https://vtex.io/docs/recipes/development/creating-a-development-workspace/). 

Use the `vtex use` command in order to start configuring Store Framework in your store. For example:

```sh
$ vtex use examplename
```

*Remember to replace* `examplename`  *with a name of your choosing that will be given to the workspace in which you will develop.*

Following our example, the command will change the login to the  `examplename` workspace if it exists. If it does not, Toolbelt will create it: 

![workspace-examplename EN](https://user-images.githubusercontent.com/52087100/63979000-30899300-ca8e-11e9-9d9d-234e31ac45f7.png)
 
<div class="alert alert-info">
The <code>vtex use</code> command makes all your operations run in the workspace specified in the command, which means you can shift your operations to Master simply by running <code>vtex use master</code> in Toolbelt, for example.
</div>

## Step 4 - Accessing your store using a workspace

Having created your own development workspace in VTEX IO, you can now go to your store by accessing `https://{workspace}--{account}.myvtex.com`, where `{workspace}` should be replaced with the name of the workspace that you've just created and `{account}` with the name of the VTEX account in which you are working.

<div class="alert alert-info">
<strong>Tip</strong>: you can simply run <code>vtex browse</code> in your terminal to automatically open your browser using the workspace and account in which you are working.
</div>

Done! Your store is now connected to the VTEX IO platform and you are technically ready to implement the VTEX Store Framework!


