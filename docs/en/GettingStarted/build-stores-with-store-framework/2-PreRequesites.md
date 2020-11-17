# Prerequisites

Now that you have completed the VTEX IO basic setup, it is time to make sure that your VTEX account already has:

- Filled out the application form.
- Installed the correct Edition app.
- Implemented the VTEX Intelligent Search.

By meeting these three prerequisites, you guarantee that your store is apt to use the VTEX Store Framework free from any technical issue that could emerge due to flaws during the implementation steps.

Find below more info on each one of them and follow the instructions if necessary. 

## Filling out the Application form

As an open beta, Store Framework is included by default in VTEX contracts, being available to any VTEX store at no additional cost.

Making Store Framework publicly available to users enables faster development of the project and ensures that all business scenarios are impacted by the solution in the most scalable way possible.

Besides, making the resource available also entails access control, which promotes transparency in the development of the solution and gives our product team a good overview of the entire ecosystem.

Seeking to leverage our resources and keep everyone up-to-date with any changes, **the VTEX Store Framework team asks stores that are interested in the Store Framework solution to submit their VTEX account data through this [Store Framework Application form](https://docs.google.com/forms/d/e/1FAIpQLSclhQed9copSm44UuMBMXxosxndtWvWrYDrrZOaO62mKP8zlg/viewform)**.

>ℹ️ *Once you fill in the application form requesting access to use the VTEX Store Framework, our team will analyze your store's scenario and get in touch within three business days for support on your project.*

## Implementing the correct Edition app 

An [Edition app](https://vtex.io/docs/concepts/edition-app/) is a mandatory app that exports a bundle of settings and basic configurations to the VTEX account in which it is installed.

Every store with operations supported by VTEX must necessarily decide, at one point or another, between two available Edition apps.

The options are as follows:

-   `vtex.edition-business@0.x` - For stores whose front-end is built using VTEX [CMS](https://help.vtex.com/tutorial/what-is-cms--EmO8u2WBj2W4MUQCS8262);
-   `vtex.edition-store@3.x` - For stores whose front-end is built using the [VTEX Store Framework](https://vtex.io/docs/introduction/what-is-vtex-store-framework/).

In practice, this means that, by default, every VTEX store comes with the `vtex.edition-business@0.x` installed. Unless the account specifically requests to use VTEX Store Framework instead.

>⚠️ *Whether you are a new VTEX account or a former account using CMS, installing the `vtex.edition-store@3.x` Edition app is a prerequisite to successfully implementing the Store Framework solution.*

Therefore, get in touch with our [Customer Care team](https://support.vtex.com/hc/pt-br/signin?return_to=https%3A%2F%2Fsupport.vtex.com%2Fhc%2Fpt-br%2Frequests) to check the installed Edition and request the installation of the `vtex.edition-store@3.x` app in your VTEX account. 

## Implementing the VTEX Intelligent Search 

In order for your store to properly function with VTEX Store Framework, you first need to configure the [VTEX Intelligent Search](https://help.vtex.com/tracks/vtex-intelligent-search--19wrbB7nEQcmwzDPl1l4Cb) in your store. 

VTEX Intelligent Search is an intelligent search engine for e-commerce that aims to assist customers throughout their entire purchasing journey. 

The solution is an alternative to the platform's old native search engine and requires the installation of the following two apps on your VTEX account in order to work: 

- `admin-search` - Allows stores to configure every functionality made available by the search solution, including first-time catalog indexing. 
- `search-resolver` - Solves all search queries, being the main back-end app from the Intelligent Search.

>⚠️ *To proceed to the next steps and begin implementing the framework, both apps must be installed on your VTEX account. If not, you won't be able to perform any front-end changes to your website using the VTEX Store Framework.*

### Installing the Search apps

1. Log in to your VTEX account using your terminal:

```sh
vtex login {account}
```

>⚠️ *Do not forget to replace `account` for your VTEX account name.*

2. Once logged in, run the following command to list the apps already installed on your account:

```sh
vtex list
```

3. If any of the two apps is missing from the list, install it using the Toolbelt as follows:

```sh
vtex install vtex.admin-search vtex.search-resolver@1.x
```

>ℹ️ *Keep in mind that you should only install the apps missing from the list.*

Once both apps are installed on your account, along with the correct Edition App, you'll be ready to successfully implement VTEX Store Framework. Time to get busy! Let's go?

