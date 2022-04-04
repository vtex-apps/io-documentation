---
title: User experience guidelines
description: "User experience guidelines enforced by the VTEX App Store to guarantee a baseline standard of quality, viability and usability for all apps available for VTEX stores."
date: "2021-07-21"
tags: ["app-store", "app", "development", "design guidelines", "UX", "User experience"]
version: " "
git: " "
---

# User Experience guidelines

Before you begin [developing your App](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-an-app), you must first decide on the UX flows and interfaces that will make it accessible and intuitive to use.

Refer to the best practices listed below when designing your app.

## Visual consistency
The apps available through the [VTEX App Store](https://apps.vtex.com) must be consistent with:
- **[VTEX brand manual](https://brand.vtex.com/?_ga=2.86158557.436370270.1649074565-1001456323.1619912759):** The VTEX set of rules or visual guidelines to be followed.

- **[VTEX brand colors](https://brand.vtex.com/identity/color):** The VTEX color brand palette to uniform an app with VTEX standards.

- **[VTEX Styleguide for Admin apps](https://styleguide.vtex.com/#/Introduction):** a Design System with a set of reusable patterns, components, and materials for VTEX app development.

Take a look at the following example of an Admin app using some of the VTEX Styleguide components.

![admin-page-example](https://user-images.githubusercontent.com/67270558/158217591-cba1ddec-2de5-4eda-aa4a-c45fee38db0f.png)

Check out some of our most-used components listed on [VTEX Styleguide](https://styleguide.vtex.com/#/Introduction):


| Component Name | Usage | 
| -------- | -------- | 
| Layout     | Displays an empty standard Admin page. Refer to the [Layout guidelines](https://styleguide.vtex.com/#/Components/Admin%20structure/Layout) for more details.    | 
| PageBlock   | Displays an empty container. Refer to the [PageBlock guidelines](https://styleguide.vtex.com/#/Components/Admin%20structure/PageBlock) for more details.| 
| PageHeader   | Displays a standard header used in Admin pages. Refer to the [PageHeader guidelines](https://styleguide.vtex.com/#/Components/Admin%20structure/PageHeader) for more details.| 
| Styles     |  The Styles configure your app's layout's colors, spacing, and typography. Refer to the [Styles guidelines](https://styleguide.vtex.com/#/Styles) for more details.| 
| Tabs     |  Displays a navigation tab that allows alternating between content in the same level of hierarchy Refer to the [Tabs guidelines](https://styleguide.vtex.com/#/Components/Navigation/Tabs) for more details.    | 
| Button     | Displays a button that trigger actions and/or redirects users to another page. Refer to the [Button guidelines](https://styleguide.vtex.com/#/Components/Forms/Button) for more details.| 
| Alerts    | Displays short notifications to users about an issue or a new feature. Refer to the [Alert guidelines](https://styleguide.vtex.com/#/Components/Notification/Alert) for more details.| 
| Table     | Displays structured data and offers controls to navigate, search, and filter through it. Refer to the [Table guidelines](https://styleguide.vtex.com/#/Components/Display/Table) for more details.| 
| Modal    | Displays a dialog window on top of a page content. Once a Modal opens, the user can not interact with the content behind it. Refer to the [Modal guidelines](https://styleguide.vtex.com/#/Components/Overlays/Modal) for more details. | 


## Identify potential
Besides adhering to interface consistency standards, you must design your app experience to be fluid, simple, and accessible. Hence, before submitting your app to the homologation process, we recommend that you:

- Run usability tests with users.
- Identify potential friction points and implement solutions to any issues that may arise.


> ℹ️
>
> **The homologation process** is when our team review and test your app before making it public on the VTEX App Store. Apps that are difficult to configure, have confusing guidelines, or break the user journey critically will not be approved in our homologation process.

### User journey
User journeys in the application should be linear and complete, indicating a path with a beginning, middle, and end. They should:

- Allow merchants to go back to previous steps when setting up and using your app.
- Provide clear directions on how to proceed from a certain point. 

### System status and feedback
To guarantee that your users understand and effectively finish their journeys in your app, you must provide status and feedback on their actions:

- Make it clear when a configuration is incorrect, completed, or pending authorization. For example, you can use [Alerts](https://styleguide.vtex.com/#/Components/Notification/Alert) or a [TextArea](https://styleguide.vtex.com/#/Components/Forms/Textarea) to display a message.

- Use short and actionable notifications to eliminate any friction in the app configuration. For example, you can use [Modals](https://styleguide.vtex.com/#/Components/Overlays/Modal).

Even if your UI is consistent and provides clear feedback messages, users may still experience difficulties installing and using your app, especially during their first contact. Hence, to avoid mistakes and errors:

- Include mechanisms that offer confirmation messages when the user attempts to conduct undesired operations such as registry removal, app uninstallation, or resumption of extensive configurations.


### UX writing principles
It is important that you communicate with our users the same way VTEX communicate with them.

The writing of your app's instructions, actions, feedback, and settings must follow our [UX Writing guidelines](https://uxwriting.vtex.com/).

## Related Articles

- [App Store Guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-homologation-requirements-for-vtex-app-store)
- [VTEX Styleguide](https://styleguide.vtex.com/#/Introduction)
- [VTEX brand manual](https://brand.vtex.com/?_ga=2.86158557.436370270.1649074565-1001456323.1619912759)
- [UX Writing guidelines](https://uxwriting.vtex.com/)
