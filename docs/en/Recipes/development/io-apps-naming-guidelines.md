# VTEX IO Apps naming guidelines

## Audience
- VTEX IO external developers

## Prerequisites
- Basic knowledge of how IO apps are structured

> **Disclaimer**: These are not guidelines for apps' implementations!

So, you're starting to develop a VTEX IO app and, as our development flow describes, you first need to **request permission** to *link* and eventually publish your app. You need to inform its **name**, **vendor**, **major** and also **what's the motivation for developing such app.** How should you better fill this information?

To avoid receiving a **"request denied"** from our whitelist team, we're here to clarify our **app naming**. Follow it, and you'll have a better chance to have your app's permission granted!

## Should you develop more than one app?

We often receive requests from partners developing one single functionality, but **for multiple apps**. For example, let's suppose you're developing an **integration with Instagram**(with vendor *you*) and you eventually need to have **an admin session**, **a backend service** and **a storefront page**. You may be inclined to request whitelist for the apps:

- `you.store-instagram` for exporting store blocks.
- `you.admin-instagram` for creating an session on admin.
- `you.instagram-graphql` for the backend service.

But, **there's no need for that** :no_entry_sign:. We at VTEX usually take this approach because our apps are used by multiple modules, but it's better to **keep functionality together**. Thanks to our **builder platform**, you can package all of those use cases **into one single app**:  `you.instagram` :white_check_mark:

It's even easier for other stores to install your app, since they'll only need one single command `vtex install you.instagram`, and not manage to install dependencies in order.

>  :heavy_exclamation_mark: Keep in mind to not abuse of this guideline and keep many functionalities into one generic app!

## App name

Beware that the app name you fill on the **whitelist form** will be the one you'll use on development, on the `manifest.json` file. **You should fill it correctly!**

Apps' names are *[kebab-case](https://en.wiktionary.org/wiki/kebab_case)*, or, basically, **just lowercase letters separated with hyphens**. They should also not contain special characters (like ., *, @...) or start with numbers (although they may have it elsewhere). 

And, of course, they should **concisely express the app's  purpose.** You should not call our Instagram example app `integration`, `social-media` or the target store/vendor's name! Also, **theme apps should only use the _store_ builder!**

### Dont's :no_entry_sign:
- `integration`
- `Instagram Integration`
- `i`
- `2plus2`
- `insta%gram`

### Do's :white_check_mark:
- `instagram-integration`
- `instagram`
- `store-name-theme`
- `service-b2b`


## Version

We follow the [Semantic Versioning specification](https://semver.org/) for versioning our apps, which impacts on how we release new versions. For development, **you should always start with major 0**, so, for new apps, **don't request whitelist for majors 1 or greater**.

If you want to know more about VTEX versioning and release process, check [this doc](https://vtex.io/docs/recipes/development/releasing-a-new-app-version/) on our VTEX IO documentation.

## Vendor

The `vendor` field on an app represents **its owner**, usually who is developing the application. A vendor always is a **VTEX account**. If the app is to-be sold on VTEX App Store, the `vendor` is the one to profit from its installations.

If you're gonna use that app on multiple accounts, **you don't need to request whitelist for every account as `vendor`**. 

## Details or motivation

This is one of the most important fields you need to fill on our **whitelist request form**, as it's gonna be determinant on our evaluation flow. It should be **as descriptive as possible!**.

### Dont's :no_entry_sign:
- `It's an integration with a marketplace`
- `It's for developing components of this store`

### Do's :white_check_mark:
- `This app will integrate a VTEX Storefront with Instagram API, making possible for the merchant to display its latests Instagram posts and stories. It will also allow style customization via Admin. We also need a backend service because of API quotas of the external service, since an application key is necessary for high usage`
- `The account I'm targetting with this app needs a frontend component to show the nearest physical store to the customer. Using the browser's geolocalization API, it fetches all the pickup points availabe on vtex.store-graphql and it displays the nearest one`

If you have question about our guidelines, feel free to reach us at [`store-discussion`](http://github.com/vtex-apps/store-discussion/)!
