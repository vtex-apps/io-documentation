# 2. Creating the new app

To start developing your app optimally, you need to:

- Copy our [React app boilerplate](https://github.com/vtex-apps/react-app-template) to your local files.
- Make the first and main changes to the `manifest.json` file in the React example app. 

This step is important to eliminate the concerns about the default settings in the VTEX IO platform. Once copied, the repository will automatically import the basic settings that you will need to start developing your app.  

## Cloning the boilerplate repository to your local files

Clone the boilerplate repository to your local files by running the following command: 

```sh
git clone https://github.com/vtex-apps/react-app-template
```

Then, open the imported React app's repository using the code editor of your choice.

## Editing the `manifest.json` file

Having the app's code open in your code editor, let us analyze the `manifest.json` file, which saves **basic and essential information** about the app, such as:

- `vendor` - Name of the VTEX account that develops, maintains, and distributes the app. 
- `name` - App name. You choose the name, but be careful to avoid special characters (with the exception `-` hyphens). 
- `version` - App's current version. For versioning, VTEX IO uses [Semantic Versioning 2.0.0](https://semver.org/). 
- `title` - App's distribution name. This name will be displayed on the `Apps` section in the admin and, also, on the VTEX App Store.
- `description` - Brief description of the app's functionality. 
- `builders` - List of [Builders](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders/) that facilitate the app's development, abstracting service configurations. 
- `dependencies` - List of apps that the app you are developing depends on for proper functioning. 

At the beginning of the process, it is very important to incorporate the new app's basic information in the `manifest.json` file in order to make it your own instead of it staying another example version provided by VTEX. To do that:

1. Replace the account in the `vendor` field with the VTEX account you are using for development.
2. Replace the value in the `name` field with the name you want. Remember that the name defined in this field will be the name of your new app.
3. Replace the values in the `title` and `description` fields with something that matches the app you are developing.
4. Add the `store@0.x` builder to the builder list to allow the creation of new blocks:

```diff
"builders": {
+  "store": "0.x"
}
```

5. If you want to import any React components previously developed for your new app, update the `dependencies` list with the name of the app that runs the desired component, for example:

```diff
"dependencies": {
+  "vtex.styleguide": "9.x"
}
```

This will allow you to later import the app component added in `dependencies` into your code via the `import {componentName} from 'vtex.styleguide'` structure, for example.
