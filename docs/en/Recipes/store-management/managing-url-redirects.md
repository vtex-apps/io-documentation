---
title: Managing URL Redirects
description: "Create, delete and verify your store's URL redirects through the VTEX IO CLI."
date: "2020-04-08"
tags: ["adding", "removing", "verifying", "managing", "url", "redirect"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs/docs/en/Recipes/store-management/managing-url-redirects.md"
---

# Managing URL redirects
  
URL redirect is a technique to forward website visitors and search engines from one URL to another. Redirects might be useful when you need to move content to a new URL, remove an old product page, or forward users from a specific region to a custom page. 

Implementing the appropriate redirects can improve user experience by preventing visitors from hitting a 404 error page. 

Check the following section to learn how to [create](#creating-url-redirects), [remove](#deleting-url-redirects) and [verify](#verifying-url-redirects) your store's URL redirects.
  
## Step by step

### Creating URL redirects

1. Follow our [CSV file template](#csv-file-template) and create a new `.csv` file with the redirects you want to create. You can use Excel or Google sheets, for example.
2. Save the file under a name of your choice.
4. Using the terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference), log in to your VTEX account.
5. Import redirects to your account by running the following command:

```
vtex redirects import {CSVpath}
```

>⚠️ Replace `{CSVpath}` with the path to your `.csv` file.

Once your file is processed, the redirects will take effect. Notice that this might take a while.

### Deleting URL redirects

1. Follow our [CSV file template](#csv-file-template) and create a new `.csv` file with the redirects you want to delete. You can use Excel or Google sheets, for example.
2. Save the file under a name of your choice.
3. Using the terminal and the [VTEX IO CLI](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), log in to your VTEX account.
4. Delete redirects from your account by running the following command:

```
vtex redirects delete {CSVpath}
```

>⚠️ Replace `{CSVpath}` with the path to your `.csv` file.

### Verifying URL redirects

1. Using the terminal and the [VTEX IO CLI](https://vtex.io/docs/recipes/development/vtex-io-cli-installment-and-command-reference), log in to your VTEX account.
2. Retrieve the full list of your store's redirects into a `.csv` file by running the following command.

```
vtex redirects export {fileName}.csv
```

>⚠️ Replace `{fileName}` with any name of your choice.

Once you run this command, a file named `{fileName}.csv` containing all the redirects of your store will be created in your current directory.

Check the [CSV file template](#csv-file-template) to understand the meaning of each field of the `.csv` file generated.

## CSV file template

To create or delete URL redirects in your store, you must create a `.csv` file as in the following example.

![csv-file-url-redirect](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/managing-URL-redirects-1.png?raw=true)

Notice that the file must contain a row with four columns, and the following values: `from`, `to`, `type` and `endDate`.

>⚠️ You must not modify this row. Otherwise, you won't be able to create or delete redirects.

Under the first row of your `.csv` file, you must enter the `from`, `to`, `type`, and `endDate` values corresponding to the redirects you want to create or delete, as in the following example:

![urls-redirect-csv-file](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/managing-URL-redirects-2.png?raw=true)

Check in the following the meaning of each one of these fields:

| Property name | Description | Example |
|--|--|--|
| `from` | Original path. | `/blouse/p` |
| `to` | Relative path or full URL to which you want to redirect your visitors. | `/blouse/p?skuId=2000549` |
| `type` | Redirect type. `TEMPORARY` or `PERMANENT` | `TEMPORARY` |
| `endDate` | (Only for `TEMPORARY` redirects.) Expiration date of the redirect on the format `mm/dd/yyyy`.| `5/20/2020` |

Keep in mind that:

- The `from` column can only receive relative paths.
- The `to` column can receive either relative paths (e.g., `/blouse/p?skuId=200`) or a full URL (e.g., `https://myotherstore.com`).
- `TEMPORARY` redirects receive the `302` status code, while `PERMANENT` redirects receive the `301` status code.
- The `endDate` must be left empty if the redirect is `PERMANENT`.

<div style="text-align: right"><a href="#creating-url-redirects">Creating URL redirects 🔼</a></div>
<div style="text-align: right"><a href="#deleting-url-redirects">Removing URL redirects 🔼</a></div>
<div style="text-align: right"><a href="#verifying-url-redirects">Verifying URL redirects 🔼</a></div>
