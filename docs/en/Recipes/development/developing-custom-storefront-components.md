---
title: Developing custom storefront components
description: "Learn the guidelines adopted by our very own product team to cooperate with your development journey using Store Framework, VTEX IO and the React technology."
date: "2021-03-12"
tags: ["storefront", "component", "react", "development", "block", "best-practices"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/edit/docs/en/Recipes/development/developing-custom-storefront-components.md"
---

# Developing custom storefront components

During the development process, it is natural to face,  among other issues that directly affect the shopping experience, critical questions regarding performance and internationalization.

Although **VTEX does not grant any support for custom projects**, we have put together the guidelines adopted by our very own product team to cooperate with your development journey using Store Framework, VTEX IO and the React technology. 

Find below the best practices regarding tooling, features, flexibility, scalability, performance, accessibility, internationalization, and styling, to be adopted when creating your storefront component.

>⚠️ 
> 
> Before applying the configurations stated below, it is highly recommended that you understand how VTEX IO, Store Framework and React work since the guidelines take into account previous knowledge. You can take a closer look at the [VTEX IO learning course](https://learn.vtex.com/) and the [React official documentation](https://reactjs.org/) for support.*

## Tooling

When creating a custom component, use tools to ease the code development by automatically formatting and testing it.

Features such as [ESLint](https://eslint.org/), [Typescript](https://www.typescriptlang.org/), and [Prettier](https://prettier.io/) are not mandatory for project deployment, but they help development, code maintenance, and testings. 

The [React App repository](https://github.com/vtex-apps/react-app-template) is the go-to model template for tooling since it provides formatting features and the [VTEX Test Tool](https://github.com/vtex/test-tools), a native testing tool from VTEX that leverages from [Jest](https://jestjs.io/).

Use Typescript types as an ally in your development journey since they provide autocomplete tools that can be used when developing and importing a new component. To have them at hands, run the following command in your terminal: 

`vtex setup --typings`   

>⚠️ 
> 
> The command above will install all Typescript types from the apps listed in the app's `dependencies` list in your project. Whenever you add a new dependency, the command must be executed again.

## Feature development

### Store-specific

A typical slip is to design a component to perform different tasks on the screen, aiming to reuse code and develop a more *"significant"* project.

Do not lose track of what you desire as the component's primary goal: **the more specific, the better!** 

Keep it simple. Components with several functionalities tend to mislead users on the interface and represent a big package of code to manage behind the scenes, especially when handling with APIs. 

### Native-first 

Before developing a custom component from scratch, make sure VTEX does not already offer the same feature natively through the [Store Framework's native components](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-components).

Create your component importing and combining native components in order to achieve a better result. For example:

```tsx
import React from 'react'
import { ProductSummaryList } from 'vtex.product-summary'

interface Props {
  title?: string
}

function Shelf({ title }: Props) {
  return (
    <div>
      <h3>{title}</h3>
      <ProductSummaryList />
    </div>
  )
}

export default Shelf
```

> ℹ️ 
> 
> Notice how the Store Framework solution counts on specific apps for [integrations with 3rd solutions](https://developers.vtex.com/vtex-developer-docs/docs/vtex-accessibe) and [layout structuring](https://developers.vtex.com/vtex-developer-docs/docs/vtex-condition-layout), besides having template components that play a particular role once rendered to the final users, such as the [Product Identifier app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-product-identifier). When developing your storefront component, keep in mind that segmentation is the key to a light code and successful component!

## Flexibility and scalability

### Rendering 

Your component should be flexible in dealing with all possible scenarios once rendered.

Be careful not to only think about its appearance when fully rendered. It is important to consider all other possible statuses during the rendering process, such as:

- `Loading` - When the component is already visible to users but not fully rendered due to data loading. 
- `Error` - When the component could not be rendered due to an error.
- `Empty` - When the component could not fetch data and therefore is rendered with empty content.

> ℹ️ 
> 
> The Render Runtime is the VTEX app responsible for rendering the storefront. Check out the [app documentation](https://github.com/vtex-apps/render-runtime) and get to know some valuable variables to your project.

Also, be careful with the usage of browser variables, such as `window` and `document`, since they only exist in the browser context and may harm your component display when opting for server-side rendering. 

Before implementing your component, check which variables are available on browser using the [Render Runtime](https://github.com/vtex-apps/render-runtime#canusedom)'s `canUseDom` variable.

### Browser compatibility

The VTEX IO platform automatically provides JavaScript polyfills responsible for implementing features on web browsers that are not able to. 
 
Although this practice ensures the good performance of your component in several user agents, you may work with NPM libraries that can not be implemented in old web browsers. 

Check out which web browsers are more common among your audience and focus on them when developing your storefront component. Despite the fact that the Internet Explorer is falling into disuse, some stores are still IE11-oriented, for example.  

### Prop substitution

The simplicity presented by boolean props, which toggle component behaviors between `true` and `false`, makes them well-employed in React projects.

However, they do not present great scalability considering that the component evolution may ask for a third (or more) behavior to be enabled. 

Boolean props, therefore, demand creating brand new props whenever unprecedented use cases are introduced to your component. 

>⚠️ 
> 
> Once the component is deployed, avoid managing its props (creating, removing, and/or updating them)! Managing props can be costly since it can directly impact the API's maintenance and therefore harm other developers working with it.

With that in mind, replace boolean for enum props! The latter has a broader range, being more ready to keep up with your component's evolution and the several behaviors it may have. 

For example:

| xxxxxxxxx | Don't | Do | 
| --------- | ----- | -- |
| Prop name | `show` | `visibility` |  
| Values    | `true` or `false` | `visible` or `none` | 

Bet on enum props to develop a future-proofing component!

### Responsive values

One of the critical points of flexibility and scalability is to have a component ready to be displayed on every possible device. 

Instead of creating specific props to attend to devices' typical scenarios, leverage from the [VTEX Responsive Values app](https://github.com/vtex-apps/responsive-values) to enable your component's props to accept different values by device, such as desktop and mobile. 

#### Don't 

![best-practices-for-storefront-component-development-1](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/Media/best-practices-for-storefront-component-development-1.png?raw=true)

#### Do

![best-practices-for-storefront-component-development-2](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/Media/best-practices-for-storefront-component-development-2.png?raw=true)

>ℹ️ Combine enum props with responsive values, as shown below, and enhance your code quality with super optimized props!

![best-practices-for-storefront-component-development-3](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/Media/best-practices-for-storefront-component-development-3.png?raw=true)

### Slots

Slots enable you to render components through props instead of declaring an array of blocks in the Store Theme. Its simplicity removes the need for the `allowed` property in the [interface](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-interfaces) file and enlights your code, increasing the flexibility when developing a new storefront component.

You can learn more about Slots [here](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-slots).

#### Don't 

![best-practices-for-storefront-component-development-4](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/Media/best-practices-for-storefront-component-development-4.png?raw=true)

#### Do

![best-practices-for-storefront-component-development-5](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/development/Media/best-practices-for-storefront-component-development-5.png?raw=true)

> ℹ️ 
> 
> When not using Slots, prefer to use the `children` [composition](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-composition).

## Performance

In digital, the store's website performance plays an essential role in user-experience, directly impacting sales conversion rate and user session time, among other important metrics.

In addition to the practices listed below, do not forget to access our documentation on [optimizing performance](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-best-practices-for-optimizing-performance) to enable advanced configurations and boost your store's website performance.

### NPM libraries

Avoid using heavy npm libraries since they negatively impact the page's loading time and can therefore harm user experience on your store. 

Prefer light libraries to support your code and optimize its performance!  

> ℹ️ 
> 
> Check how your npm libraries can impact user browsing accessing [bundlephobia.com](https://bundlephobia.com/).

### Data sharing 

Use the React context to share data between components and avoid over-fetching at all costs.  

The Dispatcher and State patterns, as well as the useMemo feature, are powerful resources that can be made available by the context and used by your component. 

> ℹ️ 
> 
> Check out the article on [using React context effectively](https://kentcdodds.com/blog/how-to-use-react-context-effectively) to have an in-depth understanding of how the React context can work in your favor.

### Media upload

The usage of media in storefront components can be tricky if you are not critically thinking about performance. 

When [uploading the desired media assets to the VTEX File Server](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-the-assets-builder), clearly define height and width parameters to avoid data over-fetching and resizing on the client-side. This way, you can set up your component to request media assets according to the needed size per breaking point. 

### Rendering

Performance can be optimized during the component rendering as well. 

When declaring the block's [interface](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-interfaces), set the `Hydration` attribute and pass `on-view` as its value to only load and properly render your component once users find it on the interface.

The [Footer](https://developers.vtex.com/vtex-developer-docs/docs/vtex-store-footer) is a good example of a Store Framework's native component that counts on this attribute to be rendered optimizing store performance!

> ℹ️ 
> 
> The default value for `Hydration` is `always`, meaning that the component will be loaded and rendered as expected, regardless of the user's view.

## Accessibility 

Highly considering accessibility leads to the excellent opportunity to bring more users closer to the store's shopping experience.

Adopt the following practices to promote inclusion: 

- Enable user interactivity through the keyboard.
- Bet on color contrast when defining the component style. You can use the [ChromeLens extension](http://chromelens.xyz/) to help you with that. 
- Avoid HTML divs: they are the number one enemy of screen readers (and search engines). 

## Internationalization

Your component should be ready to be displayed worldwide if store globalization is a goal.

In terms of content internationalization, be cautious with string text translations. You can leverage from the Messages app, a native VTEX IO service for automatic translations, and perform manual translations of your own as well. 

Be aware that internationalization can mean more than string text translations! Take care of interpolation, pluralization, price and percentage formatting, among other discrepancies that may come into your way once borders are crossed.

Read the [Translating the component](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-8-translating-the-component) article and the [multi-language store documentations](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-multi-language-stores) to understand how you can make these adjustments in your component! 

## Styling

Style customization is one of the main steps when building a page template and developing storefront components.

When applying CSS to your project, always prefer to use Tachyons instead of CSS Modules. Whereas the Tachyons solution is more useful for different storefront scenarios, CSS Modules presents restrictions of use depending on the component behavior.

Understand both tools' particularities to make the best decision for your component style without wasting development efforts. 

Also, do not forget to make CSS Handles available for your component users if its distribution is a goal. Through Handles, future users will be able to style your storefront component as desired, according to their own specific needs. 

Check out the documentation on [Defining styles](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-5-defining-styles) to learn about Tachyons, CSS Modules and CSS Handles, as well as their use cases.

Another good styling tip is to be careful with the breakpoints on the screen according to devices. Remember to set the component style for every possible scenario on the interface!

> ℹ️ 
> 
> The [VTEX Styleguide](https://styleguide.vtex.com/) is a go-to document during your style customization. The guide is constantly updated by our team and provides useful guidelines in terms of design.

## Engagement

Finally, the best practice to be adopted by you is to keep up with the VTEX IO platform! Engage with us:

- Follow up the [Developer Portal's release notes feed](https://developers.vtex.com/vtex-developer-docs/changelog). 
- Subscribe to the [VTEX Developer Newsletter](https://forms.gle/DHo3SS7ZaGCvAMow8)
- Join the [Office Hours meeting](https://zoom.us/j/282720990?pwd=MkhFajhPS0xxZGppVjhNSm9MeUVJdz09) on Tuesdays, at 4 pm.
- Contribute with the [Store Framework's native components](https://github.com/vtex-apps/store-discussion)
