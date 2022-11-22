# Migrating CMS settings after a theme major update

You may need to do a major update of your store theme app due to changes in its peer dependencies, for example. In this situation, however, changing to a new store theme major could lead to undesired consequences, such as losing the admin's page template settings.

To handle this situation, follow the steps below to migrate template settings.

## Before you start

1. Install the [VTEX IO CLI.](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-install)
2. Install the GraphQL IDE by running the following command: `vtex install vtex.admin-graphql-ide@3.x`.

## Step by step

1. Open the terminal and log in to your account.
2. Change to the **production workspace** containing your latest changes and [publish](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available#step-2---publishing-the-new-app-version) a new major version of your store theme app.
3. Create a new production workspace by running the following command:
  - _Replace the values between curly braces according to your scenario._
  ```
  vtex use {workspaceName} --production
  ```
4. Install the store theme app published in the previous steps:
   ```
   vtex install {appVendor}.{appName}@{appVersion}
   ```
5. Open the VTEX Admin using the workspace created in Step 3 and go to the **GraphQL Admin IDE**:
  ```
  vtex browse admin/graphql-ide
  ```
6. From the **Choose an app** dropdown list, select `vtex.pages-graphql@2.x`.
7. Copy the code below and paste it into the GraphQL IDE. 
  ```
  mutation{
    updateThemeIds(from:"{appvendor}.{appname}@{oldmajor}.x", to:"{appvendor}.{appname}@{newmajor}.x")
  }
  ```
8. Replace the values between curly braces according to your scenario and press the play button.
9. Open the VTEX Admin using the workspace created in the previous steps and validate the CMS's content, routes, pages, and redirects.
10. Once you validate your data, [promote your workspace to master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master/).
