---
title: Using sandbox blocks
description: "With Store Framework you're able to use iframes to attend specific custom needs"
date: "2019-08-19"
tags: ["iframe", "sandbox", "custom"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/layout/using-sandbox-blocks.md"
---

# Using sandbox blocks

VTEX's store framework is a very powerful tool that is going bigger everyday, so that it can attend most of the its' clients needs. It's understandable, though, that there are extra customizations that compose your store's needs and that the framework may not attend. That's what the **Sandbox App** was created for. 

The **Sandbox App** is basically a component that supports iFrames. Therefore, it's intended to make available the possibility to use custom `html`, `css` and `js` code.

As a front end developer, it might be the case that you tend to think that it's easier then to just use this app whenever it fits, but that is not really what the Store Framework, neither the Sandbox App is about. Creating everything using iFrames will make your store easily obsolete to new Store Framework's features and not really performatic.

**So when, then, should I use the Sandbox App?**, you might be wondering. Take a good look at [all the components](link componentes) we offer see what they're capable of. If you think a component is very similar to what you're trying to accomplish but with some minor changes, then you should find the right styling and props so that it becomes what you need. **Sandbox should be used whenever Store Framework native components won't handle your scenario, and what you want to do is simple enough that doesn't require much out source data.**

Ok, with that in mind, let's get to the point. To use Sandbox App you should first declare it as a dependency. Go ahead to your `manifest.json` file. Edit the dependencies node and add the sandbox app:

![sandbox dependency](https://lh6.googleusercontent.com/xHiHR8-_xYO2NuPaAHSAC2zxaFMCJyP72NIGAPi0EK77D60bdkFkcmvQLqYbenwvlTuTO875jfrMhh5HGxo9OXI7ZtSANTCxTytUJD0d)

Now you need to declare your sandbox block, let's say you want to create a simple `h1` sandbox block, that would be something like:

```
"sandbox#h1": {
    "props": {
        "width": "100%",
        "height": "auto",
        "initialContent": "<h1 style=\"text-align:center;\">Hello World</h1>",
        "allowCookies": false
    }
}
```

Finally, just reference it in a another's block `children` or `blocks`, on your `store.home`, for instance: 

```
//home.jsonc

"store.home": {
    "blocks": [
      "carousel#home",
      *"sandbox#h1"*,
      "flex-layout.row#deals",
      "shelf#home",
      "info-card#home",
      "rich-text#question",
      "rich-text#link",
      "newsletter"
    ]
},
```

That should, therefore, render the h1 sandbox on the store's page:

![Hello world sandbox](https://lh3.googleusercontent.com/Rc4W95PP3U7vWemeuT_Btgw3e-itXkK-L84NFTlHet_2zge_l50ygV4e5CX5CLaH2R4G9xmHya7xiwz3hQ8gPr7QN9RQYgLrLidPs_UN)
