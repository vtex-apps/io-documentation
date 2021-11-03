---
title: Running IO scripts in non-IO VTEX stores
description: "Learn how to develop your own Scripts app to make it possible to run VTEX IO scripts in any VTEX store."
date: "2020-10-26"
tags: ["scripts", "custom"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/running-IO-scripts-in-non-IO-VTEX-stores.md"
---

# Running IO scripts in non-IO VTEX stores

To make it possible to run VTEX IO scripts in non-IO VTEX stores, you must develop and release your own *Scripts app*.

A *Scripts app* is an application that allows the usage of pre-defined VTEX IO scripts in pages external to the VTEX IO. That means that any VTEX store that installs your new *Scripts app*, even the ones that don't use the VTEX IO, can take advantage of running the VTEX IO scripts defined within your application in its website pages.

Notice that nothing keeps an account from having multiple *Scripts apps* installed. Hence, we recommend that, when building a *Scripts app*, you define a clear goal and offer a suite of coherent functionalities.

In the following sections, we'll teach you how to develop and implement your own *Scripts app*.

## Step by Step

## Step 1 - Developing your app

1. Using your terminal, clone the *Scripts app* boilerplate repository to your local files by running:
    
```
git clone https://github.com/vtex-apps/app-scripts-example
```
    
2. Then, using any code editor of your choice, open the boilerplate repository's directory.
3. Open the `manifest.json` file and update its metadata, according to your scenario. It's essential that you update the following fields:

 - `vendor` - The app owner. That is, the VTEX account responsible for the app development, maintenance, and distribution.
 - `name` - The app name. It should concisely express the app's purpose. They must be comprised of lowercase letters separated by hyphens. Special characters, such as `*` and `@`, and numbers at the beginning of the name are not recommended.
- `title` - The app distribution name. This name is the one used in the Apps section from the Administrative Panel and in the VTEX App Store.
- `description` - A brief description explaining the app's purpose. This description will be publicly available in the App Store, providing context for whoever wants to install your app.

4. In the `/scripts` folder, delete the example files and save your own `.ts` scripts.
5. In the `/scripts` folder, open the `loader.json` file, and edit it by declaring in which page each script must be executed following the instructions provided in the [Configuring the `loader.json` file](#configuring-the-loaderjson-file) section.
6. Open the admin of the account you're using to develop your app, and follow the instructions provided in the [Importing scripts](#importing-scripts) section, considering a development workspace.
7. Once everything is set up, use the terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/) to log in to the VTEX Account that you are using to develop your VTEX IO *Scripts App*.
8. Run `vtex use {workspace}` to use a developer environment.
    
>⚠️ Remember to replace the values between the curly brackets according to your scenario.
    
9. Run `cd app-scripts-example` to go to the local app directory.
10. Run `vtex link` to [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) your new app to your development workspace.
11. Check the pages for which you implemented your scripts. 
12. Once you're happy with the changes, update your *Scripts app* `docs/README.md` file as instructed in [Documenting your app](#documenting-your-app). Therefore, follow our documentation on [making your new app version publicly available](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available/) to run your app on master. 

## Step 2 - Implementing your scripts in the desired account

Now that you finished developing your *Scripts* app, you must implement it in the desired VTEX account.

1. Using the VTEX IO CLI or the App Store, install the app you just developed in the desired account.
2. Follow the instructions provided in the [Importing scripts](#importing-scripts) section, considering a production workspace.

## Configuring the `loader.json` file

The `loader.json` file acts as a declarer of which scripts should be executed on which page. 

Each entry in the `loader` `JSON` object must have a `RegExp` key, indicating the page path, and a corresponding array of strings, where each string points to the script files that must be loaded to a page if the `RegExp` key matches the path of that page URL.

Take the following example:

```json
{
  ".*": ["script1"],
  ".*\/b$": ["script2"],
  ".*\/p$": ["script2", "script3"]
}
```

In this example, the `script1` will be loaded and executed in all pages (`.*`) of the application. 

For brand pages, expressed by URLs ending in `/b`, besides the `script1`, the `script2` will also be loaded. 

Finally, for product pages, expressed by URLs ending in `/p`, besides the `script1`, the `script2` and the `script3` will also be loaded.

>⚠️ Note that, by default, the scripts are located in the `scripts` folder. Hence, the complete path can be omitted. Also, as the scripts builder only looks for `.ts` files, it's not necessary to indicate file extensions.

Although a single `RegExp` can have multiple corresponding scripts and multiple `RegExp` can match a single URL path, each script is loaded and executed only one time per page, independently of how many occurrences it has in matched `RegExps`.

## Importing scripts

1. Considering the workspace in which you're currently working, open the VTEX admin of the desired account and workspace.
2. Go to **CMS > Layout**.
3. Open the desired page template.
4. Before the `body` closure, place a single HTML `script` tag to import the `load.js` file, as in the following examples:

**Development**

```html
<script src="https://{devWorkspace}--{account}.myvtex.com/_v/public/vtex.scripts-server/v1/load.js" type="text/javascript"></script>
```

where:

- `devWorkspace`- the development workspace of the account used to develop your *Scripts app.*
- `account`- the name of the account used to develop your *Scripts app.*

**Production**

```html
<script src="/api/io/_v/public/vtex.scripts-server/v1/load.js?workspace={productionWorkspace}" type="text/javascript"></script>
```

where:

- `productionWorkspace` - the production workspace of the account you are implementing the *Scripts app.*

The `src` value from the `script` tag is the same for all pages in which you want to load your app's scripts.

According to the definitions from the `loader.json` file, the script server will load and execute only the appropriate scripts for that page: the ones whose the URL matches the `RegExps` from the `loader.json` file against the page path.

## Modus Operandi

All scripts available in a *Scripts app* are saved in its `/scripts` folder along with a `loader.json` file, which indicates in which page each script must be executed. 

The scrips builder, set in the `manifest.json` file, is responsible for parsing each script declared in the `loader.json` file and for making them available to the `/load.js` route of the VTEX IO script server.

Hence, once you install a *Scripts app* in a VTEX account, you can import the script server's route (`/load.js`) to your pages by using the `script` HTML tag.

Finally, according to the definitions from the `loader.json` file, the appropriate scripts for each page will be loaded and executed instantly.
