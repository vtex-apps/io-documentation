# VTEX IO's CLI Plugins

D️ifferent from the previous version, VTEX IO's CLI 3.x has a plugin-based architecture. With this improvement, the commands are detached from the CLI code, 
each command will have his own repository in the format `cli-plugin-COMMAND_NAME` and will be hosted by [Github](https://github.com/) on VTEX org.

See the [CLI plugin template documentation](https://github.com/vtex/cli-plugin-template) and check how to create and mantain a plugin.

## VTEX plugins settings

<details>
  <summary><span class="fa fa-lplugins">&nbsp;</span>Listing all VTEX plugins</summary>
  <br>

  To list all VTEX supported plugins, run the following command in your command line:

  ```sh
  vtex plugins source
  ```
  ![cli plugins](https://user-images.githubusercontent.com/67270558/127198123-7c5777f3-0ab2-4c2e-b5a5-188665951646.png)

  > ℹ️ If you already have downloaded a plugin, it will be highlighted in green.

  <br>
</details>

<details>
  <summary><span class="fa fa-lplugins">&nbsp;</span>Listing all downloaded plugins</summary>
  <br>

  To list all downloaded plugins, run the following command in your command line:

  ```sh
  vtex plugins list
  ```

  <br>
</details>

<details>
  <summary><span class="fa fa-iplugin">&nbsp;</span>Installing a plugin</summary>
  <br>

  To install a new plugin, run the following command in your command line:
  ```sh
  vtex plugins install plugin_name
  ```

  > in `plugin_name` insert, the name of the plugin you want to install, which which has two types of format: **VTEX** and **third parties** plugins. For VTEX commands, only use the command name from `plugins source`, i.e., `vtex plugins install infra`. 
  That way, the CLI will look for `@vtex/cli-plugin-infra` in `NPM` registry. For third parties plugins, you type `@org/plugin_name`.


  ![install-plugin](https://user-images.githubusercontent.com/67270558/127199329-914dcea3-4068-4e4f-ba89-7a2f1d43b2ad.png)

  <br>
</details>

<details>
  <summary><span class="fa fa-uplugin">&nbsp;</span>Updating all plugins</summary>
  <br>

  To update all plugins, run the following command in your command line:
  ```sh
  vtex plugins update
  ```

  ![update-plugins](https://user-images.githubusercontent.com/67270558/127201651-d44f6cb3-421f-466f-a09d-649cd1ab74b7.png)
  <br>
</details>

<details>
  <summary><span class="fa fa-dplugin">&nbsp;</span>Deleting a plugin</summary>
  <br>

  To delete a plugin, run the following command in your command line:
  ```sh
  vtex plugins delete plugin_name
  ```
  > in `plugin_name` insert, the name of the plugin you want to install, which which has two types of format: **VTEX** and **third parties** plugins. For VTEX commands, only use the command name from `plugins source`, i.e., `vtex plugins install infra`. 
  That way, the CLI will look for `@vtex/cli-plugin-infra` in `NPM` registry. For third parties plugins, you type `@org/plugin_name`.
  <br>
</details>


## Overview

Check in the following a brief description of the main plugins of VTEX IO's CLI.

|Plugin Name|Functionality|
|------------|-------------|
| [`vtex add`](#add) |Add app(s) to the manifest dependencies.|
| [`vtex autoupdate`](#vtex-autoupdate) | Update the VTEX IO'S CLI.|
| [`vtex congif get`](#vtex-config-get) |Gets the current value for the requested configuration.|
| [`vtex congif reset`](#vtex-config-reset) |Reset the requested configuration to the default value.|
| [`vtex congif set`](#vtex-config-set) |Sets the current value for the given configuration.|
| [`deps update`](#deps-update) |Updates a dependency of the current workspace. If not specified which one, it updates all dependencies.|
| [`edition get`](#edition-get) |Displays the Edition App version installed on the current account.|
| [`edition set`](#edition-set) |Sets the Edition App version for the current account.|
| [`vtex infra install`](#vtex-infra-install) |Installs an infra service.|
| [`vtex infra list`](#vtex-infra-list) |Lists installed infra services.|
| [`vtex infra update`](#vtex-infra-update) |Updates all installed infra services.|
| [`vtex lighthouse audit`](#vtex-lighthouse-audit) |Runs a Lighthouse audit over the specified URL.|
| [`vtex lighthouse show`](#vtex-lighthouse-show) |Shows a previous audit report, filtering by app and/or URL.|
| [`vtex logs`](#vtex-logs) |Shows logs of an app (only apps in production).|
| [`vtex redirects delete`](#vtex-redirects-delete) |Deletes redirects from the current account and workspace.|
| [`vtex redirects export`](#vtex-redirects-export) |Exports all redirects defined in the current account and workspace to a CSV file.|
| [`vtex redirects import`](#vtex-redirects-import) |Imports redirects from a CSV file to the current account and workspace.|
| [`vtex settings get`](#vtex-settings-get) |Prints the settings of the specified app.|
| [`vtex settings set`](#vtex-settings-set) |Sets value to the specified setting of an app.|
| [`vtex settings unset`](#vtex-settings-unset) |Disables the specified setting of an app.|
| [`vtex submit`](#vtex-submit) |Submits the current app, or an specified one, to validation from VTEX App Store team.|
| [`vtex support`](#vtex-support) |Logs in as support to another VTEX account.|
| [`vtex test e2e`](#vtex-test-e2e) |Runs E2E integration tests for the app in the current directory.|
| [`vtex test unit`](#vtex-test-unit) |Runs unit tests for the app in the current directory.|
| [`vtex url`](#vtex-url) |Prints base URL for the current account and workspace.|
| [`vtex workspace abtest finish`](#vtex-workspace-abtest-finish) |Stops all A/B tests from running on the current account.|
| [`vtex workspace abtest start`](#vtex-workspace-abtest-start) |Starts a new A/B test on the current workspace.|
| [`vtex workspace abtest status`](#vtex-workspace-abtest-status) |Displays the results of the active A/B tests.|

## Detailed reference

Check in the following the help texts for each plugin of VTEX IO's CLI. 

### add
