---
title: Using the Assets Builder
description: "Use the VTEX Assets Builder and easily handle your store block's asset files."
date: "2020-03-02"
tags: ["assets", "builder", "file-manager", "files"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/using-the-assets-builder.md"
---

# Using the Assets Builder

The VTEX Assets Builder is responsible for  **handling assets**  within store theme  `blocks` and CSS classes by getting all asset paths used and uploading them in the  **File Manager**  service.

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

2.  In the `store`  root directory of your app, create an  `assets` folder to manage your store's assets, such as images.
3. Then, add the desired asset files in the  `assets` folder. Notice that you can create subfolders within the  `assets`  folder to better organize the assets used by the theme blocks, as shown below:

![assets-folder](https://user-images.githubusercontent.com/60782333/83685560-3e40eb80-a5bf-11ea-9ea1-d443bce21b11.png)

>⚠️ If you created subfolders inside the Assets folder, remember to include the folder hierarchy in the asset path, such as:  `assets/events/vtex-day.jpg`.

4. Use the asset path (`assets/{imageFileName}.{jpg/png/gif}`) as the value of a given block's prop, such as `src`, or CSS class for media rendering:

```JSON
"image": {  
    "props": {  
      "src": "assets/myimage.png"  
    }  
}
```

Once the asset path was added and you save the changes performed, Assets Builder will automatically work to save it in the VTEX IO File Manager and then generate a URL for it, which will be considered by the platform during the theme rendering.

A few things to consider: 

- The Assets Builder is not responsible for URL caching, File Manager is; 
- It is not possible to reference assets through React or other apps; 
- Avoid long file names or unnecessarily heavy assets. This will negatively affect the request payload size and Builder optimization;
- Any *image* extension is allowed, such as **JPEG**, **PNG** and **GIF**. Videos are not allowed yet.
