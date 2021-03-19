# Basic development setup in VTEX IO

Any development in VTEX IO begins and ends with the [**VTEX IO CLI**](https://vtex.io/docs/concepts/toolbelt/) (Command Line Interface), that works as a communication gateway between your VTEX account and the VTEX IO development platform. 

Using the CLI, you will be able to log in to your VTEX account, manage workspaces, develop apps, and install new ones.

## Installing VTEX IO's CLI

To install VTEX IO’s CLI, you need to ensure that [Node.js](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) are properly installed on your machine. 

To follow all the required steps for installing VTEX IO's CLI, access our documentation on [VTEX IO CLI Installation and Command Reference](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/).

## Logging in to your VTEX account

Once VTEX IO’s CLI is installed, log in to your VTEX account with the following command:

```sh
$ vtex login {account}
```

This will open a browser window asking for your credentials.

>⚠️ Replace `{account}` with the name of your VTEX account.

Once you are logged in, run the `vtex whoami` command to show which **VTEX account** and **workspace** are being used by the VTEX IO CLI. 

![VTEX IO CLI - whoami](https://user-images.githubusercontent.com/52087100/61886028-517e2780-aed5-11e9-9398-b6d2f3909a50.png)

## Creating your own workspace

When using VTEX IO, any development must happen in a [**workspace**](https://vtex.io/docs/concepts/workspace/). 

A workspace works as a GitHub branch in the sense that any development operation is done in a specific workspace that is separate from others. This means that workspaces allow you to develop and test your changes without any risk of interfering with live apps or with the work of other developers.

To start developing, you have to [create a **Developer workspace**](https://vtex.io/docs/recipes/development/creating-a-development-workspace/) in your VTEX account. When you log in, you are automatically using the Master workspace, which means you are in the version available to the end user. 

Run the `vtex use` command in your terminal as shown below:

```sh
$ vtex use {examplename}
```

This changes your VTEX account to a Development workspace called `examplename`, creating it from scratch if it does not already exist.

![workspace-examplename EN](https://user-images.githubusercontent.com/52087100/63979000-30899300-ca8e-11e9-9d9d-234e31ac45f7.png)

Having logged in to your account and created your own Development workspace, you are ready to begin developing your React app and building your storefront using VTEX IO.
