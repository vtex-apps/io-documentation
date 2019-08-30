# IO Documentation

This is a central repository that structures [VTEX IO Docs](https://vtex.io/docs).

## How documentation works in VTEX IO?

Documentation in VTEX IO is built with the mindset that it should be closer to developers, in order to encourage scaling and maintenance. Therefore, what that means is that all the content that is on [VTEX IO Docs](https://vtex.io/docs) is dynamically rendered from each and every app's code on VTEX IO's registries, using the **Docs Builder**. 

## What is the Docs Builder?

The Docs Builder is a VTEX IO builder that reads the content in the `/docs` folder in the app's code, reads its markdown content and renders a page on [VTEX IO Docs](https://vtex.io/docs).

![diagram (1)](https://user-images.githubusercontent.com/18701182/64049859-9fc5bc80-cb4c-11e9-8072-4200ead73e9a.png)

Take for instance the `product-identifier` app, looking at the app's content structure, it's possible to see a `/docs` folder with a `README.md` 

![image](https://user-images.githubusercontent.com/18701182/64050596-f2a07380-cb4e-11e9-8ad2-69cc7cd850ff.png)

That will render a page on [VTEX IO Docs](https://vtex.io/docs) on a custom URL that references the app: 

[vtex.io/docs/app/**vtex.product-identifier**](https://vtex.io/docs/app/vtex.product-identifier)

The page produced is:

![image](https://user-images.githubusercontent.com/18701182/64051239-d00f5a00-cb50-11e9-93d1-29974d9803a4.png)

## How to structure an app to be built with Docs Builder

To be able to use the Docs Builder, you need to go through some quick steps:

1. Create a `docs/` folder on the root of the app

2. Update the app's `manifest.json` file to declare `vtex.docs` as one of the app's builders

![image](https://user-images.githubusercontent.com/18701182/64052096-a99eee00-cb53-11e9-8d69-925a451231ab.png)

3. Inside the `docs/` folder create a `README.md` file.

**DISCLAIMER:** In order not to have to keep track of two `README.md` files(one at the root of the project and the other at the `docs/` folder), you can delete the one at the root at the project and keep only the one at the `docs/` folder. GitHub will read the one at `docs/` on the landing page.
