# Configuring templates

When a store is created, a **template** must be configured for each page the user will visit, such as homepage, product page, etc.

The default Store Theme model already implements basic templates for your store’s pages. It is however possible to configure these either by adding or removing components, using [**blocks**](*link*).

## Blocks structure 

We declare a new block in a template in order to add a new component to a page, in the same way that a component can be excluded from a page by removing a block.

As we have previously seen, the folder responsible for organizing your store’s blocks and templates is called `store`. In it, you can declare all your blocks in the `blocks.jsonc` file or create as many files and folders as you want, to then declare these in an organized manner in the `blocks` subfolder. 

For a better understanding of this structure, let’s have a look at your store’s predefined homepage Store Theme template using the code editor of your choice. Access `store` > `blocks`> `home`> `home.jsonc` and you will be able to check out the following example:


```
{
 "store.home": {
   "blocks": [
     "carousel#home",
     "flex-layout.row#deals",
     "shelf#home",
     "info-card#home",
     "rich-text#question",
     "rich-test#link"
     "newsletter"
   ]
 }, 
    (...)
}
```
As we can see, the default `store.home` homepage template declares the following blocks: 

- `carousel#home`
- `flex-layout.row#deals`
- `shelf#home`
- `info-card#home`
- `rich-text#question`
- `rich-text#link`
- `newsletter`

This means that your default store homepage components will be comprised of these declared blocks, in the order in which they are organized.

You’ll be able to find each block’s declaration in this same file, as in the following example:

```
"rich-text#question": {
  "props": {
    "text": "**This is an example store built using the VTEX platform.\nWant to know more?**",
    "blockClass": "question"
  }
},
```

You may customize already declared Store Theme blocks as well as new ones freely, according to your business needs.

## Declaring a new block

Let’s now add a new [__infocard__](*link*) component to your store’s homepage, before the shelf. To do this, we’ll need to add `info-cardf#bestdeals` to the `store.home` template in `home.jsonc`. Then, we will declare the block below in the same file.

<img width="645" alt="newblock-step4" src="https://user-images.githubusercontent.com/52087100/61960418-ca47b700-af9b-11e9-8787-b68cafae1225.png">

```
"info-card#bestdeals": {
   "props": {
     "isFullModeStyle": false,
     "textPosition": "center",
     "imageUrl": "http://cybercitycomix.com/wp-content/uploads/2015/08/Sale-sign.jpg",
     "headline": "BEST DEALS",
     "callToActionText": "DISCOVER",
     "callToActionUrl": "/sale/d",
     "textAlignment": "center"
   }
 },


```

<div class="alert alert-info">
Your store’s component behavior varies according to each block’s defined properties. Check out the block configuration examples for each component in our [related documentation](*link*)
</div>

When saving your changes in code and running `vtex.link` in your terminal, you should see the rendered new Infocard in your store’s homepage:  

<img width="1422" alt="BANNER-INFOCARD-STEP4-FORREAL" src="https://user-images.githubusercontent.com/52087100/61972032-e73db380-afb6-11e9-833e-977964fe5105.png">

<div class="alert alert-warning">
Changes will be reflected in the workspace in which they are made. Therefore, when checking your store’s new Infocard rendering, don’t forget to check which account workspace you’re accessing.
</div>
