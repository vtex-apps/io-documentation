---
title: Using the Assets Builder
description: "Use the VTEX Assets Builder and easily handle your store block's asset files."
date: "2020-03-02"
tags: ["assets", "builder", "file-manager", "files"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/using-the-assets-builder.md"
---

# Using the Assets Builder

The VTEX Assets Builder is responsible for **handling assets** within store theme `blocks` by getting all asset paths used and uploading them in the **File Manager** service. 

As its name implies, the File Manager manages all of your store files and their respective URLs. It is able to translate the asset paths and then export the asset immutable URLs so that all block assets can be properly rendered. 

The Assets Builder has two main advantages: 

- You won't need to declare URLs for assets in each blocks, making your code lighter;
- You can use it whenever you want, having no prerequisites. 

Check out the instructions to use it below:

## Step by step 

1. Add the `assets-builder` to your theme's builder list in the `manifest.json` file. For example:

```JSON
"builders": {
  "assets": "0.x"
},
```

2. Create an `assets` folder in your app *root* directory, to insert and manage the desired assets:

![assets-folder](https://user-images.githubusercontent.com/52087100/75712413-a6252480-5ca6-11ea-8ef6-7c54752d451f.png)

3. In the `assets` folder, add the desired asset files as you want as showed above. You can create subfolders within the `assets` folder and better organize the assets used by the theme blocks. 

<div class="alert alert-info">
The storage process takes some of the asset particularities into account, such as the app version in which the code input occurred. It means that you can save several images using the same name, as long as these are spread across different versions of the same app. 
</div>

4. Then, in a given block which uses media, use the desired asset path (directing to the `assets` folder):

![assets-path-blocks](https://user-images.githubusercontent.com/52087100/75712419-a7565180-5ca6-11ea-9afe-5ce398f7e0f4.png)

<div class="alert alert-warning">
Remember to include the folder hierarchy in the asset path, such as: <code>assets/events/vtex-day.png</code>.
</div>

Done! The Assets Builder is configured and ready to be used by the Platform. 

A few things to consider: 

- The Assets Builder is not responsible for URL caching, File Manager is; 
- It is not possible to reference assets through React or other apps; 
- Avoid long file names or unnecessarily heavy assets. This will negatively affect the request payload size and Builder optimization;
- Any *image* extension is allowed, such as **JPEG**, **PNG** and **GIF**. Videos are not allowed yet.
