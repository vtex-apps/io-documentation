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

For Linux, you will use the standalone install, a tarball with a binary that contains its own node.js binary.

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

For Windows you can install it through `standalone.exe` or [Chocolatey](https://chocolatey.org/).

* **Standalone**
1. Download the VTEX Setup by copying and paste in your browser the following:

```sh
https://vtex.io/vtexcli/install/win-x64
```

2. Once downloaded, got to the folder where the VTEX Setup was downloaded and open it on your machine.
3. To finish the installation process, follow the instructions described on it.

* **Chocolatey**
1. Download and install **Chocolatey** as described on this [link](https://chocolatey.org/install).
2. Once Chocolatey is set up, run the following command from the command line:

```sh
choco install vtex
```


<br>
</details>

## Installing VTEX IO's CLI by NPM

The CLI is built with Node.js and is installable via `npm`. However, according to your operating system, we recommend using the other installation methods from the previous section, [Installing VTEX IO's CLI](#installing-vtex-ios-cli). Since the proper version of Node.js is already included in the other methods, it does not conflict with any other version on your system.

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

After verifying the installation, if you see an error saying that the `vtex` module  could not be found, you will need to create a `symlink` from `VTEX_FOLDER/node_modules/vtex` to `VTEX_FOLDER/`. take the following steps according to your operating system, to solve this problem.

> `symlink`, also known as a symbolic link, is a file that contains a reference to another file or directory.

>ℹ️ This error is related to commands that are [plugins](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-plugins). Plugins are detached from Tooolbelt base code but still need some functions of it, so that, a request VTEX is made.
When the plugin is installed inside the toolbelt the request made searches for the `vtex package` inside `/node_modules/vtex`, but this package does not exist, since it uses his own functions.



<details style="padding-left:30px">
  <summary><span class="fa fa-apple">&nbsp;</span> MacOS</summary>
<br>

1. In your command line, run the following:

```sh
ln -s /usr/local/Cellar/vtex/2.119.2/libexec /usr/local/Cellar/vtex/2.119.2/libexec/node_modules/vtex
```
2. After running the command, a `symlink` should be created to solve the dependencies' issues.
3. To confirm that the installation occurred as expected, run `vtex` to check all default commands available in VTEX IO's CLI.
<br>
</details>

<details style="padding-left:30px">
<summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

1. In your command line, run the following:

```sh
ln -s /usr/local/lib/vtex /usr/local/lib/vtex/node_modules/vtex
```
2. After running the command, a `symlink` should be created to solve the dependencies' issues.
3. To confirm that the installation occurred as expected, run `vtex` to check all default commands available in VTEX IO's CLI.

<br>
</details>

<details style="padding-left:30px">
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

* Chocolatey

1. In your command line, run the following:

```sh
New-Item -ItemType SymbolicLink -Path 'C:\Program Files\vtex\client\node_modules\vtex' -Target 'C:\Program Files\vtex\client'
```
2. After running the command, a `symlink` should be created to solve the dependencies' issues.
3. To confirm that the installation occurred as expected, run `vtex` to check all default commands available in VTEX IO's CLI. 

<br>
</details>

#### NPM

After verifying the installation, if you see an error saying that the command or program could not be found, take the following steps according to your operating system.

>ℹ️ Notice that this error is related to the Yarn installation, meaning that the `yarn global add` command did not add Yarn binaries to a directory known by your terminal as `PATH`. Hence, by not adding the Yarn binaries to terminal `PATH`, Yarn and its programs can't be found, resulting in an error when running VTEX IO's CLI.

<details style="padding-left:30px">
  <summary><span class="fa fa-apple">&nbsp;</span> MacOS</summary>
<br>

1. In your local directories, find the Profile file. It is usually hidden and named after the command line's interpreter. For example: if you're using `bash`, your Profile file will be named `bashrc`. If you use `zsh`, it will be `zshrc`.
2. Once in the Profile file, add the following command: `export PATH=$PATH:$(yarn global bin)`.
3. Log in and log out of the terminal for the changes to take effect.

>ℹ️ If your command line Shell is Fish, you can ignore the step by step above. Run the following command in your terminal: `set -U fish_user_paths (yarn global bin) $fish_user_paths`.

<br>
</details>

<details style="padding-left:30px">
<summary><span class="fa fa-linux">&nbsp;</span>Linux</summary>
<br>

1. In your local directories, find the Profile file. It is usually hidden and named after the command line's interpreter. For example: if you're using `bash`, your Profile file will be named `bashrc`. If you use `zsh`, it will be `zshrc`.
2. Once in the Profile file, add the following command: `export PATH=$PATH:$(yarn global bin)`.
3. Log in and log out of the terminal for the changes to take effect.

>ℹ️ If your command line Shell is Fish, you can ignore the step by step above. Run the following command in your terminal: `set -U fish_user_paths (yarn global bin) $fish_user_paths`.

<br>
</details>

<details style="padding-left:30px">
  <summary><span class="fa fa-windows">&nbsp;</span>Windows</summary>
<br>

1. Run the `yarn global bin` command in your terminal. It will return the path in which the yarn global binaries were saved.
2. Copy it to your clipboard. This path now must be added to the Windows Environment Variable Path;
3. Click on the Windows button and search for environment. Then, click on `Edit the system environment variables`.
4. In the `System Properties` dialog, click on the `Environment Variables...` button.
5. In `User Variables`, select `Path` and then click on the `Edit...` button.
6. Click on the `New` button to add a new path to the search.
7. Paste the yarn global binary path copied in Step 2 and click `OK` when prompted. This will save your changes.
8. Log in and log out of the terminal for the changes to take effect.

<br>
</details>

To confirm that the installation occurred as expected, run the following command :

```sh
vtex
```

If the error persists, don't hesitate to [open a support ticket.](https://help-tickets.vtex.com/smartlink/sso/login/zendesk)
