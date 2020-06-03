---
title: Using the Assets Builder
description: "Use the VTEX Assets Builder and easily handle your store block's asset files."
date: "2020-03-02"
tags: ["assets", "builder", "file-manager", "files"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/using-the-assets-builder.md"
---

# Using the Assets Builder

The VTEX Assets Builder is responsible for  **handling assets**  within store theme  `blocks`  by getting all asset paths used and uploading them in the  **File Manager**  service.

As its name implies, the File Manager manages all of your store files and their respective URLs. It is able to translate the asset paths and then export the asset immutable URLs so that all block assets can be properly rendered.

The Assets Builder has two main advantages:

-   You won't need to declare URLs for assets in each blocks, making your code lighter;
-   You can use it whenever you want, having no prerequisites.

Check out the instructions to use it below:


## Step by step 

1.  Add the  `assets-builder`  to your theme's builder list in the  `manifest.json`  file. For example:

```JSON
"builders": {
  "assets": "0.x"
},
```

2.  In the _root_  directory of your app, create an  `assets`  folder to store and manage your store's assets, such as images:

![assets-folder](https://user-images.githubusercontent.com/60782333/83685560-3e40eb80-a5bf-11ea-9ea1-d443bce21b11.png)

3. Add the desired asset files in the  `assets`  folder as shown above. Your asset files are now saved in the **File Manager**. Notice that you can create subfolders within the  `assets`  folder to better organize the assets used by the theme blocks. 

<div class="alert alert-info">
The storage process takes some of the asset particularities into account, such as the app version in which the code input occurred. It means that you can save several images using the same name, as long as these are spread across different versions of the same app. 
</div>

4. Now you're able to use your assets within store theme blocks that uses media, such as an [Image](https://vtex.io/docs/components/all/vtex.store-components@3.115.3/image/) block, an [Info Card](https://vtex.io/docs/components/all/vtex.store-components@3.116.0/infocard/), etc. To do that, you must use the desired asset path as the value of a given prop of your block. For example, for an Image block, you'll use `assets/{your-image}.{jpg/png/gif}` as the `src` value:

```JSON
"image": {  
    "props": {  
      "src": "assets/myimage.png"  
    }  
}
```
Our builder will automatically look for the path `assets/{your-image}.{jpg/png/gif}` of your asset in the **File Manager** to replace its value with its URL. 
<div class="alert alert-warning">
If you created subfolders inside the `assets` folder, remember to include the folder hierarchy in the asset path, such as:  `assets/events/vtex-day.jpg`.
</div>

Done! The Assets Builder is configured and ready to be used by the Platform. 

A few things to consider: 

- The Assets Builder is not responsible for URL caching, File Manager is; 
- It is not possible to reference assets through React or other apps; 
- Avoid long file names or unnecessarily heavy assets. This will negatively affect the request payload size and Builder optimization;
- Any *image* extension is allowed, such as **JPEG**, **PNG** and **GIF**. Videos are not allowed yet.
