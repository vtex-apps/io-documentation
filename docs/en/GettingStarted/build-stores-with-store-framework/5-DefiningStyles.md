# 5. Defining styles

Your website’s **visual style** is a fundamental resource to building your **store’s identity**. 

Once you understand what blocks and templates are and how they render interface components, it's time to learn how to customize them.

The Store Theme will allow you to:

- Set a *default style* for all your store components.
- Set a *specific style* for a store component type or for a single component from all available in your store.

## Setting a default style for all store components

The theme's default visual style is configured in a single file named `style.json`, in the  Store Theme app's `style` folder.

This means that you can customize your entire store’s appearance by simply adjusting the default definitions declared in this file, without the need to customize components on each page.

For example: we can set the default theme background color to blue, by simply changing the `semanticColors` block’s `base` property:

```css
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

This is easy to do thanks to the [**VTEX Styleguide**](https://styleguide.vtex.com/#/Styles), a highly-configurable CSS framework responsible for defining the component style guideline. In it you can find a detailed explanation on the `styles.json` file structure to help with your customization. 

## Setting a specific style for a component type or a single component

The `style.json` file allows for a more generic customization of your store's visual style and can be very useful in most scenarios. 

However, you may want to create a more custom store identity, giving some components a more exclusive look with styles that are different than the default theme.

Picture the following scenario: your entire store uses blue as its main color, but you want your store's text components (rendered by `rich-text` blocks, as shown in the previous step) to be displayed in red. 

Let's also imagine that instead of all text components, you now want just one to be displayed in red - with the rest being displayed in the store's main color, blue.

For such an advanced customization, you can overwrite the default style declared in `styles.json` using **CSS Handles**, along with the `blockClass` prop for the last given example. 

If you are interested on applying advanced customization in your store's style, access the recipe on [**Using CSS Handles for store customization**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization/) for more instructions.





