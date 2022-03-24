---
title: Engineering guidelines
description: "Engineering guidelines enforced by the VTEX App Store to guarantee a baseline standard of quality, viability and usability for all apps available for VTEX stores."
date: "2021-07-21"
tags: ["app-store", "app", "development", "Engineering guidelines"]
version: " "
git: " "
---

# Engineering best practices
Refer to the following guidelines to guarantee the quality and usability of your VTEX IO app during development. 

> ⚠️
>
> Notice that you must respect these guidelines if you aim to publish your app at the VTEX App Store.
> 
## Scalability and performance
Use the [VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/what-is-vtex-io) infrastructure to build and deploy your extensions. The VTEX IO development platform uses cloud computing to ensure that your app runs without bottlenecks 24/7.

### Dos and Don'ts

- If you opt to use external APIs in your app development, make sure they are fast and scalable. 

- Remember that when you offer your app on the VTEX App Store, your app becomes available to brands of all sizes across different time zones and business calendars. In this context, relying on a manual system with on-demand scalability can become a huge risk in terms of performance.

> ℹ️ Info
> 
> During the [homologation process](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-homologation-requirements-for-vtex-app-store), a series of load tests are performed under different conditions to ensure that your application is scalable. This includes, for example, testing the response time of your APIs at request levels similar to those experienced on Black Friday. At any sign of a crash or failure to respond, your app will fail for performance issues.


## Security and data privacy
To ensure that all points of contact between our retailers, their customers, and other parts of the ecosystem are protected and secure, we test if your app respects regulations on data traffic, usage, and storage worldwide.

At the development level, we are very strict about each piece of data requested by your application to our APIs.

### Do's and Don'ts

- Request only data that is essential for the app to work.
- Be clear, both in your documentation and in your app's terms of use, what data, modules, APIs, and general information are being used in your app, how they will be accessed, and why they are necessary for it to work.
- Make sure your data policy is as clear and public so that retailers are not vulnerable when agreeing to the use and storage of their information.

### Handling security breaches
Nevertheless, If you identify any security breaches after publishing your app, take the following measures:

1 - Remove your app from the VTEX App Store to avoid further installations of the unstable version.

2 - Notify us of the issue by [opening tickets](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) so that we can provide support to retailers operating with this version and guide them on how to remove it from their stores.

3 - Fix the security flaw and resubmit your application for homologation. 

Once the new version is approved, the app will be available again in the VTEX App Store.


## Coding standards
In addition to security and performance guidelines, you must follow some coding standards before publishing your app at the VTEX App Store.

We value clear, well-formatted and easy-to-read codes. Therefore, please follow the criteria listed below before submitting your app:
- Remove unnecessary comments from the code.
- Remove any commands used for debugging, such as `console.log()` — it should not be used in production workspaces.
- Always use the `import` command instead of `require` to import references into Typescript files.
- Always use the `const` command instead of `let` or `var` to declare elements in Typescript files.
- Follow the order below when importing references into Typescripts files: 
    1) External dependencies; 
    2) Other VTEX apps; 
    3) Local modules of your code.

- Avoid implementing routes and resolvers directly in the `index.ts` file. Instead, implement the middleware functions in other files and import them into the main file

> ℹ️ Info
> 
> Check out the free [VTEX IO](https://learn.vtex.com/) courses. In these course, you will find technical requirements of the development platform, examples, do's and don'ts, and answers to the main questions that may arise along the development journey. They will guide your learning at the code level, complementing the guidelines outlined in this section.

### VTEX builders
[Builders](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders) work as an API responsible for configuring other IO services in your app.
For developing and publishing apps for the VTEX App Store, the following builders must be up-to-date in your app's code: 

- Node builder - version 6.x
- React builder - version 3.x
- Admin builder - version 1.x
- Messages builder - version 1.x
- Docs builder- version 0.x
- Graphql builder -version 1.x

### Front-End
To ensure your front-end code is performant, take the following recommendations: 

- Use [Tachyons](https://tachyons.io/), a modern framework for writing CSS styles.

- Avoid external Javascript libraries when rendering component content to avoid increasing time-response for users. Give preference to the [React Hooks](https://pt-br.reactjs.org/docs/hooks-reference.html) API.

- Do not use hardcoded labels in your code. If your app works with text components, create a structure of constants in a `constants.ts` file and import their content dynamically. To translate these labels into other languages, always use _messages builder._

### Security and authentication
At the authentication level, take the following requirements

- Do not use VTEX’s appKey and appToken framework in your app routes, as this is an option focused on communication with channels external to the platform.

- Use user authentication or an app token to communicate with other VTEX services instead of a key pair.


- Never import other libraries to handle external HTTP requests. It is mandatory to use the [VTEX IO clients](https://developers.vtex.com/vtex-developer-docs/docs/how-to-use-and-create-clients-on-vtex-io) for this type of communication.

## Plug&Play
For homologation approval, it is required that your app is plug and play. Those interested in your app should:

- Be able to install and configure it using only the VTEX Admin panel.

- Not considered external assistance to support the app implementation process.

## Support channel
Every app in the VTEX App Store must:

- Provide a direct support channel for retailers who install it, such as email, phone, ticketing tool, or a combination of these options.

- Have the first response time up to eight business hours in the developer's time zone. This requirement aims to ensure that store operations will not be affected by errors in third-party applications.

## Documentation
While [developing your app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-an-app) and [preparing the app for distribution](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-preparing-your-app-distribution), make sure to provide official documentation that supports future users in implementing and understanding your app. 

The app documentation should include:
- Technical and commercial requirements for the app's operation.
- Installation and configuration guides.
- Answers to frequently asked questions.

## Next

- Coming soon: Documentation best practices. 

