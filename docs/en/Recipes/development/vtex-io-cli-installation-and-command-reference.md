---
title: VTEX IO CLI installation and command reference
description: "Any development in VTEX IO begins and ends with the Toolbelt, our CLI (Command Line Interface). Learn now how to install it in your terminal and all needed command to development in the platform."
date: "2020-03-23"
tags: ["toolbelt", "cli", "command-line-interface", "commands", "install", "installation"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/adding-new-docs/docs/en/Recipes/development/vtex-io-cli-installation-and-command-reference.md"
---

# VTEX IO CLI installation and command reference

Any development in VTEX IO begins and ends with the **Toolbelt**, our CLI (Command Line Interface). 

Toolbelt allows you to login to a desired VTEX account, link your local files to the platform, manage an account's workspaces, in addition to performing any action necessary to your development process.

## Installation

To install the VTEX IO’s CLI, you need to ensure that [Node.js](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) are installed on your machine. 

Thereafter, type `yarn global add vtex` in your computer’s terminal.

```sh
$ yarn global add vtex
```

<div class="alert alert-info">
To confirm that the installation occurred as expected, you can execute the <code>vtex</code> command. This should display all available commands in a help text. 
</div>

### Troubleshooting

After installing and running `vtex` in the terminal, an error saying that the command or program wasn't found may show up. 

This happens due to an error concerning the Yarn installation. The `yarn global add` command does not properly add Yarn binaries to a directory known by your terminal as `PATH`.

By not adding the Yarn binaries to terminal `PATH`, Yarn and its programs can't be found, thereby resulting in an error when running Toolbelt. 

#### Workaround for MacOS and Linux users

1. In your local directories, find the Profile file. It is usually hidden and is named after the command line's interpreter. For example: If you're using `bash`, your Profile file will be named `bashrc`. If you use `zsh`, it will be `zshrc`;
2. Once in the Profile file, add the following command: `export PATH=$PATH:$(yarn global bin)`;
3. Log in and log out of your terminal for the changes to take effect; 

<div class="alert alert-info">  
If your command line Shell is Fish, you can ignore the step by step above. Simply run the following command in your terminal: <code>set -U fish_user_paths (yarn global bin) $fish_user_paths</code>.
</div>

#### Workaround for Windows users

1. Runs the `yarn global bin` command in your terminal. It will return the path in which the yarn global binaries were saved; 
2. Copy it to your clipboard. This path now must be added to the Windows Environment Variable Path;
3. Click on the windows button and search for environment. Then, click on `Edit the system environment variables`;
4. In the `System Properties` dialog, click on the `Environment Variables...` button;
5. In `User Variables`, select `Path` and then click on the `Edit...` button;
6. Click on the `New` button to add a new path to the search;
7. Paste the yarn global binary path copied in step 2 and click `OK` when prompted. This will save your changes;
8. Log in and log out of your terminal for the changes to take effect. 

If the error persists, don't hesitate to [send a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to our support team.  

## Command Reference

**Every** command executed in Toolbelt must begin with `vtex`, irrespective of its name, as can be seen in the examples in the command table below. 

| Command Name  | Functionality | Example | 
|--------------------|---------|----|
|  `add` | Adds an app to the dependencies of the app you are currently working on. | `vtex add vtex.store-header@2.x` |
| `browse` | Opens an endpoint in a browser window based on the current logged in account, workspace and environment data. | `vtex browse` |
| `deploy` | Publishes an app as a stable version. It only works in apps already published as a release candidate version. | `vtex deploy vtex.modal-layout@0.1.1` |
| `deprecate` | Deprecates an app's version. | `vtex deprecate vtex.store-components@3.104.2` |
| `deps list` | Lists the apps dependencies of the workspace in which you are working. | `vtex deps list`| 
| `deps update` | Updates all app dependencies of the workspace in which you are working or a single app dependency (when specified). | `vtex deps update` or `vtex deps vtex.product-summary@2.52.0` | 
| `deps diff` | Compares app dependencies list of two workspaces and lists the apps that appear in both.  | `vtex deps diff workspace1  workspace2` |
| `edition` | Gets the edition of the account you are logged in. | `vtex edition` | 
| `edition set` | Sets an edition for the account you are logged in. | `vtex edition set vtex.edition-store@2.x` | 
| `init` | Displays a list with boilerplate files or directories for new VTEX apps. | `vtex init`| 
| `install` | Installs an app to the account you are logged into. |  `vtex install vtex.store-drawer@0.8.0` | 
| `link` | Locally links the app directory you are working into the development workspace you are working on. | `vtex link` |
| `list`| Lists all VTEX apps running in the account you are logged into. | `vtex list` |
| `local account` | Displays the account name you are logged into and copies it to the clipboard. | `vtex local account` | 
| `local workspace` | Displays the workspace name you are working in and copies it to the clipboard. | `vtex local workspace`| 
| `local token` | Displays the user's authentication token current being used and copies it to the clipboard. | `vtex local token`|
| `promote` | Promotes the production workspace you are working in to Master. | `vtex workspace promote` | 
| `publish` | Publishes the app as a release candidate version. | `vtex publish vtex.menu@2.23.1` or `vtex publish`  | 
| `redirects import` | Adds a URL redirect into the account and workspace you are logged into. | `vtex redirects import {fileName}.csv` |
| `redirects export` | Gets existing redirects from the account and workspace you are logged into. | `vtex redirects export {fileName}.csv`|
| `redirects delete` | Deletes redirects in the the account and workspace you are logged into. | `vtex redirects delete {urlPath}` |
| `release` | Only for git users. When executed in the app's directory, it releases the app's new version in the `manifest.json` file according to SemVer (semantic versioning) best practices, updates the `CHANGELOG.md` file, assigns commit tags and sends the performed changes to the app's repository.  | `vtex release major beta` | 
| `support` |  Logs you into an account using a support role. | `vtex support storecomponents` | 
| `test` | Runs the app's **unit tests** according to the directory you are in (in case the app has any tests already configured for it). | `vtex test`| 
| `undeprecate` | Reverts an app's deprecation. | `vtex undeprecate vtex.store-components@3.104.2` |
| `uninstall` | Uninstalls an app from the account you are logged into. | `vtex uninstall vtex.menu@2.23.1` | 
| `unlink` | Unlinks the app directory you are in from the development workspace you are working in. | `vtex unlink` |  
| `update` | Update all installed apps to the latest version in the account you are logged into (valid only for patches and minors, Majors are not updated when using this command). | `vtex update` |
| `url` | Displays a complete URL in the terminal, based on the current logged in account, workspace and environment data. | `vtex url` |
