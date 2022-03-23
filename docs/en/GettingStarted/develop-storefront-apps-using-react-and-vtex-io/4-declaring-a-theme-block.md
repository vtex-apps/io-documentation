# 3. Declaring a theme block

With the app template already copied, we will now create a **new theme block**. Follow the instructions below to create the new theme block.

## Before you start
1. It is important that you are already familiar with VTEX Store Framework and fully understand what a block, store theme, and template are. If you are not familiar with these concepts or want to refresh them a little before working with the settings, check [**Build stores with Store Framework**](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3).

2. When creating a storefront component, follow the best practices regarding tooling, features, flexibility, scalability, performance, accessibility, internationalization, and styling, to be adopted when creating your storefront component. Check [**Developing custom storefront components**](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-custom-storefront-components) for more information.

## Understanding interfaces

An interface basically works as an API (*application programming interface*) that defines the theme blocks’ behaviour following the React component that they render.

In the same way that an API uses parameters to define how the conversation with a server will take place, the interface uses what we call *keys*. 

**The interfaces, using their keys, define a block's behavior when implementing and rendering in a store theme**. 

This means that, for each theme block exported by your app, you will need to define an [interface](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-interface), linking the block to a React component of your choice.

The following table shows some possible keys that could be added to your block's interface, as well as their respective descriptions:

| Key | Description | 
|----- | ----- |
| `component` | Name of the React component that is linked to the theme block, in other words, name of the React component that the theme block will render.|
| `allowed` | List of other theme blocks that, when declared, will help build the desired React component. In practice, blocks declared as `allowed` must be declared in the theme app (Store Theme) as children to the block you developed.|
| `composition` | Defines whether the children of the block you are developing will have a specific rendering position in the interface or not. Remember that when defining the `composition` key, you are not controlling the positioning of the block defined by it, but the positioning of that block's children. Possible values for this key are `blocks` (the child blocks have a specific position in the interface, according to the React component on which they are based) or `children` (the position of the child blocks depends exclusively on how they are declared in the theme). If no value is defined for the `composition` key, the platform default is `blocks.`|
| `device` | Defines whether your theme block is designed for mobile or desktop devices. Possible values are `mobile` (designed for mobile devices) and `desktop` (designed for desktop devices).|
| `required` | List of theme blocks that must be rendered in the interface to support the block rendering you are developing.|
| `around` | List of theme blocks that must be rendered in the interface around your new block for its correct functioning.|
| `before` | List of theme blocks that must be rendered in the interface before your block (above it) for its correct functioning. For example: header. |
| `after` | List of theme blocks that must be rendered in the interface after your block (below it) for its correct functioning. For example: footer. |
| `preview` | Defines the behavior of the page while the block is loaded. |
| `render` | Defines the block's rendering type. Possible values are `lazy` (the block is only rendered when a user interacts with it), `server` (the block is rendered from the server side), or `client` (the block is rendered from the client side, that is, by the browser). |

The only mandatory key that needs to be declared in a block interface is `component`. You have to declare the other ones according to the desired scenario for your new theme block.
 
## Declaring an interface

We declare the interface of one or more blocks in the app's `interfaces.json` file, used by [Store Builder](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders/) to correctly build your website's *front-end*.

For this example, we will create an interface for a basic block called `hello-world` (based on the React `HelloWorld` component). 

When following these steps, remember to replace the values with the ones that correspond to your app’s actual scenario, in accordance with the React component you are actually importing.

1. Open your app's code (previously called `react-app-template`) in your code editor.
2. In the `react` folder, create a new TypeScript file with the name of the desired React component. According to our example, we would have `HelloWorld.tsx`.
3. Once you are in the file, add the sample code below (replacing the values according to your scenario):

```jsx
import { React } from 'react'

const HelloWorld = () => <div>Hello, World!</div>

export default HelloWorld
```

