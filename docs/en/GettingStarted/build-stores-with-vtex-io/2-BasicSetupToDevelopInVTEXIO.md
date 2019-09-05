# Basic setup to develop in VTEX IO

Any development in VTEX IO beings with the **Toolbelt**, our CLI (Command Line Interface) that allows you to login, develop new apps and manage already installed ones.

## VTEX IO Toolbelt

To install VTEX IO’s CLI, you need to ensure that [Yarn](https://yarnpkg.com/) is installed on your machine. 

Thereafter, type `yarn global add vtex` in your computer’s terminal.

```
$ yarn global add vtex
```

<div class="alert alert-info">
To confirm that the installation occurred as expected, you can execute the `vtex` command. This should display all available commands in a help text. 
</div>

## Login

Once VTEX IO’s CLI is installed, you can login to your VTEX account with the following command: 

```
$ vtex login {VTEXaccount}
```

> `{VTEXaccount}` should be replaced with the name of the VTEX account in which you are working 

This would in turn open a browser window asking for your credentials.

When you are logged in, you can use the `vtex whoami` command to uncover which **account** and **workspace** is being used by the terminal. 

[toolbelt-whoami](https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png)

## Creating your own workspace

When using VTEX IO, any interaction with an account happens in a **workspace**. As you log into a store, you are automatically in its master workspace, meaning you are in the version available to the end user. Therefore, always remember to create a development workspace using the `vtex use` command whenever you want to test a new configuration. 

```
$ vtex use {examplename}
```

This changes your Toolbelt to a so-called `examplename` workspace and creates it if it doesn’t already exist.

[workspace-examplename EN](https://user-images.githubusercontent.com/52087100/63979000-30899300-ca8e-11e9-9d9d-234e31ac45f7.png)

<div class="alert alert-warning">
<code>vtex use</code> makes all your operations run in the workspace set in the command, which means you can shift your operations to Master simply by executing <code>vtex use master</code> in Toolbelt, for example.
</div>

Having created your own development workspace, you can go to your store by accessing:

`https://{workspace}-{account}.myvtex.com`

Where `{workspace}` is the workspace that you've just created and `{account}` is the name of the account in which you are working.

<div class="alert alert-info">
<strong>Tip</strong>: you can simply run <code>vtex browse</code> in your terminal to automatically open your browser on the <code>https://{workspace}-{account}.myvtex.com</code> URL.
</div>

Done! You can begin developing your store in VTEX IO.
