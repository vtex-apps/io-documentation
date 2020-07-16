# Routes

Routes are used to define the URL path related to a store's page template. 

In VTEX Store Framework, some default page templates page with predefined URL paths are already available, such as the [home page](https://github.com/vtex-apps/store/blob/master/store/routes.json#L2), [product page](https://github.com/vtex-apps/store/blob/master/store/routes.json#L11), [login page](https://github.com/vtex-apps/store/blob/master/store/routes.json#L8), etc. 

However, it's also possible for you to create a [*custom* landing page](https://developers.vtex.com/docs/vtex-io-documentation-creating-a-new-custom-page). In this case, custom routes can be defined in the `routes.json` file inside the app's `store` folder, according to the following example:

```json
{
    "store.custom#{templatename}": {
      "path": "/{URL}"
    }
}
```

In this example, `store.custom#{templatename}` is the name of the custom page template declared within your store's `blocks` folder and `path` is the root-relative URL that you want your page to be accessed by users.

:information_source:  **Tip**: *You can set a path that accepts URL parameters and optional parameters as in: `/path/:param(/:optional-param)`.*

Optional props such as the ones presented in the following table can also be added to your route's definition, according to your desired scenario:

| Prop | Type | Description |
| ---- |------| ----------- |
| `title` | `string` | The title of your custom route used as an identifier in the account's admin (CMS > Pages). |
| `canonical` | `string` | A unique string containing the shortest absolute path used for defining the canonical URL. For example, consider the path `/_v/segment/routing/vtex.store@2.x/product/:id/:slug/p`. Its canonical path is `/:slug/p`.|
| `isSitemapEntry`| `boolean` | A prop that allow your custom page to be displayed in your store's [sitemap](https://github.com/vtex-apps/store-sitemap/blob/2.x/README.md) when set as `true`. |
