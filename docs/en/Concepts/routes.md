# Routes

A route maps a URL pattern and an HTTP request method to an action. It's, therefore, a way of setting the application expected behavior for client requests to specific endpoints.

In VTEX IO, however, you don't need to worry about routing and HTTP request methods, since this is handled by the [Rewriter app](https://developers.vtex.com/vtex-developer-docs/docs/rewriter) or by the VTEX IO native builder called [Store](https://github.com/vtex-apps/store), depending on the route type.

Therefore, all you need to know is how to create and manage route paths and page templates.

In this sense, it's important to know that VTEX IO routes can be classified into four different categories: 

- Product routes - routes related to product pages.
- Search routes - routes related to search pages.
- Navigation routes - client-side defined routes related to VTEX IO custom paths and pre-defined templates, such as [department](https://github.com/vtex-apps/store/blob/master/store/routes.json#L27), [brand](https://github.com/vtex-apps/store/blob/master/store/routes.json#L21), and [category](https://github.com/vtex-apps/store/blob/master/store/routes.json#L33) routes.
- Custom routes - routes created by the user to handle custom landing pages.

The Rewriter app is responsible for managing the first three route types: it interprets the requested path, identifies the route type, and, in the sequence, forwards the route path to the rendering pipeline.

The Store builder, in turn, is responsible for managing custom routes. Hence, custom routes are not stored in the Rewriter app, meaning that their paths are directly forwarded to the render server.

## Routes in Rewriter

Commonly, routes stored in the Rewriter have complex paths since they communicate with other systems and databases. For example, when a user registers a new category, subcategory, or product in the VTEX IO Admin, its related pages are automatically created in the Rewriter database.

Take the product route as an example. Its standard path is `/_v/segment/routing/vtex.store@2.x/product/:id/:slug/p`. Notice that this path is not user-friendly in the client-side context and, consequently, a solution that provides a more personable path is needed.

Hence, in Rewriter, besides the path itself, a route definition must include a canonical path for client-side usage and enhanced SEO rankings. 

The canonical path is the unique string that contains the route shortest absolute path. For the product route example, its canonical is `/:slug/p`.

Now, to better understand the rendering process of a page in VTEX IO, it's important to know that the render server recognizes only the *path* property of a route. Therefore, the Rewriter app is an interface that intermediates the client request of a canonical and the rendering process.

Rewriter interprets the *canonical path* received from the client request and translates it into the route *path* itself. In the sequence, to finally display the requested page, Rewriter forwards the route *path* to the rendering pipeline.

## Custom routes

In VTEX IO, search, product, and some navigation pages with preset paths are already available, such as [home page](https://github.com/vtex-apps/store/blob/master/store/routes.json#L2), [product page](https://github.com/vtex-apps/store/blob/master/store/routes.json#L11), [login page](https://github.com/vtex-apps/store/blob/master/store/routes.json#L8), etc.

However, it's also possible to create [*custom* landing pages](https://developers.vtex.com/docs/vtex-io-documentation-creating-a-new-custom-page). 

In this case, routing is handled by the Store builder, meaning that custom routes are not stored in the Rewriter app and that their paths are directly forwarded to the render server.

Hence, to create a custom route in VTEX IO, all that is needed is a page template and a path.

These routes must be declared in a `routes.json` file inside the store's `store` folder as in the following example:

```json
{
    "store.custom#{templatename}": {
      "path": "/{URL}"
    }
}
```

Where `store.custom#{templatename}` is the name of the custom template declared within the store's `blocks` folder, and `path` is the root-relative URL where the page will be available.

>ℹ️ **Tip**: A path can accept URL parameters and optional parameters as in: `/path/:param(/:optional-param)`. But we recommend that you keep it simple since paths of custom pages are the ones used in the client-side and search engines.

Optional props such as the ones presented in the following table can also be added to a custom route definition.

| Prop | Type | Description |
| ---- |------| ----------- |
| `title` | string | The name of the custom route used as an identifier in CMS > Pages. |
| `isSitemapEntry`| boolean | Makes the route available in the store [sitemap](https://github.com/vtex-apps/store-sitemap) when set as `TRUE`.|
