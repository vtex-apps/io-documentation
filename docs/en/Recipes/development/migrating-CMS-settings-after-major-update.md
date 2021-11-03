# Migrating CMS settings after a theme major update

You may need to do a major update of your store theme app due to changes in its peer dependencies, for example. In this situation, however, changing to a new store theme major could lead to undesired consequences, such as losing the admin's page template settings.

To handle this situation, follow the steps below to migrate template settings.

## Step by step

1.  Using the terminal and [VTEX IO's CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference), log in to the desired account.
2. Switch to the production workspace containing the desired changes and [publish](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-making-your-new-app-version-publicly-available#step-2---publishing-the-new-app-version) a new major version of your store theme app.
3. Run `vtex use {workspaceName} --production` to **create and use a new** production workspace.

>⚠️ Replace the values between the curly braces according to your scenario.

4. Run `vtex install {appvendor}.{appname}@{appversion}` to install the store theme app published in Step 1.
4. Run `vtex install vtex.admin-graphql-ide@3.x` to install the GraphQL admin IDE.
5. In your browser, access your account's admin, using the workspace created in Step 3, and select the GraphQL admin IDE in the side-bar menu.
6. From the dropdown list, choose the `vtex.pages-graphql@2.x` app.
7. Copy the mutation command presented below to the text box that is displayed and update the `from` and `to` values according to your scenario.

```
mutation{
  updateThemeIds(from:"{appvendor}.{appname}@{oldmajor}.x", to:"{appvendor}.{appname}@{newmajor}.x")
}
```

8. Open the workspace and validate content, routes, pages, and redirects.
9. If everything goes as expected, [promote your workspace to master](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-promoting-a-workspace-to-master/).
