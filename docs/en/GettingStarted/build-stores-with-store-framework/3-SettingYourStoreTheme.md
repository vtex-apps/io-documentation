# Setting your store's theme

The **Store Theme** is a default theme applicable to all VTEX IO stores. The theme performs two tasks:

- **Declares templates**, configuring and mixing components.

- **Declares styles**, configuring primary and secondary colors, typography scales and spacing, etc.

This means that the Store Theme is a default theme responsible for defining the basic look of your store's front.

VTEX IO Toolbelt offers the `vtex init` command which can quickly copy Store Theme to your computer where it may be configured and customized according to your business needs.

## Implementing your Store Theme
  
<div class="alert alert-warning">
Before downloading the Store There in your local files, <b>make sure your VTEX account has installed the Store Edition app</b>, otherwise you won't be able to work with VTEX IO. For more details on Edition apps and their importance, check out the <a href="https://vtex.io/docs/concepts/edition-app/">documentation</a>.
</div>

Using your terminal, navigate to an already existing local files directory where you want Store Theme to be copied to. Then, use the `vtex init` command, select the `store-theme` option and confirm that you want to download the theme folder to the destination you just chose.

```sh
$ cd {examplefolder}
```

Notice that `{examplefolder}` should be replaced with the folder name where the Store Theme is going to be copied to.

```sh
$ vtex init
```

You'll receive important information about Store Theme, such as vendor, name, title and description. With the exception of **vendor**, press enter to keep each field's predefined values.

<div class="alert alert-info">
Replace the predefined vendor value with the account name of the store that you are developing, so that you'll be able to correctly publish its theme later on. 
</div>

![toolbelt-store-theme-selection](https://user-images.githubusercontent.com/52087100/61887063-3d3b2a00-aed7-11e9-92b8-653c4972a218.png)

## Linking your local code to VTEX IO

Now that Store Theme has been copied to your local folder, you have to run `cd store-theme` in your terminal. Afterwards, run `vtex link` to have the theme compiled and published in the account and workspace that you've just created.

<div class="alert alert-warning">
Run <code>vtex whoami</code> to be sure that you're in the right account and in a development workspace. Otherwise, Toolbelt will not accept the link directly with the master workspace.
</div>

```sh
$ cd store-theme
```

```sh
 $ vtex link
```

![VTEX link example](https://user-images.githubusercontent.com/52087100/61887229-9dca6700-aed7-11e9-9934-030a153b75b6.png)

When linking Store Theme, your computer's local files are synced with the VTEX IO platform. This means that any change done locally to the code will be sent to and reflected in your workspace.

## Understanding Store Theme's structure

To better understand the default theme's structure, let's have a closer look at the files that were created in your local files. You can browse through your code with whatever editor you prefer.

![Repository tree](https://user-images.githubusercontent.com/52087100/61887339-ce120580-aed7-11e9-8c7b-eb55d12def2b.png)

- **manifest.json**: main file of any app. It saves important metadata, such as _vendor_, name, version, app dependencies and builders.

- **store**: folder responsible for defining a store's structure. It's where you configure each page's components and its properties. 

- **styles**: folder responsible for setting a store's visual theme, by customizing the components on each page.

## Visiting your new store

Navigate again to your new store by accessing:

`https://{workspace}--{account}.myvtex.com`

After the login, you should already see Store Theme reflected in your store:

![Store Theme](https://user-images.githubusercontent.com/52087100/61896668-d4aa7800-aeeb-11e9-906b-9d6b04fd03c0.png)

Now that your store is online and has a default theme, we can build its identity by configuring its templates and customizing its styles.
