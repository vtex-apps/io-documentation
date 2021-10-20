---
title: Installing VTEX IO's CLI
description: "Any development in VTEX IO begins and ends with the Toolbelt, our CLI (Command Line Interface). Learn now how to install it in your terminal."
date: "2021-07-15"
tags: ["toolbelt", "cli", "command-line-interface", "install", "installation"]
version: "3.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/vtex-io-cli-install.md"
---

# Installing VTEX IO's CLI

According to your operating system, take the following steps to install VTEX IO’s CLI on your machine.

<details>
  <summary><span class="fa fa-apple">&nbsp;</span>MacOS</summary>
  <br>

1. Go to the **Homebrew** [page](https://brew.sh/index).
2. Copy the command below **Install Homebrew**.

![brew](https://files.readme.io/7a812a5-Screen_Shot_2021-04-20_at_19.49.25.png)

```sh
$ /bin/bash -c “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)”
```

3. Open a terminal by typing `Command + Space` and typing` terminal`.

4. In your terminal, paste the **Homebrew** command and hit `Return` (Enter).

5. Now, **install VTEX IO'S CLI** by running the following command:

```sh
brew tap vtex/vtex
brew install vtex
```

<br>
</details>

<details>
  <summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

For Linux, you will use the standalone install, a tarball with a binary that contains its own `node.js` binary.

>ℹ️ Before the installation, check if you have the command-line tool and library, [curl](https://curl.se/).

Open your command line and run the following command to install **VTEX IO'S CLI**:

```sh
curl -L https://vtex.io/vtexcli/install | sh
```


<br>
</details>

<details>
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

1. Download the appropriate installer for your Windows.

**Installer for Windows**

<a href="https://vtex.io/vtexcli/install/win-x64" style="text-decoration:none;"
        class="vtex-landing-button vtex-header-hero-y-margin rebel_pink_background">64-bit installer</a>
<br>
<a href="https://vtex.io/vtexcli/install/win-x32" style="text-decoration:none;"
          class="vtex-landing-button vtex-header-hero-y-margin rebel_pink_background">32-bit installer</a>
<br>      

2. Open the downloaded file and follow the instructions to finish the installation process.

<br>
</details>

## Installing VTEX IO's CLI by NPM

Since VTEX IO's CLI is built with [Node.js](https://nodejs.org/en/), you can manually install it via [npm](https://www.npmjs.com/package/vtex). This method is recommended only for environments in which auto-updating VTEX IO's CLI is not ideal.

>⚠️ ***We strongly recommended that you use an alternative installation method.***
> *If you opt for installing VTEX IO's CLI using npm, keep in mind that VTEX IO's CLI won't be automatically updated, and the Node version on your machine might conflict with the one used by the CLI developers. Notice that if you opt for any other installation method, VTEX IO's CLI will always be up-to-date, and you will avoid installation issues.*

>ℹ️  Before the installation, check if you have [Node.js](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) installed on your machine.

<details>
  <summary><span class="fa fa-apple">&nbsp;</span>MacOS</summary>
  <br>

1. Go to the **Homebrew** [page](https://brew.sh/index).
2. Copy the command below **Install Homebrew**.

![brew](https://files.readme.io/7a812a5-Screen_Shot_2021-04-20_at_19.49.25.png)

```sh
$ /bin/bash -c “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)”
```

3. Open a terminal by typing `Command + Space` and typing` terminal`.

4. In your terminal, paste the **Homebrew** command and hit `Return` (Enter).

5. After the Homebrew installation is finished, run the following command:

  ```sh
  brew install node
  ```

6. Now, **install Yarn** by running 
  
  ```sh
  brew install yarn
  ```

7. And finally, install **VTEX IO's CLI** by running:

  ```sh
  yarn global add vtex
  ```



<br>
</details>

<details>
  <summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

1. Install **Node.js** by running the following command: 
   
  ```sh
  sudo apt install nodejs
  ```

2. Install **Yarn** by following the [Yarn installation](https://classic.yarnpkg.com/en/docs/install#gentoo-stable) for Linux.
3. Install VTEX IO's CLI by running the following command:

```sh
$ sudo yarn global add vtex
```


<br>
</details>

<details>
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

1. Download and install **Node.js** as described on this [document](https://nodejs.org/pt-br/download/).
2. Download and install **Yarn** as described on this [document](https://classic.yarnpkg.com/en/docs/getting-started).
3. Open the CMD by pressing the Windows key and typing `cmd`.
4. Install VTEX IO's CLI by running the following command.

```sh
$ yarn global add vtex
```

<br>
</details>
 

## Verifying the installation

To confirm that the installation occurred as expected, run the following command to check all default commands available in VTEX IO's CLI.

```sh
vtex
```

![vtex](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/Recipes/development/Media/vtex-command.png)

### Troubleshooting

If VTEX IO's CLI is not behaving as expected, run `vtex --version` to make sure you're using the [latest version](https://github.com/vtex/toolbelt/blob/3.x/CHANGELOG.md) available. If not, consider [updating](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-update) it.

In case the problem persists, check the following directions.

<details>
  <summary><code>Error: Cannot find module 'vtex'</code></summary>
  <br>

  This error is related to commands detached from the VTEX IO's CLI base code (i.e., [plugins](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-vtex-io-cli-plugins)). 

  Even though plugins are decoupled from VTEX IO's CLI, they rely on the CLI functionalities. Therefore, this error signalizes that these plugins are failing to access VTEX IO's CLI functionalities.

  To solve this problem, you will need to create a [symlink](https://en.wikipedia.org/wiki/Symbolic_link) from `{vtex-folder}/node_modules/vtex` to `{vtex-folder}/`.

  Creating a symlink:

  <details style="padding-left:30px">
    <summary><span class="fa fa-apple">&nbsp;</span> MacOS</summary>
  <br>

  *Brew*

  ```
  ln -s /usr/local/Cellar/vtex/2.119.2/libexec /usr/local/Cellar/vtex/2.119.2/libexec/node_modules/vtex
  ```

  <br>
  </details>
  <br>
  <details style="padding-left:30px">
  <summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
  <br>

  *Standalone*

  ```
  ln -s /usr/local/lib/vtex /usr/local/lib/vtex/node_modules/vtex
  ```

  <br>
  </details>
  <br>
  
If the error persists, don't hesitate to [open a support ticket.](https://help-tickets.vtex.com/smartlink/sso/login/zendesk)