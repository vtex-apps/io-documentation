# Migrating CMS settings after a theme major update

You may need to do a major update of your app store theme due to changes in its peer dependencies, for example. In this situation, however, changing to a new app store theme major could lead to undesired consequences, such as losing the page template settings in the admin.

To handle this situation, you have the option of migrating template settings by following the step-by-step presented in the sequence.

## Step by step

1. Using your terminal and the VTEX IO [Toolbelt](https://vtex.io/docs/recipes/development/vtex-io-cli-installation-and-command-reference/), [publish](https://vtex.io/docs/recipes/development/making-your-new-app-version-publicly-available/#step-2-publishing-the-new-app-version) the new major version of your app store theme.
2. Log into the account which the theme is installed.
3. Run `vtex use {workspaceName} --production` to **create and use a new** production workspace.

⚠️ *Remember to replace the values between the curly braces according to your scenario.*

4. Run `vtex install {appvendor}.{appname}@{appversion}` to install the `store-theme` published in step 1.
4. Run `vtex install vtex.admin-graphql-ide@3.x` to install the GraphQL admin IDE.
5. In your browser, access your account's admin and select the GraphQL admin IDE in the side-bar menu.
6. From the dropdown list, choose the `vtex.pages-graphql@2.x` app.
7.  Copy the mutation command presented in the following to the text box that is displayed and update the `from` and `to` values according to your scenario.

```
mutation{
  updateThemeIds(from:"{appvendor}.myvtex@{oldmajor}.x", to:"{appvendor}.myvtex@{newmajor}.x")
}
```
8. Open the workspace and validate content, routes, pages, and redirects.
9. If everything goes as expected, [promote your workspace to master](https://vtex.io/docs/recipes/development/promoting-a-workspace-to-master/).
