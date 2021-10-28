# 7. Making your Pixel app publicly available

Up until now, your Pixel app is being developed in your local files, meaning it is only connected to the VTEX IO platform through your development workspace.

Once you are happy with the implemented configurations, you are ready to make you Pixel app publicly available i.e. **make it possible for your app to be installed by other users** besides you!

The first thing to be defined is your app distribution: who will be able to install it? Will you charge your app users? If positive, how much?

The answers for these questions directly depend on the chosen distribution type. In the VTEX IO platform, an app can be: 

- **Private** - It can only be installed by the `vendor` account i.e. the VTEX account responsible for the app development and management. 
- **Public** - It is available to all account ecosystem using VTEX platform. 

## Step 1 - Defining your app distribution

The decision between private or public must be made even before the application is released. 

Depending on what is chosen, some settings must be made in the `manifest.json` file of the app before its distribution takes place in order to define who can use the app, as well as whether its use will be free or not.

Access the documentation on [Billing Options](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-billing-options/) and follow the instructions to perform the needed settings according to the desired scenario for your app distribution. 

>ℹ️ Remember that [linking](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) the app you are working on will not suffice: you will also need to release it, publish it, have it installed in a production workspace for testing and, finally, validate it for *deploy* - as we shall see below.

## Step 2 - Releasing a new version

If you're sure of all the changes performed in your development workspace, it's time to launch a new version of your app.

Using your terminal, access the app directory and run the following command:

```sh
$ vtex release major
```

It will be responsible for:

- Updating the new version in the app's `CHANGELOG.md` and` manifest.json` files according to the [proper semantics](https://semver.org/).
- Creating a launch *commit*.
- Creating a new repository on GitHub for your application.

If you want to release a **Beta** version of your app, run the command `vtex release major beta` on your terminal instead. It will perform the same actions as the previous command, with the difference that you will be releasing a *beta* version of your application instead of *stable*.

>⚠️ Don't forget to log in to the desired VTEX account before releasing the new version - the app's `vendor` should be the VTEX account you are working on!

## Step 3 - Publishing the app in the VTEX IO platform 

Once the application has been released, it must be properly installed in other workspace in order to have your settings tested. 

It is not possible, however, to install an app that only exists in your local environment: it will be necessary to *publish* your new Pixel app in the VTEX IO platform!

>ℹ️ Notice that, until this step, the app was not published in the platform. The `vtex release major` command only automated actions for the app versioning.

Using your terminal, access the app directory and run the following command:

```sh
$ vtex publish
``` 

The command will make your app a ***release candidate version***, thereby enabling it to be installed via VTEX IO CLI for testing purposes.

>ℹ️ You must always be logged into the desired VTEX account for publishing the app. Make sure the app's `vendor` is the same as the account you're working on.

>⚠️ If your app does not have the `billingOptions` field configured, users with access to the VTEX account responsible for the publication will also be able to install the app through the Admin, in the **Apps** section.

## Step 4 - Installing it in a production workspace

Once your app is ready to be installed, you must create a production workspace to test its settings and possible behaviors.

Using your terminal, run the following command (replacing `workspaceName` with the desired name for your new workspace):

```sh
$ vtex use workspaceName --production
```

>⚠️ From this moment on, changes in your app code are no longer recommended, since production workspaces are able to receive traffic from users i.e. it can be accessed by other people other than you. If you want to make any changes in the code, work on the new settings from a development workspace and then follow the steps detailed in this documentation again.

To install the app in the new workspace, run the command below replacing the default values with real ones from your scenario:

```sh
$ vtex install appVendor.appName@appVersion
```

## Step 5 - Validating your app deploy 

It is finally time to validate your release candidate version!

We strongly recommend you to firstly run a [native A/B test](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing) between the new production workspace and your store's Master workspace in order to check your app stability.

>⚠️ If you are working with a beta version and all its settings have already been properly tested, return to the second step of this article to release the stable version of your app.

If your happy with your results, access the app directory using your terminal and run the following command to deploy your *release candidate* version as a *stable* version:

```sh
$ vtex deploy
```

>ℹ️ Running the command above will automatically install the new *stable* version of your app in all accounts that had previously installed the release candidate version.

## Extra steps

### Promoting your production workspace to Master

Promoting the production workspace in which the application was installed to Master is an essential step to use your new Pixel app in a real scenario i.e. your store website.

Using your terminal, log in to your VTEX account and make sure you are using the production workspace used in the previous steps. Then, run the following command:

```sh
$ vtex workspace promote
```

>ℹ️ The status of a Master workspace is `production true`. Once you receive this response from your terminal, your new Pixel app is already available in your store website.

### Submitting your app to the VTEX App Store

It is also possible to add your brand new Pixel app in the catalog of the **VTEX App Store**.

The [VTEX App Store](https://extensions.vtex.com/) is a marketplace for plug&play solutions, and it can be used by any VTEX account interested in making its solutions available to other VTEX accounts as well.

To make your new Pixel app part of our App Store, check out the documentation [Submitting an app in the VTEX App Store] (https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-submitting-your-app-in-the-vtex-app-store/).

---

**Done!** At the end of these steps, your Pixel app will have been released, published, tested, validated to be deployed and finally made available in your store website.

Throughout this track, you have learned all the necessary steps to develop from scratch a native integration between your VTEX store and third party solutions using the VTEX IO platform.

To understand more about the platform's development possibilities, don't forget to access the rest of our [**documentation**](https://developers.vtex.com/vtex-developer-docs/docs)!

