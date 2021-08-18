---
title: VTEX IO CLI command reference
description: "Any development in VTEX IO begins and ends with the Toolbelt, our CLI (Command Line Interface). Learn all the necessary commands to develop in the platform."
date: "2020-04-04"
tags: ["toolbelt", "cli", "command-line-interface", "commands", "reference"]
version: "3.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/vtex-io-cli-command-reference.md"
---

# Command reference

## Overview

Check in the following a brief description of the main commands of VTEX IO's CLI.

|Command Name|Functionality|
|------------|-------------|
| [`autoupdate`](#autoupdate) |	Update the VTEX IO'S CLI.|
| [`browse`](#browse) |Opens the URL relative to your current workspace and account in a new browser window.|
| [`deploy`](#deploy) | Publishes an app as a stable version. Only works for apps previously published as a release candidate version.|
| [`deprecate`](#deprecate) |Deprecates the specified app, uninstalling and downgrading it to the latest stable version in every VTEX account.|
| [`deps diff`](#deps-diff) |Displays the differences between the dependencies of two distinct workspaces.|
| [`deps list`](#deps-list) |Displays the complete dependency tree of the current workspace.|
| [`deps update`](#deps-update) |Updates a dependency of the current workspace. If not specified which one, it updates all dependencies.|
| [`edition get`](#edition-get) |Displays the Edition App version installed on the current account.|
| [`edition set`](#edition-set) |Sets the Edition App version for the current account.|
| [`help`](#help) |Displays help for VTEX CLI commands.|
| [`init`](#init) |Copies starting files and folders from VTEX boilerplates into your local directories.|
| [`install`](#install) | Installs an app on the current workspace. If not specified which one, it defaults to the app in the current directory.| 
| [`link`](#link) |Syncs the app in the current directory with the development workspace in use.|
| [`list`](#list)| Lists the apps installed on the current workspace and account.|
| [`local token`](#local-token) |Prints the user's auth token and copies it to the clipboard. |
| [`login`](#login) |Logs in to a VTEX account.|
| [`logout`](#logout) |Logs out of the current VTEX account.|
| [`publish`](#publish) | Publishes the app in the current directory as a release candidate version. |
| [`release`](#release) |(Only for git users.) Bumps the app version, commits, and pushes to remote the app in the current directory.|
| [`setup`](#setup) |Sets up typings and tools for the current development environment.|
| [`switch`](#switch) |Switches to another VTEX account.|
| [`undeprecate`](#undeprecate) |Reestablishes a deprecated version of an app as a stable version.|
| [`uninstall`](#uninstall) |Uninstalls an app from the current account and workspace.|
| [`unlink`](#unlink) |Unlinks an app from the current workspace.|
| [`update`](#update) |Updates all installed apps to the latest (minor or patch) version. Does not upgrade to another major version.|
| [`whoami`](#whoami) |Prints the current account, workspace, environment, and login details.|
| [`workspace abtest finish`](#workspace-abtest-finish) |Stops all A/B tests from running on the current account.|
| [`workspace abtest start`](#workspace-abtest-start) |Starts a new A/B test on the current workspace.|
| [`workspace abtest status`](#workspace-abtest-status) |Displays the results of the active A/B tests.|
| [`workspace delete`](#workspace-delete) |Deletes one or many workspaces from the current account.|
| [`workspace list`](#workspace-list) |Lists all workspaces of the current account.|
| [`workspace promote`](#workspace-promote)|Promotes the current workspace to master. Only works for production workspaces|
| [`workspace reset`](#workspace-reset) |Cleans all configurations of the specified workspace and recreates it with the configurations from master.|
| [`workspace status`](#workspace-status) |Displays information about the specified workspace.|
| [`workspace use`](#workspace-use) |Creates and switches to a new workspace or simply switches to an existing one.|


## Detailed reference

Check in the following the help texts for each command of VTEX IO's CLI. You can also access this information in your terminal by adding `--help` or `-h` after the command name.

### Autoupdate

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-autoupdate`. See more details about plugins on [VTEX IO's CLI plugins]().

Update the VTEX IO'S CLI.

#### Usage

```shell
  $ vtex autoupdate [CHANNEL]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**CHANNEL** (optional)|.|

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### browse

Opens the URL relative to your current workspace and account in a new browser window.

#### Usage

```shell
  $ vtex browse [PATH]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**PATH** (optional)|Relative path from `https://{workspace}--{account}.myvtex.com/`.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--qr**|-q|Prints a QR Code on the terminal.|
  
#### Examples

```shell
  vtex browse
  vtex browse admin
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>


### deploy

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-deploy`. See more details about plugins on [VTEX IO's CLI plugins]().

Publishes an app as a stable version. Only works for apps previously published as a release candidate version [see vtex publish --help].

#### Usage

```shell
  $ vtex deploy [APPID]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**APPID** (optional)|Name and version of the app you want to deploy.|

#### Options

|Option|Alias|Description|
|------|-----|-----------|
|**--yes**|-y|Answers yes to all prompts.|
|**--force**|-f|(Use with caution.) Ignores the testing period of 7 minutes after publishing an app.|

#### Examples

```shell
  vtex deploy
  vtex deploy vtex.service-example@0.0.1
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### deprecate

Deprecates the specified app, uninstalling and downgrading it to the latest stable version in every VTEX account.

#### Usage

```shell
  $ vtex deprecate [APPID] [ITHAPPID]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**APPID** (optional)|Name and version of the app (`{vendor}.{appname}@{x.x.x}`) to deprecate.|
|**ITHAPPID** (optional)|Names and versions of the multiple apps (`{vendor}.{appname}@{x.x.x}`) to deprecate.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--yes**|-y|Answers yes to all prompts.|

#### Examples

```shell
  vtex deprecate
  vtex deprecate vtex.service-example@0.0.1
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### deps diff

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-deps`. See more details about plugins on [VTEX IO's CLI plugins]().

Displays the differences between the dependencies of two distinct workspaces. If a single parameter is passed, the specified workspace's dependencies are compared with the master's. If no parameter is passed, the diff is made between the current workspace and master.

#### Usage

```shell
  $ vtex deps diff [WORKSPACE1] [WORKSPACE2]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**WORKSPACE1** (optional)|First workspace for comparison.|
|**WORKSPACE2** (optional)| [default: master] Second workspace for comparison.|

#### Example

```shell
  vtex deps diff workspace1 workspace2
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### deps list

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-deps`. See more details about plugins on [VTEX IO's CLI plugins]().

Displays the complete dependency tree of the current workspace.

#### Usage

```shell
  $ vtex deps list
```

#### Options

|Option|Alias|Description|
|------|-----|-----------|
|**--keys**|-k|Shows only key dependencies.|
|**--npm** |-n|Includes dependencies from the npm registry.|
  

#### Alias

```shell
  $ vtex deps ls
```

#### Examples

```shell
  vtex deps list
  vtex deps ls
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### deps update

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-deps`. See more details about plugins on [VTEX IO's CLI plugins]().

Updates a dependency of the current workspace. If not specified which dependency, it updates all of them.

#### Usage

```shell
  $ vtex deps update [APPID] [ITHAPPID]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**APPID** (optional)|Name and version of the app (`{vendor}.{appname}@{x.x.x}`) to update.|
|**ITHAPPID** (optional)|Names and versions of the multiple apps (`{vendor}.{appname}@{x.x.x}`) to update.|

#### Examples

```shell
  vtex deps update
  vtex deps update vtex.service-example@0.0.1
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### edition get

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-edition`. See more details about plugins on [VTEX IO's CLI plugins]().

Displays the Edition App version installed on the current account.

#### Usage

```shell
  $ vtex edition get
```

#### Example

```shell
  vtex edition get
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### edition set

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-edition`. See more details about plugins on [VTEX IO's CLI plugins]().

Sets the Edition App version for the current account.

#### Usage

```shell
  $ vtex edition set EDITION
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**EDITION**|Name of the Edition App to install.|

#### Example

```shell
  vtex edition set editionName
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### help

Displays help for VTEX CLI commands.

#### Usage

```shell
  $ vtex help [COMMAND]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**COMMAND** (optional)|Command to show help about.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--all**|-|Displays all commands available in the CLI.|

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### init

Copies starting files and folders from VTEX boilerplates into your local directories.

#### Usage

```shell
  $ vtex init
```

#### Example

```shell
  vtex init
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### install

Installs an app on the current workspace. If not specified which one, it defaults to the app in the current directory.

#### Usage

```shell
  $ vtex install [APPID] [ITHAPPID]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**APPID** (optional)|Name and version of the app (`{vendor}.{appname}@{x.x.x}`) to install.|
|**ITHAPPID** (optional)|Names and versions of the multiple apps (`{vendor}.{appname}@{x.x.x}`) to install.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--force**|-f|Installs the specified app without checking for route conflicts.|
  
#### Examples

```shell
  vtex install
  vtex install vtex.service-example@0.x
  vtex install vtex.service-example@0.0.1
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### link

Syncs the app in the current directory with the development workspace in use.

#### Usage

```shell
  $ vtex link
```

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--account=account**|-a|Starts a development session in the specified account. Must be paired with the '--workspace' flag.|
|**--clean**|-c|Cleans builder cache.|
|**--setup**|-s|Sets up typing definitions before linking the app [see vtex setup --help].|
|**--unsafe**|-u|Allows linking the app despite Typescript errors.|
|**--workspace=workspace**|-w|Starts a development session in the specified workspace. Can be paired with the '--account' flag to switch from the current account and workspace.|
|**--no-watch**|-|Doesn't watch for file changes after the initial link.|  

#### Example

```shell
  vtex link -a youraccount -w yourworkspace
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### list

Lists the apps installed on the current workspace and account.

#### Usage

```shell
  $ vtex list
```

#### Aliases

```shell
  $ vtex ls

```

#### Examples

```shell
  vtex list
  vtex ls
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### local token

Prints the user's auth token and copies it to the clipboard.

#### Usage

```shell
  $ vtex local token
```

#### Example

```shell
  vtex local token
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### login

Logs in to a VTEX account.

#### Usage

```shell
  $ vtex login [ACCOUNT]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**ACCOUNT** (optional)|Account name to log in.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--workspace=workspace**|-w|Logs in the specified workspace.|

#### Examples

```shell
  vtex login
  vtex login storecomponents
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### logout

Logs out of the current VTEX account.

#### Usage

```shell
  $ vtex logout
```

#### Example

```shell
  vtex logout
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### publish

Publishes the app in the current directory as a release candidate version.

#### Usage

```shell
  $ vtex publish
```

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--force**|-f|Publishes the app independently of SemVer rules.|
|**--tag=tag**|-t|Adds the specified tag to the release.|
|**--workspace=workspace**|-w|Uses the specified workspace in the app registry.|
|**--yes**|-y|Answers yes to all prompts.|
  

#### Example

```shell
  vtex publish
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### release 

(Only for git users.) Bumps the app version, commits, and pushes to remote the app in the current directory.

#### Usage

```shell
  $ vtex release [RELEASETYPE] [TAGNAME]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**RELEASETYPE** (optional)|Release type (major, minor, or patch).|
|**TAGNAME** (optional)|Tag name (e.g., stable, beta).|

#### Examples

```shell
  vtex release
  vtex release patch
  vtex release patch beta
  vtex release minor stable
  vtex release pre
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### setup

Sets up typings and tools for the current development environment.

#### Usage

```shell
  $ vtex setup
```

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--ignore-linked**|-i|Sets up types from published apps, and ignores types from linked apps.|
|**--all**|-|Sets up all available typings, configs, and tools.|
|**--tooling**|-|Sets up Prettier, Husky, and ESLint.|
|**--tsconfig**|-|Sets up React and Node TSconfig, if applicable.|
|**--typings**|-|Sets up GraphQL and React typings.|

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### switch

Switches to another VTEX account.

#### Usage

```shell
  $ vtex switch ACCOUNT
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**ACCOUNT**|Account name to log in.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--workspace=workspace**|-w|Moves to the specified workspace.|
  
#### Examples

```shell
  vtex switch storecomponents
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### undeprecate

Reestablishes a deprecated version of an app as a stable version.

#### Usage

```shell
  $ vtex undeprecate [APPID] [ITHAPPID]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**APPID** (optional)|Name and version of the app (`{vendor}.{appname}@{x.x.x}`) to undeprecate.|
|**ITHAPPID** (optional)|Names and versions of the multiple apps (`{vendor}.{appname}@{x.x.x}`) to undeprecate.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--yes**|-y|Answers yes to all prompts.|

#### Example

```shell
  vtex undeprecate vtex.service-example@0.0.1
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### uninstall

Uninstalls an app from the current workspace. If not specified which app to uninstall, it defaults to the app in the current directory.

#### Usage

```shell
  $ vtex uninstall [APPNAME] [ITHAPPNAME]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**APPNAME** (optional)|Name and version of the app (`{vendor}.{appname}@{x.x.x}`) to uninstall.|
|**ITHAPPNAME** (optional)|Names and versions of the multiple apps (`{vendor}.{appname}@{x.x.x}`) to uninstall.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--yes**|-y|Answers yes to all prompts.|

#### Examples

```shell
  vtex uninstall
  vtex uninstall vtex.service-example
  vtex uninstall vtex.service-example@0.x
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### unlink

Unlinks an app from the current workspace. If not specified which app to unlink, it defaults to the app in the current directory.

#### Usage

```shell
  $ vtex unlink [APPID] [ITHAPPID]
```

appname Name of the app to unlink.

#### Arguments

|Argument|Description|
|--------|-----------|
|**APPID** (optional)|Name and version of the app (`{vendor}.{appname}@{x.x.x}`) to unlink.|
|**ITHAPPID** (optional)|Names and versions of the multiple apps (`{vendor}.{appname}@{x.x.x}`) to unlink.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--all**|-a|Unlinks all apps.|

#### Examples

```shell
  vtex unlink
  vtex unlink vtex.service-example@0.x
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### update

Updates all installed apps to the latest (minor or patch) version. Does not upgrade to another major version.

#### Usage

```shell
  $ vtex update
```

#### Example

```shell
  vtex update
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### whoami

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-whoami`. See more details about plugins on [VTEX IO's CLI plugins]().

Prints the current account, workspace, environment, and login details.

#### Usage

```shell
  $ vtex whoami
```

#### Example

```shell
  vtex whoami
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### Workspace abtest finish

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-abtest.`. See more details about plugins on [VTEX IO's CLI plugins]().

Stop all AB testing in current account.

#### Usage

```shell
  $ vtex workspace abtest finish
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### Workspace abtest start

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-abtest.`. See more details about plugins on [VTEX IO's CLI plugins]().

Start AB testing with current workspace.

#### Usage

```shell
  $ vtex workspace abtest start
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### Workspace abtest status

>ℹ️ This command refers to the plugin `@vtex/cli-plugin-abtest.`. See more details about plugins on [VTEX IO's CLI plugins]().

Display currently running AB tests results.

#### Usage

```shell
  $ vtex workspace abtest status
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### workspace delete

Deletes one or many workspaces from the current account.

#### Usage

```shell
  $ vtex workspace delete WORKSPACE1 [ITHWORKSPACE]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**WORKSPACE1**|Name of the workspace to delete.|
|**ITHWORKSPACE** (optional)|Name of the multiple workspaces to delete.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--force**|-f|Deletes the specified workspace even if it is currently in use.|
|**--yes**|-y|Answers yes to all prompts.|

#### Examples

```shell
  vtex workspace delete workspaceName
  vtex workspace delete workspaceName1 workspaceName2
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### workspace list

Lists all workspaces of the current account.

#### Usage

```shell
  $ vtex workspace list
```

#### Aliases
  
```shell
  $ vtex workspace ls

```

#### Examples

```shell
  vtex workspace list
  vtex workspace ls
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### workspace promote

Promotes the current workspace to master. Only works for production workspaces.

#### Usage

```shell
  $ vtex workspace promote
```

#### Aliases
  
```shell
  $ vtex promote

```

#### Examples

```shell
  vtex workspace promote
  vtex promote
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### workspace reset

Cleans all configurations of the specified workspace and recreates it with the configurations from master.

#### Usage

```shell
  $ vtex workspace reset [WORKSPACENAME]
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**WORKSPACENAME** (optional)|Name of the workspace to reset.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--production**|-p|Recreates the workspace as a production one.|
|**--yes**|-y|Answers yes to all prompts.|
  
#### Examples

```shell
  vtex workspace reset
  vtex workspace reset workspaceName
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### workspace status

Displays information about the specified workspace.

#### Usage

```shell
  $ vtex workspace status [WORKSPACENAME]

```

#### Arguments

|Argument|Description|
|--------|-----------|
|**WORKSPACENAME** (optional)|Name of the workspace.|

#### Example

```shell
  vtex workspace status
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>

### workspace use

Creates and switches to a new workspace or simply switches to an existing one.

#### Usage

```shell
  $ vtex workspace use WORKSPACE
```

#### Arguments

|Argument|Description|
|--------|-----------|
|**WORKSPACE**|Name of the workspace to use.|

#### Options

|Option|Alias|Description|
|-------|-----|-----------|
|**--production**|-p|Creates and/or switches to a production workspace.|
|**--reset**|-r|Resets the workspace before switching to it.|

#### Aliases

```shell
  $ vtex use
```

#### Examples

```shell
  vtex workspace use workspaceName
  vtex use workspaceName
```

<div align="right"> 🔼 <a href="#overview">Back</a></div>


  > ℹ️ VTEX IO's CLI 3.x now has a plugin-based architecture and the following commands from the previous version were detached from the CLI and transformed into plugins:
  `@vtex/cli-plugin-add`, `@vtex/cli-plugin-autoupdate`, `@vtex/cli-plugin-config`, `@vtex/cli-plugin-debug`, `@vtex/cli-plugin-infra`, `@vtex/cli-plugin-lighthouse`, `@vtex/cli-plugin-logs`, `@vtex/cli-plugin-redirects`, `@vtex/cli-plugin-settings`, `@vtex/cli-plugin-submit`, `@vtex/cli-plugin-support`, `@vtex/cli-plugin-test`, `@vtex/cli-plugin-url`.
    To Learn more about, check out [VTEX IO's CLI plugins]().
