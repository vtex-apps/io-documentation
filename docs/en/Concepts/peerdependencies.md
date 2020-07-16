# Peer Dependencies

Peer dependencies is how we call a JSON object field (`peerDependencies`) in the app's `manifest.json` file. 

This field is used to specify the set of **IO apps** an app relies on to properly work. However, unlike regular dependencies, peer dependencies **are not automatically installed** in an account. Hence, setting peer dependencies can be especially useful for cases when an app relies on a **paid app**, for example.

Another use case for the `peerDependencies` field is when you need to guarantee that an account trying to install your new app has the exact same version of the dependencies your app relies on previously installed.

To make it more tangible, take the following example, in which `vtex.store@2.x` and `vtex.paid-app-example@1.x` are declared as peer dependencies of the `vtex.example` app.

```json
{
  "name": "vtex.example",  
  ...
  "peerDependencies": {
      "vtex.store": "2.x",
      "vtex.paid-app-example": "1.x"
  },
  "dependencies": {
      "vtex.styleguide": "9.x"
  }
  ...
}
```

For this example, if you wanted to install the `vtex.example` app in an account, you'd first need to manually install the exact versions of `vtex.store` and `vtex.paid-app-example` apps declared under the `peerDependencies` field.

Now, considering the development context, suppose the following: you are developing an app that directly depends on the `vtex.example` app. Therefore, you list `vtex.example` as a dependency in the `dependencies` field from the `manifest.json` file. The `vtex.example`, in turn, has `vtex.store@2.x` and `vtex.paid-app-example@1.x` set as its `peerDependencies`. 


If your account does not have `vtex.store@2.x` and `vtex.paid-app-example@1.x` installed, you won't be able to install the `vtex.example` and your development flow will be interrupted.

Notice that, this way, the `vtex.example` forces every account that is installing it to also have `vtex.store@2.x` and `vtex.paid-app-example@1.x` installed. 

<div class="alert alert-warning"><strong>Keep in mind:</strong> Peer dependencies are not automatically installed, therefore you will have to manually install them in the account in which you are working. As a result, if your app relies on a paid app you should declare it as a peer dependency.</div>
