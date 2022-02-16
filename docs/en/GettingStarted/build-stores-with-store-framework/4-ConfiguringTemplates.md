# 4. Configuring templates

**We call a template your website's page structure.** 

Templates are responsible for declaring `JSON` blocks that, once rendered, will define the set of components for your website's pages, such as the home page, product page, search results page, etc. 

As you could see in the previous step, the Store Theme app already implements basic templates for each and every of your store’s pages in its `blocks.json` and `blocks.jsonc` files. This is what allowed your store to display VTEX Store Framework default components even when no configurations were performed by you in the code.  

In practice, managing templates is what allows you to build the desired theme for your website by adding or removing blocks according to your store's needs. 

## Step 1 - Understanding what is a JSON block

In order to edit templates and consequently your store's components, we need to take a closer look at what blocks are and how they are applied to the store theme. 

**Blocks are the minimal Store Framework abstraction of React components that we want to see on the UI**. Blocks are small pieces of code, exported to the platform by independent apps that configure how they will be rendered on your website.

Although they may look simple at first, blocks are imbued with higher flexibility, allowing you to achieve complex scenarios and specific component behaviors by configuring their properties (*props*) or even declaring them in other blocks. 

This means that whenever you edit your theme's code using the Store Theme app, you're also editing blocks that will end up being your store's page components when rendered.

>ℹ️ We declare a new block in a template in order to add a new component to a page, in the same way that a component can be excluded from a page simply by removing a block from a template.

## Step 2 - Managing blocks in your theme

As we have previously seen, the folder responsible for organizing your store’s blocks and templates is called `store`. 

In it, you can declare all your blocks in the `blocks.jsonc` file or create as many `blocks.jsonc` files and folders as you want. You can also declare blocks using the `blocks` subfolder. The only difference between the two folders is that `jsonc` files allow you to comment in the code.

As previously mentioned, blocks are pieces of code exported by VTEX Store Framework apps. This means that whenever a block is used in your theme, the app behind it must be declared in your Store Theme [dependencies](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-dependencies/) list.
 
Have a look at the `manifest.json` file from the Store Theme app. You'll come across an object called `dependencies` which contains the names of several apps and their respective versions. These apps are already listed, since the default Store Theme code already declared templates which in turn use blocks that these apps export.

When declaring a new block in your Store Theme app, make sure to check that the app responsible for that block is listed as a dependency. If it's not, open the `manifest.json` file and add the app's name and desired version in the `dependencies` list, following this format: `"vtex.{appName}": "{majorVersion}.x"`.

## Step 3 - Understanding a block's structure

Let’s now have a look at your store’s predefined homepage template: 

1. Open the Store Theme app using any code editor, such as Visual Studio Code.
2. Access `store` and then `blocks`. 
3. Acess `home` and then `home.jsonc`. You will be able to see a result similar to the one below:

```jsonc
{
  "store.home": {
    "blocks": [
      "list-context.image-list#demo",
      /* You can make references to blocks defined in other files.
       * For example, `flex-layout.row#deals` is defined in the `deals.json` file. */
      "flex-layout.row#deals",
      "rich-text#shelf-title",
      "flex-layout.row#shelf",
      "info-card#home",
      "rich-text#question",
      "rich-text#link",
      "newsletter"
    ]
  },

  "shelf#home": {
    "blocks": ["product-summary.shelf"]
  },

  "product-summary.shelf": {
    "children": [
      "product-summary-name",
      "product-summary-description",
      "product-summary-image",
      "product-summary-price",
      "product-summary-sku-selector",
      "product-summary-buy-button"
    ]
  },

  "list-context.image-list#demo": {
    "children": ["slider-layout#demo-images"],
    "props": {
      "height": 720,
      "images": [
        {
          "image": "https://storecomponents.vteximg.com.br/arquivos/banner-principal.png",
          "mobileImage": "https://storecomponents.vteximg.com.br/arquivos/banner-principal-mobile.jpg"
        },
        {
          "image": "https://storecomponents.vteximg.com.br/arquivos/banner.jpg",
          "mobileImage": "https://storecomponents.vteximg.com.br/arquivos/banner-principal-mobile.jpg"
        }
      ]
    }
  },
  "slider-layout#demo-images": {
    "props": {
      "itemsPerPage": {
        "desktop": 1,
        "tablet": 1,
        "phone": 1
      },
      "infinite": true,
      "showNavigationArrows": "desktopOnly",
      "blockClass": "carousel"
    }
  },

  "rich-text#shelf-title": {
    "props": {
      "text": "## Summer",
      "blockClass": "shelfTitle"
    }
  },
  "flex-layout.row#shelf": {
    "children": ["list-context.product-list#demo1"]
  },
  "list-context.product-list#demo1": {
    "blocks": ["product-summary.shelf"],
    "children": ["slider-layout#demo-products"],
    "props": {
      "orderBy": "OrderByTopSaleDESC"
    }
  },
  "slider-layout#demo-products": {
    "props": {
      "itemsPerPage": {
        "desktop": 5,
        "tablet": 3,
        "phone": 1
      },
      "infinite": true,
      "fullWidth": true,
      "blockClass": "shelf"
    }
  },

  "info-card#home": {
    "props": {
      "id": "info-card-home",
      "isFullModeStyle": false,
      "textPosition": "left",
      "imageUrl": "https://storecomponents.vteximg.com.br/arquivos/banner-infocard2.png",
      "headline": "Clearance Sale",
      "callToActionText": "DISCOVER",
      "callToActionUrl": "/sale/d",
      "blockClass": "info-card-home",
      "textAlignment": "center"
    }
  },

  "rich-text#question": {
    "props": {
      "text": "**This is an example store built using the VTEX platform.\nWant to know more?**",
      "blockClass": "question"
    }
  },

  "rich-text#link": {
    "props": {
      "text": "\n**Reach us at**\nwww.vtex.com.br",
      "blockClass": "link"
    }
  },

  "product-summary-buy-button": {
    "props": { 
      "displayBuyButton": "displayButtonAlways"
    }
  }
}
```

As we can see, the default `store.home` homepage template declares the following blocks: 

- `list-context.image-list#demo`
- `flex-layout.row#deals`
- `rich-text#shelf-title`
- `flex-layout.row#shelf`
- `info-card#home`
- `rich-text#question`
- `rich-text#link`
- `newsletter`

