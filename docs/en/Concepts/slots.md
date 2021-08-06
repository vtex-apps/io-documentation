# Slots

Slots composition is a new way to declare a React component in your store theme code.

Working simarly to the blocks and children composition, the slots allows you to use React props instead of passing an array of blocks when rendering a component on the store UI. 

It enables Store Framework users to be way more flexible when developing the store theme by removing the need for the `allowed` property in the components' interface definitions!  

Some advantages of using slots over the traditional blocks composition are, namely:

- No need for `blocks` attribute when implementing a component in the store theme. Users just need to pass the desired blocks as regular props.
- No need for the `allowed` interface attribute. Any block from any app can be declared as a regular prop. 

## Practical example

Let's suppose you are trying to create a `hello-world` block. At first, it could be as simple as:

```jsx
// HelloWorld.tsx
import React from 'react'

const HelloWorld = () => <div>Hello, world!</div>

export default HelloWorld
```

```json
// interfaces.json
{
  "hello-world": {
    "component": "HelloWorld"
  }
}
```

Let's now set up an icon to be displayed right above the "Hello, world!" text:

```jsx
// HelloWorld.tsx
import React, { ReactElement } from 'react'

const HelloWorld = ({ Icon }) => (
  <div className="tc pv5">
    <Icon size={32} />
    <h1 className="t-heading-1 c-on-base">Hello, world!<h1>
  </div>
)

export default HelloWorld
```

Notice that in the example above the icon is being declared via props to the `HelloWorld` component, clarifying how the slots composition logic works in the development flow.  

In practice, users would pass this value to the theme *block* `hello-world`, as shown in the `json` example below:

```json
{
  "hello-world": {
    "props": {
      "Icon": "icon-caret#point-up"
    }
  },
  "icon-caret#point-up": {
    "props": {
      "orientation": "up"
    }
  }
}
```

According to the slots composition logic, there is no need to use the `allowed` field in the block's interface definition the component it displays works independently.

## What is the difference between slots and blocks composition?

If you've been using Store Framework for a while, you are probably familiar with the `blocks` property - whose functionality is the same as the slots'.

According to the `blocks` prop logic, you could configure your theme as shown below and still achieve pretty much the same results on your store UI:

```json
{
  "hello-world": {
    "blocks": ["icon-caret#point-up"]
  },
  "icon-caret#point-up": {
    "props": {
      "orientation": "up"
    }
  }
}
```

```jsx
// HelloWorld.tsx
import React from 'react'
import { ExtensionPoint } from 'vtex.render-runtime'  

const HelloWorld = () => (
  <div className="tc pv5">
    <ExtensionPoint id="icon-caret" size={32} />
    <h1 className="t-heading-1 c-on-base">Hello, world!<h1>
  </div>
)

export default HelloWorld
```

```json
// interfaces.json
{
  "hello-world": {
    "component": "HelloWorld",
    "allowed": ["icon-caret"]
  }
}
```

However, if we decide to use the `blocks` composition as shown above, we would face some restrictions, such as:

- The `hello-world` block would **only** be able to receive an `icon-caret` block. Any other `icon-*` block, or any block whatsoever, would not work. To make it work we would need to allow each different block users would be able to use.
- The `blocks` approach would also be trickier to implement in `HelloWorld.tsx` because we would need to check which block was passed by the user to then pass its ID to the `ExtensionPoint` component.
- Through the use of `ExtensionPoint`s, we would not be able to render multiple instances of the same block as well. For example, if we wanted to render `icon-caret#foo` **and** `icon-caret#bar` in our `HelloWorld` component, we would not be able to do so using `<ExtensionPoint id="icon-caret" />`, since this would be ambiguous. Also, the user would not be able to pass multiple instances of the same block to `hello-world`, such as:

```json
{
  "hello-world": {
    "blocks": ["icon-caret#point-up", "icon-caret#point-down"]
  },
  "icon-caret#point-up": {
    "props": {
      "orientation": "up"
    }
  },
  "icon-caret#point-down": {
    "props": {
      "orientation": "down"
    }
  }
}
```

The main difference, therefore, is that we can offer much more flexibility to our users when using the slots composition.

## Restrictions

There are some limitations put in place to guarantee that your slots will be working consistently:

1. Slots are **always** exposed via `PascalCased` props. This is very important because otherwise our builder would not be able to identify the props as `slots` which, in turn, would block the component rendering:

```jsonc
{
  "props": {
    // Does NOT work. This will be interpreted as a string by store builder
    "icon": "icon-caret"
  }
}
 ```

```jsonc
{
  "props": {
    // Works!
    "Icon": "icon-caret"
  }
}
```

2. *Nested* slots are not currently supported. This means that you can't have a slot prop inside of an object, such as shown below:

```jsonc
{
  "props": {
    "somePropThatsAnObject": {
      "p1": "this",
      "p2": "will",
      "p3": "not",
      "p4": "work",
      // This will NOT be picked up by the store builder
      "Slot": "some-block"
    }
  }
}
```
