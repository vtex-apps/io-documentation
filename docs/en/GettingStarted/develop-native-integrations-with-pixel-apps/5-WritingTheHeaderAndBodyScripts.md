# 4. Writing the header and body scripts

Now, it is time to define the scripts that your Pixel app will run on the store website. You can specify scripts that execute inside the `<header>` and/or `<body>` tags.

Adding a script to the `<header>` ensures that it will be executed before any other HTML element is rendered on the page. Although this may harm your store's performance, it is a good option if your Pixel app relies on the interaction between users and the store components. On the other hand, adding a script to the store's `<body>` tag may not harm performance scores but at the cost of losing user data. Choose wisely according to your Pixel app functionality.

## Step by step

1. Open the `pixel/header.html` file and replace the provided function with your own. 

  >ℹ️ If you opt to execute your script inside the `<body>` tag, rename the `header.html` file to `body.html`.
   
2. Use the `settingsSchema` identification key previously defined where applicable. Take the following example:

```html
<script>
  // Using via JavaScript
  var appId = "{{settings.gtmId}}";
</script>

<!-- Using directly in an HTML tag -->
<script src="//foobar.com?gtmId={{settings.gtmId}}"></script>
```
