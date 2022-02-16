# Creating robots files for cross-border stores

A `robots.txt` file defines which folders or files a search engine may or may not ignore when crawling a website. Considering the effects of this file for a store's SEO, the following step by step explains how to create `robots` files for cross-border stores.

>⚠️ If your store is **not** a cross-border one, check this [link](https://help.vtex.com/tutorial/google-search-console-tracking-robots-txt--tutorials_574?locale=en) for a step by step on how to create a `robots` file through your store's admin.

The basic structure of a `robots.txt` file contains the following directives:

- `User-agent`: The search engine robot for which the rules specified in the following are suitable. If the rules are the same for all robots, you can specify the `User-agent` as `*`.
- `Disallow`:  The paths, relative to the root directory, of the *files* or *folders* that the search engine, specified in the `User-agent` field, must not index to the search results.
- `Allow`: The paths, relative to the root directory, of the *files* placed in a folder that has been `Disallowed`, but which are allowed to be crawled and indexed by the search engine.

You must adjust these directives according to your scenario.

>⚠️ This feature is available for stores using `vtex.edition-store@3.x` [Edition App](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app/). To check which Edition App is installed on your account, run `vtex edition get`. If it's a different Edition, please [open a ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to the VTEX Support team asking for the installation of the `vtex.edition-store@3.x` Edition App.

## Step by Step

In this step by step, you'll learn how to develop and release your own *Robots app*, an app responsible for managing your cross-border store's `robots.txt` files.

1. Using the command below, clone the `store-theme-robots` app boilerplate repository.

```
git clone https://github.com/vtex-apps/store-theme-robots
```

2. Once successfully cloned, open the local app directory in your code editor.

3. Open the `manifest.json` file and edit the `vendor` field with the name of the developing account.

```
{ 
  "vendor": "myaccount",
  "name": "robots",
  "version": "0.0.1",
  "builders": {
    "sitemap": "0.x"
  },
  ...
}
```

4. Inside the `sitemap/robots` folder, create a `.txt` robots file for each supported locale binding. The name of each file must be the `id` value of its respective `binding`.

>⚠️ Follow [this tutorial](https://developers.vtex.com/docs/checking-your-stores-binding-id) to check your stores' `binding` `id`s.

Your app's folder may end up with a structure similar to the following:

```
store-theme-robots
├── manifest.json
├── README.md
└─┬ sitemap
  └─┬ robots
    ├── 706e9126-d0fc-47de-9o2d-5f9649e61877.txt
    └── 748aafcf-1674-456d-9ffc-7ddb3f26e43f.txt
```

5. Edit each file from the `sitemap/robots` folder with the desired content for each one of your `robots` files.

6. Once everything is set up, use the terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference/) to log in to the VTEX Account in which you are currently working in.

7. Run `vtex use {workspace}` to use a developer environment.

>⚠️ Remember to replace the values between the curly brackets according to your scenario.

8. Run `cd store-theme-robots` to go to the local app directory.

9. Run `vtex link` to [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) your new app to your development workspace.

10. Check the `robots` file generated for each store by accessing `https://{workspace}--{account}.myvtex.com/{locale}/robots.txt` on your browser.

11. Once you're happy with the changes, follow our documentation on [making your new app version publicly available](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available/) to run your app on master.

Now, you are ready to check out your store's `robots` files by accessing `https://{account}.myvtex.com/{locale}/robots.txt` on your browser.

Once you finish the configuration process, your store will benefit from having a `robots` file, which can improve your store's SEO and help to avoid overloading your site with undesired requests.
