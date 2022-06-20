# Deploying the app's stable version

This guide will teach you how to deploy the latest stable version of your app so that all accounts having your app installed can be automatically updated with the new stable version.

## Before you start

Before proceeding any further, make sure the app you are about to deploy has already been [published](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-publishing-an-app) and tested. Note that deploying an app is one of the steps to **making your new app version publicly available**. Please refer to [this](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available) guide for more information.

Also, keep in mind that after publishing your app, you must wait 7 minutes before deploying it. Otherwise, you'll receive the following error: **Invalid state transition**. If you are deploying a **hotfix**, you can use the **`--force`** flag to instantly deploy your new app version. This flag is available only for VTEX IO CLI versions higher than `2.118.0`.

## Step by step

If you have already published and validated your app, take the steps below to deploy your app's candidate version as a **stable version**. 

1. Open the terminal and log in to the account responsible for the app development, i.e., **the account specified as the app's vendor in the [`manifest.json`](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-manifest) file.**
2. Deploy your new app version:
  - _Replace the values between the curly brackets according to your scenario._

  ```sh
  vtex deploy {appvendor}.{appname}@{appversion}
  ```

## Next steps

- [Promoting your changes to master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master)
