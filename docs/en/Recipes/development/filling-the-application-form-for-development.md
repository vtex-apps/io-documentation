---
title: Filling the Application form for development
description: "Find now all guidelines regarding the VTEX IO Application form to make it easier for you to start developing on the platform!"
date: "2020-04-28"
tags: ["application", "form", "development", "naming", "versioning", "guidelines"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/development/filling-the-application-form-for-development.md"
---

# Filling the Application form for development

The VTEX IO platform currently works as a **closed beta solution**, only accessible for a small group of developers, for the following development projects: 

- **Custom Admin Apps**
- **Custom back-end Apps**
- **Custom Pixel apps**
- **Custom mobile Apps**

>ℹ️ Every VTEX account and partner can freely use the VTEX IO to develop custom storefront components, meaning that the platform works as an open beta solution when it comes to React projects. The Application form is therefore not needed for this scenario.

To become part of this group, you need to first fill in the [**Application form**](https://docs.google.com/forms/d/e/1FAIpQLSfhuhFxvezMhPEoFlN9yFEkUifGQlGP4HmJQgx6GP32WZchBw/viewform) which is used by our product team to properly peruse your development project and grant you all the necessary permissions after your project has been approved.

During this process, you may feel uncertain as to which permission best suits your scenario, or about what to name the new app or even about how much detail to provide on the project when filling in the form.
  
To help answer some of these questions, we've put together **guidelines regarding the VTEX IO Application form** which will make it easier for you to start developing on the platform.

## Guidelines

### Apps development by functionality

Faced with a more complex project, that involves storefront components and a back-end service, for example, developers tens to request permissions to develop multiple apps aimed at each of these well defined platform functions.

The problem with this code segmentation is that it's done from a developer's point of view, someone who unlike the end user, has technical know-how about the platform. For end users, micro-services done behind the scenes on the platform are not what matter.

Therefore, the existence of several small apps that when put together solve a single problem can become frustrating from a user's perspective - and with good reason. 

**It's crucial for users to be able to solve any problem in the most practical way possible**, using the solution given by a single app. This includes a **seamless installation process**.  
  
>⚠️ Be careful however: overly generic apps, which bundle up a lot of distinct functionalities, are also not recommended mainly because the code can become complex and heavy.

The most important practice is to **understand which service your app is meant to offer end users** and, based on that, decide how your development is going to be. Make sure that each functionality is correctly working towards delivering the desired result.

### App naming

The app name filled in our Application form must be permanent. In other words, this means that you should be careful when choosing it once the name filled in also must be the one used in the app's `manifest.json` file. 

On the VTEX IO platform, apps' names are *[kebab cased](https://en.wiktionary.org/wiki/kebab_case)*. Basically, they must be comprised of lowercase letters separated by hyphens. Special characters, such as `*` and `@`, and numbers in the beginning of the name are not recommended.

When choosing the app name, remember: it should **concisely express the app's purpose.** 

To put this into practice, let's imagine that an app is developed for a native integration with Instagram. You should not name it `integration` or `social-media`, for example. Instead, the best choices for this scenario would be `instagram-integration` or simply `instagram`.

### App versioning

The VTEX IO Platform uses the [**Semantic Versioning specification**](https://semver.org/) for versioning all apps developed on it.

It means that if you're requesting to develop an app from scratch, you should always start with major `0`.

### Apps' vendor

The app's vendor is the **app's owner**, the VTEX account that is developing the application. 

If the app is to-be sold on VTEX App Store, the `vendor` is the one to profit from its installations. Therefore, remember the following: even is the app is installed on multiple accounts, you don't need to change the app's vendor value for every one of them. **An app must have only one vendor, which is responsible for its development and maintenance**.

### Project's motivation

Your development project should be **as descriptive as possible!** This means that you should provide as many details as possible, such as the project's need, objective and impact. 

#### Dont's

- "*It's a marketplace integration.*"

#### Do's

- "*This app will integrate a VTEX Storefront with Instagram API, allowing merchants to display their latests Instagram posts and stories. It will also allow style customization via Admin. We also need a backend service because of the external service's API quotas, since an application key is necessary for high usage.*"

If you have any question about these guidelines or about the Application form, feel free to contact our team on [Store Discussion](http://github.com/vtex-apps/store-discussion/)!
