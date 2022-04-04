---
title: Developing an app
description: "In this guide, you will learn how to develop an app using the VTEX IO platform. "
date: "2021-03-04"
tags: ["app-store", "app", "development"]
version: " "
git: " "
---

# Developing an app 

In this guide, you will learn how to develop an app using the VTEX IO platform. You will be presented with some core concepts of the platform and guided through the necessary steps to have a running application in VTEX IO.

[VTEX IO](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-what-is-vtex-io) is a cloud-native development platform that allows you to develop web storefronts, custom admin apps, and backend integrations for VTEX.


## Before you start
Make sure to install the [VTEX IO CLI (Command Line Interface) in your machine](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-install).

Any development in VTEX IO begins and ends with our CLI (Command Line Interface). VTEX IO's CLI allows you to perform any action necessary to your app development process, such as linking local files to the VTEX platform, managing workspaces, and releasing new app versions. 

## Step-by-step

### Step 1 - Creating an app 

When developing an app in VTEX IO, you can start one from scratch or use one of our boilerplates. Our boilerplates contain implementation examples and all the initial settings needed for you to start developing an app. Take a look at the available boilerplates:

| Boilerplate name | Description |
| ---------------------- | ---------------- |
| `graphql-example` | Implements a [VTEX IO service with GraphQL resolvers](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-service-configuration-apps#if-you-are-developing-a-graphql-app). |
| `payment-provider-example` | Implements a [Payment-Provider protocol](https://developers.vtex.com/vtex-rest-api/docs/payments-integration-payment-provider-protocol) |
| `admin-example` | Implements an admin app that adds a menu button to the admin sidebar and navigation via parameter example. |
| `store` | Implements the basic structure of a VTEX Store Framework storefront. |
| `service-example` | Implements a [VTEX IO service](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-service-configuration-apps) with HTTP route handlers. |
| `render-guide` | Guide repository for an app with all common patterns in app development, such as pagination and editing entities. |
| `edition app` | Creates an an [Edition app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app). |
| `react-guide` | Creates a frontend app with React. See… [react app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-1-developing-storefront-apps-using-react-and-vtex-io). |
| `checkout-ui-settings` | Guide repository for the Checkout UI Settings app, responsible for A/B testing in your store's scripts, in addition to the possibility of quick rollbacks for old scripts, i.e., scripts of older Checkout UI Settings app's versions. |
| `service-worker-example` | Guide repository for apps that enable service-worker builder to expose Service Worker. |
| `admin-ui-example` | Guide repository for Admin apps for the admin v4 with the admin-ui design system. |

#### Cloning the boilerplate repository to your local files

1. Open the terminal and clone the boilerplate you desire by running the following command:

```
vtex init
```

2. Select the boilerplate that you want. 

![boilerplates](https://user-images.githubusercontent.com/67270558/156827878-b43f13b6-3ba0-48d8-b425-ed7790e3ba5f.png)

3. A new folder will be created in your machine, and to access it run `cd {folder-name}` in your terminal.

> ℹ️
> 
> Change the name in the curly brackets to the boilerplate that you choose, for example `cd graphql-example`


#### Editing the manifest.json file
Once you have [cloned the boilerplate repository](#cloning-the-boilerplate-repository-to-your-local-files) into your local files, let's learn how to make it your own by editing the **`manifest.json`** file.

> ℹ️
> 
> The `manifest.json` file saves essential information about a VTEX IO app, such as its name, version, vendor, description, dependencies, etc. It is the core communication of your app with the VTEX IO platform.  For more information, see the [Manifest article](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-manifest).

1. Open the boilerplate project you started in [the previous step](#cloning-the-boilerplate-repository-to-your-local-files) in any code editor of your choice.

2. Open the `manifest.json` file and look at the primary information that it provides, such as in the [Manifest article](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-manifest).

3. Change the following fields according to your scenario:

- Replace the value of the `name` field with the name of your app. 

- Replace the value of the `vendor` field with the VTEX account you are using for development. This should be the name of the VTEX account resposible for the app development, maintenance, and distribution.

- Replace the value of the `version` field with the app version, according to the [Semantic Versioning 2.0.0](https://semver.org/).

- Replace the value of the `title` field with the app distribution name. This name will be displayed on the Apps section in the admin and on the VTEX App Store.

- Replace the value of the `description` field with a brief description of the app's functionality.



4. Go to the **`builders`** prop and add the ones that make sense for your app project.


> ℹ️ Info
>
> A Builder defines the nature of an app. If you are developing a frontend app, you'll probably want to use the `react` builder. Instead, if you're developing a backend integration, you'll probably want to use the `node` or `dotnet` builder. In summary, a builder is responsible for processing, validating, and forwarding a given block of code to a runtime or a framework capable of executing it. Notice that an app can have as many builders as you want. That allows bundling front and backend development and delivering your solution with just one package. Please refer to the [Builders article](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders) for more information.

5. Install the [dependencies](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-dependencies) and [peer dependencies](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-peerdependencies) necessary for your app to properly work by relying on VTEX IO apps and other apps, respectively.

6. Save your changes.

So far, you have created an app and made it your own. Now, it is time to start making changes to your code and use a development server to see your changes live.

### Step 2 - Starting the app development
In this step, you will create a  a development workspace to perform the necessary changes in your app without worrying about the app's live version and see your changes in real-time by sending the app’s changes to our cloud platform.

#### Logging in to your VTEX account

This step will guarantee that your VTEX account is in sync with the VTEX IO development platform and allow you to manage the development and publishing of the app.

1. Once installed the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-install), log in to your VTEX account with the following command:

```
$ vtex login {accountName}
```

> ⚠️
>
> ️ Replace `{accountName}` with the name of your VTEX account.

2. A browser window will open and ask for your credentials.

3. Once logged in, run the `vtex whoami` command to show which account and workspace the VTEX IO CLI is using.


![Login - Whoami](https://user-images.githubusercontent.com/67270558/151855497-21a966cf-9529-42df-8e25-27245f8e26f2.png)

#### Creating a development workspace
When using VTEX IO, any development must happen in a [workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace). 

> ℹ️ Info
>
> **Workspaces** are environments isolated from one another. They can be understood as different versions of the same VTEX account. In practice, changes performed in a particular workspace do not affect your app’s live version or other developers' work. 
Refer to the [Workspace article](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace) for more information.

To start developing, you have to create a [Development workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-development-workspace) in your VTEX account. When you log in, you automatically use the Master workspace, which means you are in the version available to the end-user.

1. Run the `vtex use` command in your terminal as shown below:

```
$ vtex use {exampleName}
```
This changes your VTEX account to a Developer workspace called `exampleName` ( ️ replace it with the name of your choice), creating it from scratch if it does not already exist.


![vtex-use](https://raw.githubusercontent.com/vtex-apps/io-documentation/master/docs/en/GettingStarted/develop-storefront-apps-using-react-and-vtex-io/assets/basic-development-setup-in-vtex-io-2.png)

2. Type `Y`, and a Development workspace will be created under your chosen name.

So far, you have created an app and have a Development workspace to perform any changes in your code. In the following section, you will learn how to sync the changes performed in your app to our cloud development environment by linking the app.

#### Starting a development server
Now that you have your app up and running on your machine, it is time to send all the changes you have performed locally so far to the cloud and reflect them in the workspace in which you are working. In other words, you will be able to see your changes in real-time by accessing the account you are logged in using the workspace you are using to develop.

1. Run `vtex whoami` in your terminal and make sure you are logged into the desired account using the development workspace you have created.

2. In the terminal, access the app's directory in your local files.

3. Once in the accurate directory, type the following command in the terminal:
```
vtex link
```

After that, every change can be seen in your browser in real-time, and you can access it by running `vtex browse` in your terminal.



## Next Steps
Now that you have created your app and it is already live in your development workspace, here are some options of what you can do next:

- [Manage application logs](https://developers.vtex.com/vtex-developer-docs/docs/managing-application-logs): keep track of errors, warnings, and informative events with VTEX IO logging service.

- [Run A/B tests](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing): Optimize your store's conversion rates by running A/B tests.

- [Release a new app version](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-releasing-a-new-app-version): Release a new app version If you’re sure about all the code changes that you’ve done to your app in a development workspace.

- [Create a Production workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-creating-a-production-workspace): Create a Production workspace to test in a user traffic environment the changes you performed in a development workspace Once you are sure of your changes performed in the Development workspace with traffic.

- [Promote a workspace to Master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master): Promoting a workspace to Master marks the final step to make an app publicly available to end-users.

### Developing for the VTEX App Store

If you are developing an app that will be distributed to the [VTEX App Store](https://apps.vtex.com/) make sure to check the following guidelines:

- [Engineering Guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-engineering-guidelines) - The Engineering guidelines are your go-to guides to learn the coding standards to develop an app using the VTEX IO infrastructure, such as scalability, performance, security and data privacy.

- [User experience guidelines](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-design-guidelines) -  Learn how you can design an app to meet the VTEX App Store requirements.


- Business Guidelines -  The Business Guidelines are divided in two: 
    - [App monetization](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-app-monetization): Learn the types of business models for your app.

    - [Marketing assets](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-business-guidelines-marketing-assets): Learn how to prepare the assets to market the app in the VTEX App Store.

## Related Articles

### Concepts

- [Manifest](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-manifest#vendor)

- [Builders](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders)

- [Dependencies](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-dependencies)

- [Workspace](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-workspace/)

### Tutorials

- [Developing Storefront apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-1-developing-storefront-apps-using-react-and-vtex-io)

- [Developing Pixel Apps](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-1-developnativeintegrationswithpixelapps)

### Guides

- [Installing the VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-install)

- [Linking an app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app)

- [Service](https://developers.vtex.com/vtex-developer-docs/docs/back-end-development-guides)

- [Developing services on VTEX IO](https://learn.vtex.com/docs/course-service-course-lang-en)