> ℹ️ 
> 
> Be sure to check out the [React solution](https://reactjs.org/docs/getting-started.html) and [Developing custom storefront components](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-developing-custom-storefront-components) documentation to better understand how components work.

4. On the first level of your app's folders create a new folder called `store`.
5. In the `store` folder, add a new file called `interfaces.json`.
6. Declare the component's interface in the new file. For example:

```json
{
 "hello-world": {
    "component": "HelloWorld"
  }
}
```

Notice the above structure, the first definition given by the interface is the name of your new theme block (`hello-world`). Within it, we declare an object containing the interface keys previously described.

In our basic example, we only use the `component` key to link the` hello-world` block to the React component that it will render (`HelloWorld`). Note that the value of the `component` key is `HelloWorld`–the file name that was previously created for the React component (`react / HelloWorld.tsx`).

>ℹ️ Be sure to check code from native Store Framework apps to learn more about structuring the <code>interfaces.json</code> file, such as [Search Result](https://github.com/vtex-apps/search-result/blob/master/store/interfaces.json) and [Header.](https://github.com/vtex-apps/store-header/blob/master/store/interfaces.json) Remember that the way we declare an interface depends directly on the behavior we want for the new block. That is why as we study different apps and blocks, we understand more the possibilities for interfaces.

After saving your code changes, your new block will be ready to be implemented by any user who installs your app.

> ℹ️
>  
> If the app under development exports more than one theme block for rendering the React component, all of these blocks' interfaces must also be declared in the <code> interfaces.json</code> file, according to the format indicated above.

### Declaring different interfaces by breakpoint 

You may want your app to export different blocks for rendering different components according to the store's *breakpoint*, in other words, according to the device that is accessing it.

To do this, you have to create different blocks for each possible device and, consequently, create interfaces for each one of them. 

For example, you are developing the `hello-world` block and want to create mobile and desktop versions for it. You will have to create the `HelloWorld`,` HelloWorldMobile`, and `HelloWorldDesktop` components, and define interfaces for each, such as `hello-world`, `hello-world.mobile`, and `hello-world.desktop`. 

The parent block's `hello-world` interface has to contain only the `component` and `allowed` keys, the latter declaring the `hello-world.mobile` and `hello-world.desktop` blocks. 

The interfaces for the last blocks, in turn, have to declare the desired keys to define the behavior of each block according to the device for which they were designed, such as the `device` key. 

App examples that use different React components for different devices are [Header](https://github.com/vtex-apps/store-header) and [Footer](https://github.com/vtex-apps/store-footer).

## Using your new theme block

We will now implement the new block you created.  

If the VTEX account you are working on already has the Store Theme app for VTEX Store Framework installed, follow the instructions below from step 2. If your account does not yet have the Store Theme app installed, follow the instructions from step 1:

1. Read carefully [step 3 in the Build stores with Store Framework section](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3) and follow the steps detailed in the article. Once you are done, you will have implemented the standard theme for the VTEX Store Framework and will be ready to test your new block.
2. Open the Store Theme app folder in your local files using the code editor of your choice.
3. In the Store Theme `manifest.json` file, add the front app you are developing as a dependency in `dependencies`. For example:

```diff
"dependencies": {
+   "yourVTEXAccountName.yourAppName": "0.x",
    "vtex.store": "2.x",
    "vtex.store-header": "2.x",
    "vtex.product-summary": "2.x",
    "vtex.store-footer": "2.x",
    "vtex.store-components": "3.x",
    ...
}
```

4. Then, add the new theme block (`hello-world` in our example) to one of the templates. For this walkthrough, we will add the `hello-world` block to the store's home page, in the `store.home` template:

```diff
{
  "store.home": { 
     "blocks": [
+       "hello-world"
     ]
  },
  ...
}
```

5. [Link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) the store's theme with the VTEX IO platform to verify the results:

![image](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/GettingStarted/develop-storefront-apps-using-react-and-vtex-io/assets/declaring-a-theme-block.png?raw=true)

6. Access your VTEX store using the structure `{workspaceName}-{accountName}.myvtex.com` 
to see your new `hello-world` block being displayed in your development *workspace*:

![image](https://user-images.githubusercontent.com/18701182/78391781-74f98600-75bd-11ea-9482-2b68f6549caa.png)
