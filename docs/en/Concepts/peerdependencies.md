# Peer dependencies

The `peerDependencies` JSON object is a key of a [project manifest](#Manifest) used to specify the set of **IO apps** an app relies on. However, unlike regular `dependencies`, `peerDependencies` **are not automatically installed** and they must be used when you need to guarantee that your app's dependency is exactly the same as the one a person installing your app has installed. Notice that this is useful when talking about **paid apps**.

To make it more tangible, suppose that you are developing an app and that you include app B as a `dependencies`. App B, in turn, has app C set as its `peerDependencies`. In this case, since your app depends on app B, you'll have to manually install app C. Otherwise, you'll receive a warning when trying to install app B. Notice that, this way, app B forces that anyone trying to use its app, also have app C installed. Hence, **if you depend on a paid app, you must declare it as a peer dependency**. 

> <div class="alert alert-warning"><strong>Keep in mind:</strong> Peer dependencies will not be automatically installed!</div>

Check the following manifest of the `example` app:

```javascript
{
  "name": "example",  
  ...
  "peerDependencies": {
      "vtex.store": "2.x"
  },
  "dependencies": {
      "vtex.styleguide": "9.x"
  }
  ...
}
```

For this example, if you needed to use `example` as a dependency of your new app, you'd first need to manually install `vtex.store`, since this is a peer dependency of the `example` app. 
