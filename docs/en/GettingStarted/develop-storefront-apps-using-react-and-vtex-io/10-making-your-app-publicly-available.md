# 9. Making your app publicly available

Once you have completed all the previous steps and are comfortable with the setup, it is time to learn how to make your app publicly available, **allowing other users to use your app too**. 

Before continuing with the app development flow, it is important first to define how you will be distributing your app–who will be able to install your app? Will you charge for using it? If so, what will be the cost for interested accounts?

The answers to these questions vary depending on the distribution type chosen for the app. The VTEX IO platform supports the following app types:

- **Private** - Can only be installed by the `vendor` account, the account that develops and maintains it. 
- **Public** - It is available for all accounts in the VTEX platform ecosystem; a fee may be charged for its use or not.

## Defining distribution

The choice between private or public has to be made before the app is launched. 

The reason is that depending on the chosen type, some settings have to be configured in the app's `manifest.json` file before it is distributed. After all, the settings in the `manifest` define who will be able to use the component and whether it will be free or not. 

To learn how to configure your app's `manifest.json` file properly, access the documentation about [Billing Options](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-billing-options/) and follow the instructions that fit the desired scenario for your project. 

After following those detailed steps, your app will be ready to be correctly distributed! 

Remember that [*linking*](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) the app you are working on will not be enough: you will also need to launch, publish, and install it in a production workspace for testing and, finally, validate it for *deploy*, as we will see below.

## Launching a new version

If you are sure about all the changes made in the development workspace, it is time to launch a new version of your app. 

Using your terminal, access the app folder and run the following command:

```sh
vtex release major
```

This will:

- Update the versioning in the `CHANGELOG.md` and `manifest.json` files following [expected semantics](https://semver.org/).
- Create a *launch* commit.
- Create a GitHub repository for the app.

If you want to release a **Beta** version, run the command `vtex release major beta` on your terminal. It will execute the same actions as the previous command, except that you will be launching a *beta* version for your app instead of a *stable* version. 

>⚠️ Do not forget to log in to the desired VTEX account before launching the new version so that the app's `vendor` is the account where you have been working. 


## Publishing on the VTEX IO platform

Once the app has been launched, it has to be properly installed to have the settings you tested. However, it is not possible to simply install an existing app on your local desktop.

>ℹ️ Note that when launching your app in step 2 above, you did not link it to the VTEX IO platform. The previous command only automated actions for proper versioning.


That means now you have to publish the app on the platform! Using your terminal, access the app folder and run the following command:

```sh
vtex publish
``` 

The command will transform your app into a ***release candidate version***, making it available to be installed for testing with VTEX IO CLI.

>⚠️ You have to always be logged in to the desired VTEX account for publishing the app. Make sure the app's `vendor` is the same as the account you are working on.


If your app does not have the `billingOptions` field configured, users with access to the VTEX account that published it will also be able to install the app through the Admin via the **Apps** section.

## Installing in a production workspace

Having your app ready to be installed, you need to create a production workspace to test the settings and possible behaviors. 

Using your terminal, run the following command (replacing the curly brackets with the desired name for your new workspace):

```sh
vtex use {WorkspaceName} --production
```

>⚠️ From this point forward, further changes are not recommended. This is because a production workspace is able to receive user traffic and can be accessed by people other than you. If you want to make any changes to the code, you have to work on the new settings in a development workspace and then follow the steps in this article again.


To install the app in the new workspace, run the command below, replacing the curly brackets with your scenario's real values:

```sh
vtex install {appVendor}.{apNname}@{appVersion}
```

## Validating the deploy 

It is time to validate your *release candidate version*!

We recommend that you first run a [native A/B test](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-running-native-ab-testing) between the new production workspace and your store's Master workspace to test the stability of the app. 

>⚠️ If you are working with a beta version and all your settings have already been properly tested, we recommend that you return to the second step of this article to launch the app's non-beta version and then follow the walkthrough again.


Once you are satisfied with the results, access the app's folder on your terminal and run the following command to publish your *release candidate version* as a *stable* version:

```sh
vtex deploy
```

Running the command will cause the new *stable* version of the app to be automatically installed on all accounts that had previously installed the *release candidate* version.

## Extra steps

### Promoting your workspace to Master

Promoting the production workspace where the app was installed to Master is essential to be able to render it to your store's end users, the ones who will actually interact with the developed component. 

That means if you want to use the app that was developed in the store you are working on, you need to complete one more step in your development process.

Using your terminal, log in to your VTEX account and make sure you are using the production workspace used in the previous steps. Then, run the command below:

```sh
vtex workspace promote
```

 The status of a Master workspace is `production true`. Upon receiving this response from your terminal, your app will already be available to your store's users.

### Submitting your app to the VTEX App Store

Whether you incorporate the new component into your VTEX store theme or not, you may still want to add the app you developed to the VTEX App Store app catalog. 

The [VTEX App Store](https://extensions.vtex.com/) is a *marketplace* for *plug&play* solutions and can be used by any interested VTEX account that wants to make available its solutions to other accounts in the ecosystem. 

To make your app available, check the documentation for [Submitting an app in the VTEX App Store](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-submitting-your-app-in-the-vtex-app-store/ ).

---

**All set!** After completing these steps, the app will be launched, published, tested, validated, and, finally, made public for all its users. 

During this article series, you learned all the necessary steps to develop a front-end app from scratch using React, GraphQL, CSS, and the VTEX IO development platform. 

To understand more about the platform's development possibilities, do not forget to access the rest of our [documentation](https://developers.vtex.com/vtex-developer-docs/docs)!
