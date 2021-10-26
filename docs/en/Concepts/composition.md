# Composition

Composition is one of the main properties for the theme's `interfaces.json` file, being used to **define the expected behavior from a React component in your Store Theme app once it is declared as a block**.

According to the framework logic, a component can be a crossroad for several different blocks: it is possible and desirable to render it using a family tree, leveraging from the parent/child relationship between blocks to achieve the proper results on the UI. 

What defines how a parent block should declare its children in your Store Theme app is the `composition` property: whenever a new block is about to be developed for the framework, it gets a composition definition in the `interfaces.json` file that can either be `blocks`, `children`, or `slots`.

> ℹ️ **We strongly recommend you to use `slots` composition whenever possible due to its greater flexibility!**

## Blocks

The `blocks` composition is the default value for a React component definition in your theme. 

Once you define that a block composition is `blocks`, you are also defining in practice that all of its child blocks must be declared through an `blocks` list, as shown in the example below:

```json
"shelf#home": {
  "blocks": ["product-summary.shelf"]
},
````
*The `product-summary.shelf` has `blocks` composition. Thereby, it is declared in the shelf's `blocks` list.*

In addition to that, the children will have an specific, fixed and preordained (according to the React component nature) position on the UI, regardless of its code positioning in the theme.

>⚠️ Notice that the `composition` property does not define the position on the UI for the block in which it is defined, but rather to its children!

## Children

Blocks whose composition is `children` will declare their child blocks in a `children` list with no preordained position attached, which means that how their children are defined in the code directly impacts their positioning on the store page.

In practice, the block declared first in the `children` list will be at the top of the page, followed by the second block below it on the list and so on.

For example:

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
*The `product-summary-name` has `children` composition, thereby it is declared in the `product-summary.shelf`'s children list.*

Notice that in the example above, `product-summary.shelf` requires other blocks as children, such as `product-summary-name`, to properly render the component. 

In this scenario, keep in mind that the blocks ordering matters. The `product-summary-name` will be rendered first, followed by the `product-summary-description` and so on.

>⚠️ Notice that the `composition` property does not define the position on the UI for the block in which it is defined, but rather to its children.

## Slots

The `slots` composition, in turn, allows you to declare child blocks using regular React props instead of declaring an array for it. 

```json
{
  "hello-world": {
    "props": {
      "Icon": "icon-caret#point-up"
    }
  },
  "icon-caret#point-up": {
    "props": {
      "orientation": "up"
    }
  }
}
```
*The `icon-caret#point-up` has `slots` composition, thereby it is declared as a prop in the `hello-world` block. Notice that the prop name can be any of your choosing and is usually defined by the block in which it is declared.*

Check out the complete documentation for slots [here](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-slots/)!
 
 
 

