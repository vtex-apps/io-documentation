# IO Documentation

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

**DISCLAIMER:** In order not to have to keep track of two `README.md` files(one at the root of the project and the other at the `docs/` folder), you can delete the one at the root of the project and keep only the one at the `docs/` folder. GitHub will read the one at `docs/` on the landing page.

## How to create multi page documentation
 
Docs builder will create complex pages with navigation handling and multipage content as well. To be able to accomplish that you need to: 

1. Create a `SUMMARY.md` file that follows the usual markdown summary format, for instance:
 
```
  - [Get started](README.md)
  - [Further](further.md)
      - [Even further](evenfurther.md)
```

2. Create the files following up the exact links you declared on your `summary` file

This will render a page with both a side bar that follows your `summary` implementation and that renders your multi page documentation. This very app (`vtex.io-documentation`) was created following up this architecture. 

## Contribution is easy and open-source on VTEX IO

Apps are, at the very beginning, programming code and they're are therefore stored on git repositories. Docs builder enables documentation contribution on a Pull Request/Merge Request level. 

**VTEX Open Source Native Apps and Documentation** are fully stored on [VTEX Apps Organization](https://github.com/vtex-apps) on GitHub, that means the documentation, as well as the code, is open source and may be contributed by creating new Pull Requests. 


## Keeping track of outdated docs

It wouldn't mean much if a tool for bringing documentation closer to the developer was created but no effort was done to create awareness of always keeping documentation up-to-date.

[VTEX Apps Organization](https://github.com/vtex-apps)  has, therefore, a bot [Docs Bot](https://github.com/vtex-apps/docs-bot) that is vigilant on documentation status. Its responsibilities are:

- Checks if PRs come with documentation changes and, if they don't, checks the reason for that. In case it's just because the timing is not good, then an issue is created at [IO Documentation](https://github.com/vtex-apps/io-documentation) and a note is created at the `README.md` of the repo to report that new documentation is coming soon.
- Creates issues weekly for repos that don't have their documentation structured properly

[Docs Bot](https://github.com/vtex-apps/docs-bot) is an **open-source** project and may be used at any third-party repo/organization with only a few tweaks. Also, it's contributions are encouraged to make it even more powerful, if **VTEX IO Docs** are important for you.
