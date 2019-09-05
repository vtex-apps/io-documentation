# Customizing styles

The `style.json` file in the `style` folder is the one responsible for defining your theme’s style. This means that you can customize your entire store’s appearance by simply adjusting the default definitions declared in this file, without the need to declare CSS for each page’s components.


Thankfully, this is easy to do thanks to the [VTEX Styleguide](https://styleguide.vtex.com/#/Styles), a highly-configurable CSS framework responsible for defining the component style guideline. There, your can find a proper translation for what your `styles.json` file props and blocks mean in order to help your customization. 


For example: in `style.json`, we can set the default theme background color to blue, by simply changing the `semanticColors` block’s `base` property:

```
"semanticColors": {
        "background": {
          "base": "#00BFFF",
          "base--inverted": "#03044e",
          "action-primary": "#0F3E99",
          "action-secondary": "#eef3f7",
          "emphasis": "#f71963",
          "disabled": "#f2f4f5",
          "success": "#8bc34a",
          "success--faded": "#eafce3",
          "danger": "#ff4c4c",
          "danger--faded": "#ffe6e6",
          "warning": "#ffb100",
          "warning--faded": "#fff6e0",
          "muted-1": "#727273",
          "muted-2": "#979899",
          "muted-3": "#cacbcc",
          "muted-4": "#e3e4e6",
          "muted-5": "#f2f4f5"
        },
        
```

Save the changes made to your code and check out your store’s new appearance:

![STORE-THEME-BLUE-FORREAL](https://user-images.githubusercontent.com/52087100/61972132-31269980-afb7-11e9-863f-0727c363cb8f.png)

## Advanced styles with CSS replacements

The `style.json`. file allows for a more generic customization of your theme. However, you may want to create a more customized store identity, giving its components a more exclusive look.

**CSS replacements customize components so that these take on styles that are different to the default theme**, overwriting what was declared in `styles.json`. You may want your homepage Infocards to have a different style than the rest of your store’s components, for example.

You declare new CSS replacements by creating a file within the `style` folder in `css`. The created file’s name should be the app whose customization will be overwritten, adhering to the `vtex.{app}.css` format.

<div class="alert alert-info">
Find out which app can have their style overwritten by accessing your theme’s <code>manifest.json</code>.
</div>

Classes should be individually customized within the file. You can find a component’s classes by accessing its [documentation](/docs/components/all).

In the `vtex.store-components.css` file, declare the following CSS replacement:

```
.infoCardContainer {
 background-color: #E71111

}

```

Save your changes and access your store once more to check out the Infocards new red style having overwritten your store’s predefined blue:

![banner-1-substituiçãocss-FORREAL](https://user-images.githubusercontent.com/52087100/61972638-7a2b1d80-afb8-11e9-8fd3-65e3852f1022.png)

![banner-2-sobrescrevendo-FORREAL](https://user-images.githubusercontent.com/52087100/61972620-697aa780-afb8-11e9-81a9-729478961e62.png)

### Block Class

Now that you’ve learned to overwrite a component’s appearance, imagine the following situation: instead of giving the same style to all your Infocards, you want each one to have its own style.

This means that you’ll need to not just declare one CSS replacement for the Infocard component, but create a CSS replacement for a specific block pertaining to it.

**Block Class (**`"blockClass"`**) is a property pertaining to some Store Theme components, that, when declared in a block, permits its exclusive customization.**

For example: let’s customize the way in which the `info-card#bestdeals` block is rendered, adding the `blockClass` prop to it inside the `store` > `home` > `home.jsonc` file:

![INFOCARD-BLOCKCLASS-FORREAL-REAL](https://user-images.githubusercontent.com/52087100/61976127-54564680-afc1-11e9-9f62-ab3473639805.png)

```
"info-card#bestdeals": {
    "props": {
      "blockClass": "sales",
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
The <code>blockClass</code> property can have a value of your choosing, as long as it’s correctly referenced in the created CSS file.
</div>

To correctly reference the block, simply add the `blockClass` property value in one of your component’s CSS replacement adhering to the `.{class}--{blockClassvalue}` format.

```
.infoCardContainer--sales {
  background-color: #E6BB12
}

```

After saving the changes, you can see the Infocard with its exclusive customization:

![infocard-yellow-forreal](https://user-images.githubusercontent.com/52087100/61976477-405f1480-afc2-11e9-842d-de5caa3f07d9.png)

<div class="alert alert-warning">
CSS replacements can only be manually changes by code, whereas customization in `json.style` can easily be edited using admin's Storefront. Therefore, when customizing your theme’s style, it’s recommended that you avoid heavy customizations that require CSS replacements.
</div>

Throughout this tutorial, you understood what **Store Framework**, **Toolbelt** and **Store Theme** are, in addition to learning how to structure your store’s pages by configuring **templates** and customizing **styles**. For further study on VTEX IO, don’t forget to access the rest of our [documentation](https://vtex.io/docs/recipes/all).
