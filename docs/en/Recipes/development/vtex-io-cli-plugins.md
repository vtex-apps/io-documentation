---
title: VTEX IO CLI Plugins
description: "Any development in VTEX IO begins and ends with the VTEX IO CLI, our CLI (Command Line Interface). Learn all the necessary plugins to develop in the platform."
date: "2020-07-28"
tags: ["VTEX IO CLI", "cli", "command-line-interface", "plugins", "reference"]
version: "3.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/vtex-io-cli-plugins.md"
---


# Managing plugins

VTEX IO CLI 3.x has a plug-in architecture that makes it more flexible and extensible to inject new commands and functionalities. This way, you can go beyond VTEX IO's CLI default commands and add specific plugins to achieve a more comprehensive experience.

Check the [Command Reference](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-command-reference#plugins) for a detailed description of all plugins developed by VTEX.

>ℹ️ The following plugins are native to VTEX IO'S CLI. Therefore, you do not need to install them:  `abtest`, `autoupdate`, `deploy`, `deps`, `edition`, `plugins`, `whoami`, `workspace`. 

## Checking plugin commands

Check all commands related to plugins by running the following command.

```shell
$ vtex plugins
```

![vtex-plugins-source](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/Recipes/development/Media/vtex-plugins.png)

## Listing all VTEX plugins

List all plugins available by VTEX by running the following command.

```sh
vtex plugins source
```

![vtex-plugins-source](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/Recipes/development/Media/vtex-plugins-source.png)

>ℹ️ If you already have downloaded a plugin, it will be highlighted in green.

## Installing a plugin

Install a new plugin by running the following command.

```sh
vtex plugins install {pluginName}
```

Replace the value between curly brackets with the name of the plugin you want to install. 

- For `vtex` plugins, use just the plugin name. For example, `vtex plugins install infra`. 
  
  >ℹ️ Tip: you can run `vtex plugins source` to check the available VTEX plugins.

- For third parties plugins, use the following format: `@{org-name}/{plugin-name}`.

![install-plugin](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/Recipes/development/Media/vtex-plugins-install.png)

## Listing installed plugins

List all plugins installed in your machine by running the following command.

```sh
vtex plugins list
```

![install-plugin](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/Recipes/development/Media/vtex-plugins-list.png)

## Updating installed plugins

Update all plugins installed in your machine by running the following command.

```sh
vtex plugins update
```

![update-plugins](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/Recipes/development/Media/vtex-plugins-update.png)

## Uninstalling a plugin

Delete a plugin from your machine by running the following command.

```sh
vtex plugins uninstall {pluginName}
```

>⚠️ Replace the value between curly brackets with the name of the plugin you want to uninstall. You can run `vtex plugins list` to check which plugins are installed in your machine.

![uninstall-plugins](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/Recipes/development/Media/vtex-plugins-uninstall.png)
