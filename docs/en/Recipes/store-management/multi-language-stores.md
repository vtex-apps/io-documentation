# Multi-language stores

Before making your e-commerce global, it's essential to take care of its website's content internationalization.

After detecting a user locale, every text from your storefront components that is set as translatable (i.e., message) will be automatically translated either by the automatic translation service, the storefront app's settings, or custom content personalized through a GraphQL mutation.

>ℹ️ A locale is the set of parameters regarding a language, region, and other regional particularities used to format the front-end data of a website.

Concerning the front-end content of a store's website, text data can be provided either by the settings of an app or by the Catalog API. 

>ℹ️ The Catalog API is one of the multiple REST APIs that compose the VTEX Administrative panel. This particular API is responsible for manipulating a store’s sales channels, categories, brands, products, SKUs, and specifications.

While app messages are specifications from front-end components, catalog messages are external data from the [Catalog API](https://developers.vtex.com/reference/catalog-api-overview).

Translations, therefore, must consider the different natures of these two kinds of content. 

In the following, we discuss how VTEX IO handles both cases.

## Storefront content internationalization

As the VTEX IO platform makes use of tailor-made React components for storefront end, it's important to get to know React basics and how VTEX IO handles these components translations.

Similarly to JavaScript functions, React components accept arbitrary arguments as `props`, and return React elements that describe what should be rendered on a page.

>ℹ️ Leveraging the VTEX IO platform, the [VTEX IO Store Framework](https://developers.vtex.com/docs/frequently-asked-questions) solution delivers the needed foundations for any storefront structure, providing high quality, customizable React store blocks so that you can build (in the fastest possible go-to-market time) comprehensive shopping experiences that never get old.

Regarding multi-language stores, one of the advantages of using React is the possibility of rendering content translations on the client-side. This way, no refresh or re-render of the page is needed, and a high-performance result is achieved.

By using the [react-intl](https://www.npmjs.com/package/react-intl) internationalization (i18n) library along with the VTEX IO Messages app, it's possible to manage and have automatic translations of every storefront text content set as translatable (i.e., *message*).

Therefore, to turn a generic text into a *message*, meaning, to indicate that a specific text component from the storefront app must be translated, the `<Formatted*>` component from the *react-intl* library must be used. 

Once every message is set up, the current locale and set of translated messages obtained from the *automatic translation system* will be provided at the root of the component tree and made available to the component.

However, since automatic translations can be unsatisfactory considering cultural factors and literal translations, the Messages app provides functionalities to manage custom translations.

This can be performed on an app or account level. 

For an app level, that means using the Messages builder to set personalized messages for each locale. These translations are set in different files named over each locale inside the `/messages` folder. With this, every store using this specific storefront app will import these overwritten messages translations.

>ℹ️ To learn how to set messages during the development of a React component, please follow this [guide.]()

At the account level, using the Messages app means overwriting a message imported from an app with a complete customized message. To perform this action, the appropriate GraphQL API request must be sent to the Messages app.

>ℹ️ To learn how to overwrite a message from a storefront app, please follow this [guide](https://developers.vtex.com/docs/storefront-content-internationalization).

To sum it up, with the Messages app it's possible to overwrite an automatic translation with a more specific or representative content of your store, such as a special login message for Spanish speaking users from Argentina.

The Messages app is a standalone translation application and might not be confused with a string repository. This means that, for it to work at its basic one must provide a source language, a source content, and a destination language. The output will be the translation of the source content at the source language to the destination language.

To make it more tangible, it's important to understand the Messages app decision flow.

Considering a message pointed out as translatable, the Messages app will first go through custom account-defined content. 

Therefore, if no definitions are found, the Messages app will go through the storefront app translations defined in the `/messages` folder of the component's development folder. 

In the sequence, if no specific translation is still not found, then the Messages app will fall back to the automatic translation service.

Since translating an app to every language is an arduous task, we suggest that you structure a precise translation for your target audience and let the automatic translation do the heavy lifting on the other languages for you.

Moreover, it's important to highlight that the Messages app aggregates all the translation services in the platform, regardless of the app nature (backend or frontend) and the actor (e.g., user, app, or automatic translation service) which contributed to that translation.

## Catalog internationalization

So far, we've talked about app messages - text messages exported from a storefront app (declared in its `message` folder), such as a text component from a React block. However, we also have catalog messages - messages related to a product name or a product description from the store catalog, which play an essential role in store internationalization.

Every data from the Catalog API, such as a product name and a product description, is already set as translatable. Therefore, it's possible to overwrite an automatic translation of the catalog by sending the appropriate GraphQL query either to the Catalog API or to the Messages app.

>ℹ️ To learn how to overwrite a catalog message through the Catalog API, please follow this [guide](https://developers.vtex.com/docs/catalog-internationalization).
