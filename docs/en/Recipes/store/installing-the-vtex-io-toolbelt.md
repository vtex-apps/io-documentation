---
title: Installing the VTEX IO Toolbelt 
description: "Any development in VTEX IO begins with Toolbelt, VTEX IO’s command line interface for app development and management. Learn how to install it now!"
date: "11/21/2019"
tags: ["toolbelt", "cli", "install"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/master/docs/en/Recipes/layout/building-a-carousel-through-lists-and-slider-layout.md"
---

# Installing the VTEX IO Toolbelt 

## Introduction

Any development in VTEX IO begins with the **Toolbelt**, our CLI (Command Line Interface) that allows you to login to the desired VTEX account, develop new apps and manage the already installed ones.

## Step by step

To install the VTEX IO’s CLI, you need to ensure that [Node.js](https://nodejs.org/) and [Yarn](https://yarnpkg.com/) are installed on your machine. 

Thereafter, type `yarn global add vtex` in your computer’s terminal.

```sh
$ yarn global add vtex
```

<div class="alert alert-info">
To confirm that the installation occurred as expected, you can execute the <code>vtex</code> command. This should display all available commands in a help text. 
</div>

## Troubleshooting

- After installing and running `vtex` in the terminal an error saying that the command or program wasn't found is shown

This may be because the path for the yarn binaries isn't in your `PATH` system environment variable. If you're on **Windows** follow the instructions on this [link](https://sung.codes/blog/2017/12/30/yarn-global-add-command-not-work-windows/). Otherwise, if you're on **MacOS** or **Linux**, you'll have to add to the end of your profile file the line:

`` export PATH="$PATH:`yarn global bin ``

If you're using `bash`, your profile file will be on `~/.bashrc`, if you use `zsh`, it will be on `~/.zshrc`.

In case you use the Fish shell, simply run the command:
`set -U fish_user_paths (yarn global bin) $fish_user_paths`

(src: https://yarnpkg.com/lang/en/docs/install/)

