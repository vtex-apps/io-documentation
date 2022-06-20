---
title: Managing URL Redirects
description: "Create, delete and verify your store's URL redirects through the VTEX IO CLI."
date: "2020-04-08"
tags: ["adding", "removing", "verifying", "managing", "url", "redirect"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs/docs/en/Recipes/store-management/managing-url-redirects.md"
---

# Managing URL redirects
  
URL redirection is a method of forwarding website visitors and search engines from one URL to another. Redirects might be useful when you need to move content to a new URL, remove an old product page, or forward users from a specific region to a custom page. Implementing the appropriate redirects can improve the user experience by preventing visitors from hitting 404 error pages. 

Check the following sections to learn how to [create](#creating-url-redirects), [remove](#deleting-url-redirects) and [verify](#verifying-url-redirects) your store's URL redirects.

## Before you start

1. [Install the VTEX IO Command-Line Interface (CLI)](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference).
2. [Install the `redirects` plugin for the VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-plugins#installing-a-plugin): 

  ```
  vtex plugins install redirects
  ```

## Creating URL redirects

1. Using the [CSV file template](#csv-file-template) as a reference, create a `.csv` file containing the redirects you wish to create.
2. Save the file under the name of your choice.
3. Open the terminal and log in to your VTEX account.
4. Import redirects to your account by running the following command:
  - _Replace `{CSVpath}` with the path to your `.csv` file._

```
  vtex redirects import {CSVpath}
  ```

Once your file is processed, the redirects will take effect. Please keep in mind that this may take some time.

## Deleting URL redirects

1. Using the [CSV file template](#csv-file-template) as a reference, create a `.csv` file with the redirects you wish to delete.
2. Save the file under the name of your choice.
3. Open the terminal and log in to your VTEX account.
4. Delete redirects from your account by running the following command:
  - _Replace `{CSVpath}` with the path to your `.csv` file._

  ```
  vtex redirects delete {CSVpath}
  ```

## Verifying URL redirects

1. Open the terminal and log in to your VTEX account.
2. Retrieve the full list of your store's redirects into a `.csv` file by running the following command.
  - _Replace `{fileName}` with any name of your choice._

  ```
  vtex redirects export {fileName}.csv
  ```

After running this command, a file named `{fileName}.csv` containing all the redirects of your store will be created in your current directory.

Check the [CSV file template](#csv-file-template) to understand the meaning of each field of the `.csv` file generated.

## CSV file template

To create or delete URL redirects in your store, you must create a `.csv` file as in the following example.

![csv-file-url-redirect](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/managing-URL-redirects-1.png?raw=true)

Notice that the file must contain a row with four columns and the following values:

| Property name | Description | Example |
|--|--|--|
| `from` | Original path. | `/blouse/p` |
| `to` | Relative path or full URL to which you want to redirect your visitors. | `/blouse/p?skuId=2000549` |
| `type` | Redirect type. `TEMPORARY` or `PERMANENT` | `TEMPORARY` |
| `endDate` | (Only for `TEMPORARY` redirects.) Expiration date of the redirect on the format `mm/dd/yyyy`.| `5/20/2020` |

>⚠️ You must not modify this row. Otherwise, you won't be able to create or delete redirects.

Under the first row of your `.csv` file, you must enter the `from`, `to`, `type`, and `endDate` values corresponding to the redirects you want to create or delete, as in the following example:

![urls-redirect-csv-file](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/managing-URL-redirects-2.png?raw=true)

Keep in mind that:

- The `from` column can only receive relative paths.
- The `to` column can receive either relative paths (e.g., `/blouse/p?skuId=200`) or full URLs (e.g., `https://myotherstore.com`).
- `TEMPORARY` redirects receive the `302` status code, while `PERMANENT` redirects receive the `301` status code.
- The `endDate` must be left empty if the redirect is `PERMANENT`.

<div style="text-align: right"><a href="#creating-url-redirects">Creating URL redirects 🔼</a></div>
<div style="text-align: right"><a href="#deleting-url-redirects">Removing URL redirects 🔼</a></div>
<div style="text-align: right"><a href="#verifying-url-redirects">Verifying URL redirects 🔼</a></div>
