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

5. After the Homebrew installation is finished, run the command `brew tap vtex/vtex`.

6. Now, **install VTEX IO'S CLI** by running.

```sh
 brew install vtex
```

<br>
</details>

<details>
  <summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

For Linux, you will use the standalone install, a tarball with a binary that contains its own `node.js` binary.

>ℹ️ Before the installation, check if you have the command-line tool and library, [curl](https://curl.se/).

Open your command line and run the following command to **VTEX IO'S CLI**:

```sh
curl -L https://vtex.io/vtexcli/install | sh
```


<br>
</details>

<details>
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

For Windows you can install it via Windows installer or [Chocolatey](https://chocolatey.org/).

* **Installer for Windows**

  <a href="https://vtex.io/vtexcli/install/win-x64" style="text-decoration:none;"
        class="vtex-landing-button vtex-header-hero-y-margin rebel_pink_background">VTEX Setup</a>

1. Once downloaded, got to the folder where the VTEX Setup was downloaded and open it on your machine.
2. To finish the installation process, follow the instructions described on it.

* **Chocolatey**
1. Download and install **Chocolatey** as described on this [link](https://chocolatey.org/install).
2. Once Chocolatey is set up, run the following command from the command line:

```sh
choco install vtex
```


<br>
</details>

## Installing VTEX IO's CLI by NPM

The CLI is built with [Node.js](https://nodejs.org/en/) and is installable via [`npm`](https://www.npmjs.com/package/vtex). This method is recommended only for environments in which auto-updating VTEX IO's CLI is not ideal.

>⚠️ *We strongly recommended that you use an alternative installation method from the previous section, [Installing VTEX IO's CLI](#installing-vtex-ios-cli). Since the proper version of Node.js is already included in the other methods and it does not conflict with any other version on your system.*

>ℹ️ Notice that, to install VTEX IO's CLI, you need to ensure that [Node.js](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) are installed on your machine.
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

5. After the Homebrew installation is finished, run the command `brew install node`.

6. Now, **install Yarn** by running `brew install yarn`.

7. And finally, install **VTEX IO's CLI** by running:

```sh
$ yarn global add vtex
```



<br>
</details>

<details>
  <summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

1. Install **Node.js** using the following command: `sudo apt install nodejs`.
2. Install **Yarn** following the [Yarn installation](https://classic.yarnpkg.com/en/docs/install#gentoo-stable) for Linux.
3. Open your command line and run the following command.

```sh
$ sudo yarn global add vtex
```


<br>
</details>

<details>
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

1. Download and install **Node.js** as described on this [link](https://nodejs.org/pt-br/download/).
2. Download and install **Yarn** as described on this [link](https://classic.yarnpkg.com/en/docs/getting-started).
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
  <details style="padding-left:30px">
    <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
  <br>

  *Chocolatey*

  ```
  New-Item -ItemType SymbolicLink -Path 'C:\Program Files\vtex\client\node_modules\vtex' -Target 'C:\Program Files\vtex\client'    
  ```

  <br>
</details>
  
If the error persists, don't hesitate to [open a support ticket.](https://help-tickets.vtex.com/smartlink/sso/login/zendesk)