This means that your default store homepage will comprise the components defined by these blocks. 

The same file (`home.jsonc`) also has each block’s declaration as well as their configuration, using the block's props and even other blocks in order to build more complex components. 

>⚠️ More than simply declare a block in the block list template, notice that you will also need to declare the block in order to set its behavior when rendered as a component. For this purpose, you will need to use the block's props (as shown in the next section) and other child blocks as well to define its configuration (as shown in the Block composition section).

## Step 4 - Clarifying block naming and properties

Still in the `home.jsonc` file, use `ctrl+f` and look up for the `rich-text#question` block:

```json
"rich-text#question": {
  "props": {
    "text": "**This is an example store built using the VTEX platform. Want to know more?**",
    "blockClass": "question"
  }
},
```

This block is responsible for rendering a component that displays markdown texts to users. 

As we can see, the `rich-text#question` block is using two props: `text` and `blockClass`. These are responsible for defining which text the component will display and for defining an ID that will be used for its customization - as we will see in the next step of this track.

You can now take a look at the [documentation](https://developers.vtex.com/vtex-developer-docs/docs/vtex-rich-text) of the app behind the block (also called Rich Text) and check the available props table in the Configuration section. 

When looking at the documentation, you'll notice that the exported block's name is merely `rich-text`, however Store Theme uses `rich-text#block`. This is due to the fact that we can use a `#` after the block's official name to easily identify when inserting it in our theme's code, thereby better organizing the theme itself.

>ℹ️ All the props available to configure a block can be found in the documentation of its exporting app or in the block's own documentation (if it exists).

## Step 5 - Understanding blocks composition

Now, let's take a look at the `shelf#home` block in the same file (`home.jsonc`): 

```json
"shelf#home": {
  "blocks": ["product-summary.shelf"]
},
````

Note that it declares another block to your `blocks` list, that in turn declares other blocks below in a list called `children`:

```json
"product-summary.shelf": {
  "children": [
    "product-summary-name",
    "product-summary-description",
    "product-summary-image",
    "product-summary-price",
    "product-summary-sku-selector",
    "product-summary-buy-button"
  ]
},
```

You'll notice that in the example above, `product-summary.shelf` requires other blocks as children, such as `product-summary-name`, to properly render the component.

>ℹ️ As previously mentioned, a component can be a crossroad for several different blocks, and therefore one of your theme's blocks may need to list other blocks to achieve the proper rendering results on the UI.

To build a component using several blocks, the main block can declare a `blocks` list onto itself, such as `shelf#home`, or it can declare a list of `children` blocks, as the `product-summary.shelf` block does. 

What defines whether a block declares other blocks using a `blocks` or a `children` list is the *composition* of the blocks about to be declared in the list. 

When a block is about to be developed for the framework, it gets a composition definition that can either be `blocks` or `children`:

- `blocks` composition blocks have a fixed position on the store's page irrespective of where they were declared in the code, leading to a preordained position on the UI.
- `children` composition blocks on the other hand do not have a fixed position on the store's page, which means that how they're declared in the code directly impacts the page position. The `children` block declared first will be at the top of the page, followed by the second block below it and so on.  

The conclusion is that, according to their composition, the listed blocks themselves will define if they should be declared in the parent block's `blocks` list or in its `children` list when building a single component on the UI. 

In our example, the `product-summary.shelf` block has a `blocks` composition, while `product-summary-name` has a `children` composition. This explains why they are declared, respectively, in a `blocks` and `children` lists.

>ℹ️ You can find out which composition a block has by looking at its code in the exporting app's `interfaces.json` file. 

