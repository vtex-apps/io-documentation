---
title: Installing VTEX IO's CLI
description: "Any development in VTEX IO begins and ends with the Toolbelt, our CLI (Command Line Interface). Learn now how to install it in your terminal."
date: "2021-04-04"
tags: ["toolbelt", "cli", "command-line-interface", "install", "installation"]
version: "0.x"
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
2. Open your command line and run the following command.

```sh
$ yarn global add vtex
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

>ℹ️ Notice that, to install VTEX IO's CLI, you need to ensure that [Node.js](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) are installed on your machine.

## Verifying the installation

To confirm that the installation occurred as expected, run the following command to check all default commands available in VTEX IO's CLI.

```sh
vtex
```

### Troubleshooting

After verifying the installation, if you see an error saying that the command or program couldn't be found, take the following steps according to your operating system.

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
5. In `System Variables`, select `Path` and then click on the `Edit...` button.
6. Click on the `New` button to add a new path to the search.
7. Paste the yarn global binary path copied in Step 2 and click `OK` when prompted. This will save your changes.
8. Log in and log out of the terminal for the changes to take effect.

<br>
</details>

If the error persists, don't hesitate to [opean a support ticket.](https://help-tickets.vtex.com/smartlink/sso/login/zendesk)
