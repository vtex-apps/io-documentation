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

>If you installed VTEX IO'S CLI via `npm`, make sure to update it by running `yarn global add vtex` in your terminal.
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

For Linux, you will use the standalone install, a tarball with a binary that contains its own node.js binary.

>ℹ️ Before the installation, check if you have the command line tool and library, [curl](https://curl.se/).

Open your command line and run the following command to **VTEX IO'S CLI**:

```sh
curl -L https://vtex.io/vtexcli/install | sh
```


<br>
</details>

<details>
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

For Windows you can install it through `standalone.exe` or [Chocolatey](https://chocolatey.org/).

* **Standalone**
1. Download the VTEX Setup by copying and paste in your browser the following:

```sh
https://vtex.io/vtexcli/install/win-x64
```

2. Once downloaded, open the VTEX Setup and follow the instructions to complete the installation.

* **Chocolatey**
1. Download and install **Chocolatey** as described on this [link](https://chocolatey.org/install).
2. Once Chocolatey is set up, run the following command from the command line:

```sh
choco install vtex
```


<br>
</details>
 

## Verifying the installation

To confirm that the installation occurred as expected, run the following command to check all default commands available in VTEX IO's CLI.

```sh
vtex
```

### Troubleshooting

After verifying the installation, if you see an error saying that the command or program couldn't be found, take the following steps according to your operating system.

>ℹ️ This error is related to commands that are plugins. Plugins are detached from Tooolbelt base code but still need some functions of it, so that, a require `vtex` is made.
When the `plugin` is installed inside `toolbelt` the required made will search for the `vtex package` inside `/node_modules/vtex`, but this package does not exist, since he will use his own functions. To solve this problem, you will need to create a `symlink` from `VTEX_FOLDER/node_modules/vtex` to `VTEX_FOLDER/`.



<details style="padding-left:30px">
  <summary><span class="fa fa-apple">&nbsp;</span> MacOS</summary>
<br>

In your command line, run the following:

```sh
ln -s /usr/local/Cellar/vtex/2.119.2/libexec /usr/local/Cellar/vtex/2.119.2/libexec/node_modules/vtex
```

<br>
</details>

<details style="padding-left:30px">
<summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

In your command line, run the following:

```sh
ln -s /usr/local/lib/vtex /usr/local/lib/vtex/node_modules/vtex
```

<br>
</details>

<details style="padding-left:30px">
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

* Chocolatey

In your command line, run the following:

```sh
New-Item -ItemType SymbolicLink -Path 'C:\Program Files\vtex\client\node_modules\vtex' -Target 'C:\Program Files\vtex\client'
```
 

<br>
</details>


To confirm that the installation occurred as expected, run the following command :

```sh
vtex
```

If the error persists, don't hesitate to [opean a support ticket.](https://help-tickets.vtex.com/smartlink/sso/login/zendesk)
