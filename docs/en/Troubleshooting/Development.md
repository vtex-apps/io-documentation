# Development

## I don't see my changes

>ℹ️ Once you [link your app](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app), you should see all your changes live at `https://{workspace}-{account}.myvtex.com`. If your theme changes are not reflecting on your store workspace, check the following workarounds to fix your scenario.

<details>
<summary>My workspace does not reflect changes in Typescript types</summary>

The `vtex link` command does not listen to changes in Typescript types. To solve this issue, run `vtex unlink` to stop the link. Then, link the app again after the new changes.
</details>

<details>
<summary>My endpoint is returning old values</summary>

Set the `no-cache` option on your endpoint's response, as in the following example:

```
ctx.set('Cache-Control', 'no-cache')
```

Notice that, for providing a fast response, caching is enabled by default. However, we understand that a real-time response might be necessary when testing an app during development.

>ℹ️ We strongly recommend that you do not disable cache for stores in production.
</details>

<details>
<summary>My theme changes are not reflecting on my store</summary>

1. Log in to your store's VTEX account.
2. Run `vtex ls` to list the apps installed on your account.
3. Check if the major of the `store theme` app installed is different from the one you are developing.

>ℹ️ To see your changes in action, the version of the theme project you're working must be in the same major as the one from the `store theme` app installed on your account.

4. Check if there is another `store theme` app installed on your VTEX account. If positive, uninstall it.

</details>

## I can't install an app

<details>
<summary>I can't install an app with a major other than <code>0.x</code></summary>


![major](https://user-images.githubusercontent.com/60782333/102230433-9ee4a580-3ecb-11eb-8926-6b5c44750123.png)

Run `vtex ls` to check which apps are included on the [Edition App](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app/) installed on your account. If you see the app you're trying to install with another major, you might have an issue with the Edition App installed on your account.

In this case, consider [opening a support ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) to change the Edition App installed on an account. First, go to the [Edition App](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-edition-app/) doc to learn more about the available Edition Apps.
</details>

## I can't create a new workspace

<details>
<summary>Render fail when sender is vtex.menu, Request failed with status code 400</summary>

#### Checking if the Search Integration process started

1. Open your account admin and go to *Store Setup > Search > Integration Settings*.
2. Check if the search has been activated in the store.
3. Press the *Start integration* button to start integration.

The indexing process will start and you will see a link to the Indexing Status screen.

>ℹ️ The [Integration settings](https://help.vtex.com/en/tracks/vtex-intelligent-search--19wrbB7nEQcmwzDPl1l4Cb/6wKQgKmu2FT6084BJT7z5V) is responsible for the Catalog's initial indexing with VTEX Intelligent Search. After installing the application, this will be the first step to integrating it with the Catalog.

![start-integration](https://user-images.githubusercontent.com/60782333/102246861-fab82a00-3edd-11eb-8115-8ecdf892262c.png)
</details>

>⚠️ Still having trouble? Contact our [support team](https://help-tickets.vtex.com/smartlink/sso/login/zendesk)!
