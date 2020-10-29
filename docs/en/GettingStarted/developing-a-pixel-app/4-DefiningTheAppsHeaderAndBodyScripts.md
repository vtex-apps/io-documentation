# Defining the app's header and body scripts

If your Pixel app employs Javascript, then you’ll also need to add scripts to the store's `<header>` and/or `<body>` tags in order to fetch and send the needed data.

> ℹ️ *Adding a script in your store's `<header>` guarantees that the first one will be executed before any other page's HTML element is rendered. Although this may harm your store performance, it is a good option if your Pixel app relies on the interaction between users and the store components. Adding a script in the store's `<body>` tag can increase performance rates, but at the cost of loosing important user data while it is being executed. Choose wisely according to your Pixel-app functionality.*

1. Create a new file called `header.html` inside your app's `pixel` folder in order to add a script to a pages’s `<header>`.
2. Create a new file called `body.html` inside your app's `pixel` folder in order to add a script to the end of the pages’s `<body>` tag.
3. In the desired files, add the `settingsSchema` variable value - the same one used in the previous step. For example:

```html
<script>
  // Using via JavaScript
  var appId = "{{settings.gtmId}}";
</script>

<!-- Using directly in a HTML tag -->
<script src="//foobar.com?gtmId={{settings.gtmId}}"></script>
```

In the example above, we use the `gtmID` user identification.
