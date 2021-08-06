---
title: Engineering guidelines
description: "Engineering guidelines enforced by the VTEX App Store to guarantee a baseline standard of quality, viability and usability for all apps available for VTEX stores."
date: "2021-07-21"
tags: ["app-store", "app", "development", "Engineering guidelines"]
version: " "
git: " "
---

# Engineering guidelines

## Scalability and performance
When installing an app from the [VTEX App Store](
https://apps.vtex.com), the retailer needs to feel secure and comfortable about their store's performance. Big brands using our platform make thousands of sales per minute and a few moments out of service can mean big financial losses.

Use the [VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/what-is-vtex-io) infrastructure to build and deploy your extensions. Our development platform is maintained on top of modern infrastructure and cloud computing to ensure that your software runs without bottlenecks 24/7.

If you still choose to use external APIs in your application development, make sure that they are fast and highly scalable. Remember that when you decide to offer your app on the VTEX App Store, it will be available to brands of all sizes, across different time zones and business calendars. In this context, relying on a manual system with on-demand scalability can become a huge risk in terms of performance.

> ℹ️ During the homologation process, a series of load tests will be performed under different conditions to ensure that your application is scalable. This includes, for example, testing the response time of your APIs at request levels similar to those experienced on Black Friday. At any sign of a crash or failure to respond, your app will fail for performance issues.


## Security and data privacy
With increasingly stringent regulation on data traffic, usage and storage around the world, VTEX seeks to ensure that all points of contact between our retailers, their customers and other parts of the ecosystem are protected and secure.

At the development level, we are very strict about each piece of data requested by your application to our APIs. You should request only data that is essential for the app to work.

Also, always make it clear, both in your documentation and in your app's terms of use, what data, modules, APIs, and general information are being used in your extension, how they will be accessed, and why they are necessary for it to work.

It is critical that your data policy is as clear and public as possible so that retailers are not vulnerable when agreeing to the use and storage of their information.

### Handling security breaches
If despite all this caution you still identify any security issues with the app after publishing it, remove it from the VTEX App Store to avoid further installations of the unstable version.

Then notify us of the issue by [opening tickets](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) so that we can provide support to retailers operating with this version and guide them on how to remove it from their stores.

Finally, fix the security flaw and resubmit your application for homologation. Once the new version is approved, the app will be available again in the VTEX App Store.


## Coding standards
In addition to the broader security and performance guidelines, there are important development standards for publishing the application.

We value clear, well-formatted and easy-to-read codes. Therefore, please follow the criteria listed below before submitting your application:
- Remove unnecessary comments from the code
- Remove the `console.log()` command — it should not be used in production environments
- Always use the `import` command instead of `require` to import references into Typescript files
- Always use the `const` command instead of `let` or `var` to declare elements in Typescript files
- Follow the proper order for importing references into Typescripts files: 
    1) External dependencies; 
    2) Other VTEX apps; 
    3) Local modules of your code.

- Avoid implementing routes and resolvers directly in the `index.ts` file. Instead, implement the middleware functions in other files and import them into the main file

> ℹ️ Check out the free content about development on [VTEX IO](https://learn.vtex.com/). In this course, you will find technical requirements of the development platform, examples, do's and don'ts and answers to the main questions that may arise along the development journey. It will guide your learning at the code level, complementing the guidelines outlined in this section.

### VTEX builders
[Builders](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders) work as an API responsible for configuring other IO services in your app.
For developing and publishing software in the VTEX App Store, some specific builders need to be up-to-date in your application's code: 

- Node builder - version 6.x
- React builder - version 3.x
- Admin builder - version 1.x
- Messages builder - version 1.x
- Docs builder- version 0.x
- Graphql builder -version 1.x

### Styles and visual specs
To ensure your front-end code is performant, use [Tachyons](https://tachyons.io/), a modern framework for writing CSS styles.

In order not to increase the response time for users, avoid external Javascript libraries when rendering component content. Give preference to the [React Hooks](https://pt-br.reactjs.org/docs/hooks-reference.html) API.

Finally, do not use hardcoded labels in your code. If your app works with text components, create a structure of constants in a `constants.ts` file and import their content dynamically. To translate these labels into other languages, always use _messages builder._

### Security and authentication
At the authentication level, do not use VTEX’s appKey and appToken framework in your app routes, as this is an option focused on communication with channels external to the platform.

Instead of this key pair, use user authentication or an app token to communicate with other VTEX services.

Also, never import other libraries to handle external HTTP requests. It is mandatory to use the [VTEX IO clients](https://developers.vtex.com/vtex-developer-docs/docs/how-to-use-and-create-clients-on-vtex-io) for this type of communication.
