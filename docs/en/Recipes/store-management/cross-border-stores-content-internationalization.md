# Cross-border store content internationalization

If you're familiar with the [multidomain](https://help.vtex.com/en/tutorial/creating-multi-store-multi-domain--tutorials_510?locale=en) concept, you know that, in VTEX, an account with multiple bindings, and different sales channels for each one of its local stores characterizes a cross-border store.

However, each one of these local stores can also have the necessity for translations into multiple languages. For example, a Canadian store binding may need a French or an English version of its website.

As each store of a VTEX account in a multidomain environment is independent, content internationalization, as presented in the [Multi-Language stores](https://developers.vtex.com/docs/multi-language-stores-2) guide, is handled mostly the same way as for a VTEX account with a single store.

Moreover, cross-border stores that share the same catalog can also have their catalog URLs translated into other languages. In the following section, we present this feature.

## Translatable URLs

[Rewriter](https://developers.vtex.com/docs/rewriter) is the VTEX IO app responsible for managing product, search, and navigation routes - client-side defined routes related to VTEX IO custom paths and pre-defined templates, such as [department](https://github.com/vtex-apps/store/blob/master/store/routes.json#L27), [brand](https://github.com/vtex-apps/store/blob/master/store/routes.json#L21), and [category](https://github.com/vtex-apps/store/blob/master/store/routes.json#L33) routes.

>ℹ️ To learn more about Routes in VTEX IO, please follow [this link](https://developers.vtex.com/docs/routes).

The main objective of this app is to make it possible to render requested pages based on shorter rewritten URLs. For example, a route such as `http://{storename}.com/_v/segment/routing/vtex.store@2.x/product/3/blouse/p` can be understood by its canonical `http://{storename}.com/blouse/p`.

Notice that the canonical path is a unique string that contains the route's shortest absolute path. Its usage allows not only more friendly URLs but also better SEO ranking.

Hence, whenever a request is made in any VTEX IO website, the requested URL is decomposed into parameters, which are interpreted by the Rewriter app and forwarded to the proper rendering pipeline.

Since every route stored in the Rewriter app carries additional related data, such as the respective `binding` in which it is available, the way VTEX IO handles routing allows setting personalized URLs for each local store.

That means cross-border stores can also have their catalog URLs translated into other languages. For example, a cross-border store that operates in the USA and Argentina, sharing the same catalog, could have two different slugs for the same product: one in English and the other in Spanish.

Hence, a product registered under the `yellow-dress` slug, for example, as in `http://{storename}.com/us/yellow-dress/p`, could have its slug translated to `vestido-amarillo`, as in `http://{storename}.com/ar/vestido-amarillo/p`.

>⚠️ Keep in mind that catalog URLs translations are accepted for each `binding`, not for a single multi-language store.

>ℹ️ To learn how to translate a catalog URL, please follow this [guide](https://developers.vtex.com/docs/catalog-internationalization).

By sending the desired URL translation via the right GraphQL mutation to the Catalog API, an alias of the main route is automatically created in the Rewriter app. 

These aliases are stored in the `resolveAs` field of its related internal route.

Hence, considering the previous example, the route `/yellow-dress` in the Argentine binding would have an alias route `/vestido-amarillo` stored in its `resolveAs` field.

Besides internal routes, the Rewriter app also manages redirects, which are custom paths a route should also resolve to. Therefore, redirects can also be part of your store's internationalization strategy.
