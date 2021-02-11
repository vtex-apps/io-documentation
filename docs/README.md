# IO Documentation

## How documentation works in VTEX IO

Documentation in VTEX IO is built with the mindset that developers should have it at hand, in order to encourage its scaling and maintenance. Therefore, what that means is that all [VTEX Developer Portal](https://developers.vtex.com/) content is dynamically rendered from the code of each and every app in VTEX IO's registry, using the **Docs Builder**. 

## Docs Builder

The Docs Builder is a VTEX IO builder that access the `/docs` folder contained in the app's code, reading its markdown content and rendering it as a page in [VTEX Developer Portal](https://developers.vtex.com/).

![diagram (1)](https://user-images.githubusercontent.com/18701182/64049859-9fc5bc80-cb4c-11e9-8072-4200ead73e9a.png)

Take for instance the `product-identifier` app. Looking at the app's content structure, it's possible to see a `/docs` folder with a `README.md` .

![image](https://user-images.githubusercontent.com/18701182/64050596-f2a07380-cb4e-11e9-8ad2-69cc7cd850ff.png)

That will render a page in [VTEX Developer Portal](https://developers.vtex.com/) with a custom URL that makes reference to the app: 

[https://developers.vtex.com/vtex-developer-docs/docs/**vtex-product-identifier**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-identifier)

The page created is as follows:

![image](https://user-images.githubusercontent.com/67089688/107689913-3118e800-6c88-11eb-9533-346ea698ee45.png)

## Structuring an app so that it can be built with Docs Builder

To be able to use the Docs Builder, you need to go through some quick steps:

1. Create a `docs/` folder in the app’s root.
2. Update the app's `manifest.json` file to declare `vtex.docs` as one of the app's builders.

![image](https://user-images.githubusercontent.com/18701182/64052096-a99eee00-cb53-11e9-8d69-925a451231ab.png)

3. Inside the `docs/` folder create a `README.md` file.

**DISCLAIMER:** in order to not have to keep track of two `README.md` files (one in the project’s root and another it the `docs/` folder), you can delete the former and only keep the latter. GitHub will read the one from the `docs/` folder and render it on the landing page.

## How to create multipage documentation
 
Docs builder will create complex pages with navigation handling and multipage content as well. To be able to accomplish this, you need to: 

1. Create a `SUMMARY.md` file that follows the usual markdown summary format, for instance:
 
```
  - [Get started](README.md)
  - [Further](further.md)
      - [Even further](evenfurther.md)
```

2. Create the files according to the exact links you declared in your `summary` file.

This will render a page with a sidebar that follows your `summary` implementation and also renders your multipage documentation. This very app (`vtex.io-documentation`) was created from this blueprint. 

## Contribution is easy and open-source in VTEX IO

Apps are, at their core, bits of programming code and are therefore stored in git repositories. Docs Builder enables documentation contribution on a Pull Request/Merge Request level. 

**VTEX Open Source native apps and documentation** are fully stored in the [VTEX Apps Organization](https://github.com/vtex-apps) on GitHub, meaning that the documentation, as well as the code are open-source and may be contributed to by creating new Pull Requests. 

## Keeping track of outdated docs

It wouldn't mean much if a tool for bringing documentation closer to the developer was created but no effort was pursued in creating the awareness of always keeping that documentation up-to-date.

As a result, [VTEX Apps Organization](https://github.com/vtex-apps) has the [Docs Bot](https://github.com/vtex-apps/docs-bot) constantly monitoring the documentation status. Its responsibilities are:

- To check if Pull Requests accompany documentation changes and, if they don't, to check the reason behind that. If it’s simply a timing issue, then an issue is created in the [IO Documentation](https://github.com/vtex-apps/io-documentation) and along with a note in the repo’s `README.md` to report that new documentation is coming soon.
- To create issues weekly for repos that don't have their documentation structured properly.

[Docs Bot](https://github.com/vtex-apps/docs-bot) is an **open-source** project and may be used by any third-party repo/organization with just a few tweaks. Also, contributions to it are encouraged to make it even more powerful.
