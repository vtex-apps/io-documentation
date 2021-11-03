---
title: Using several service workers in your store
description: "Learn how to work with several service workers at once without needing to stick to a single one and deactivate others as essential to the operation."
date: "2020-06-17"
tags: ["several", "service-worker", "service", "worker", "builder"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/using-several-service-workers-in-your-store.md"
---

# Using several service workers in your store

The Service Worker builder is responsible for fetching service workers exported by the account's installed apps and bundling them in a single file.

<div class="alert alert-info">
Working as JavaScript files, Service Workers sit between web apps, the browser, and the network to enable effective offline experiences. They can intercept, cache, and modify navigation, providing you control over your web app behavior once the network is not available. 
</div>

Thanks to the builder's bundling feature, stores can leverage from the generated file and simultaneously work with several service workers at once without needing to stick to a single one and deactivate others as essential to the operation. 

![service-worker-diagram](https://user-images.githubusercontent.com/52087100/122475832-9ca6f500-cf9b-11eb-89d7-7b980d5508c0.png)

Find below the instructions on how to generate an app using the Service Worker builder.

## Step by step 

<div class="alert alert-info">
VTEX IO CLI offers the <code>vtex init</code> command which can quickly copy the Service Worker Example app's repository to your computer, where it may be configured and fine-tuned according to your scenario needs. If an app that exports a service worker was already deployed by you and no boilerplate is needed, start with step 5. 
</div>

1. Using your terminal, navigate to an already existing local file directory where you want the Service Worker Example app to be copied to. Note that `{exampleFolder}` example below should be replaced with the folder name where the Service Worker Example is going to be copied to: 

```
$ cd {exampleFolder}
```

2. Run the `vtex init` command in your terminal:

```
$ vtex init
```

3. Select the `service-worker-example` option and confirm that you want to download the app to the destination you just chose:

![service-worker-VTEX IO CLI](https://user-images.githubusercontent.com/52087100/122475839-a03a7c00-cf9b-11eb-8619-53db3503f2cb.png)

<div class="alert alert-info">
Once you select the <code>service-worker-example</code> option, the CLI will ask you for important information about the app, such as a value for the vendor, name, title, and description. With the exception of vendor, press enter to keep each field's predefined values.
</div>

4. Open the Service Worker Example app in your local files using the code editor of your preference.
5. In the `manifest.json` file, update the app's metadata, such as name, title, and decription according to your own scenario needs. 

<div class="alert alert-info">
If you are editing an already-existing app, make sure that the Service Worker builder is declared in the <code>manifest.json</code>'s <code>builders</code> list, as shown below. 
</div>

```diff
 "builders": {
    "docs": "0.x",
+   "service-worker": "0.x"
```

6. In the `service-workers` folder, declare your app's desired event handlers in the suitable files —  in case the folder does not exist, create it. You can find more information regarding which event handler each file expects to receive in the [Service Worker Example app's documentation](https://github.com/vtex-apps/service-worker-example/blob/main/docs/README.md) (README file). For example:

```
function exampleSWInstall() {
  // eslint-disable-next-line no-console
  console.log('[example-sw] Install of service worker')
}

export default 
```

7. [Link your app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app).
8. Open the store website on your browser and inspect it.
9. In the `Console` tab, check if a message similar to `[service-worker-example] Install of service worker` is displayed. If positive, the app's service worker development was successful. 

<div class="alert alert-info">
The message's <code>[service-worker-example]</code> text string should be replaced by your app's own name. 
</div>

10. [Deploy your app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-10-making-your-app-publicly-available#validating-the-deploy) when satisfied with the changes performed. 

The app's service worker will then be automatically fetched and bundled with others exported by your VTEX account's installed apps as well, provided they are also using the Service Worker builder. 

From step 7 on, no further actions are needed from you: your store is ready to work with several service workers at the same time. 





