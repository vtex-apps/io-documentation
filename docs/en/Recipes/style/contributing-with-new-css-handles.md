---
title: Contributing with new CSS Handles
description: "Create new CSS Handles whenever you feel the need following this step by step."
date: "2020-04-08"
tags: ["contribution", "contributing", "css", "handles"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs/docs/en/Recipes/style/contributing-with-new-css-handles.md"
---

# Contributing with new CSS Handles
  
A CSS Handle is a **CSS class that maps out an HTML element**. Therefore, it can be used to [customize any of the store blocks](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization) by simply using CSS classes in the store theme's code.

At the end of the day, they are nothing more than the store's layout building assistants. The more HTML elements with CSS Handles you have at your disposal, the better!

In the step by step below, we will guide you on how to **create new CSS Handle whenever you feel the need**. To that end, we will create an example of a brand new Handle for a filter from the Search Results page.

## Step by step
  
### Step 1 - Finding the React component

[Install the React Chrome extension](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) in order to be able to see every store page's React tree.

1. Access the store you are working on;
2. Inspect the HTML element that you want to add the new CSS Handle to. By inspecting it, you will see something similar to the structure stated below:

```html
<div tabindex="0" role="link" class="ph5 ph3-ns pv5 pv1-ns lh-copy pointer hover-bg-muted-5 c-muted-1">Hats</div>
```

3. Change the tab opened in Chrome Dev Tools to the `Components` tab;
4. You will then be able to read the name of the highlighted React component. In our example, it's `CategoryItem`:

![React Component name](https://user-images.githubusercontent.com/284515/74465583-6e2f7c00-4e74-11ea-8791-c15681b73917.png)

### Step 2 - Forking the app's repository

To start the process of code contribution, you firstly need to [fork the app repository]((https://help.github.com/en/github/getting-started-with-github/fork-a-repo)) in which you desire to add new CSS Handles and clone your fork to a local directory.

>⚠️ The forked app must be the one that provides the theme block wrapping the HTML element in which you want to add new Handles to.

2. In your terminal, clone the code of the forked app to your local files using `git clone` + the URL of the desired repository;
3. Then, using any code editor, open the app's code;
4. Open the file named after the component highlighted in the `Step 1 - Finding the React component`. Use your code editor search bar to look it up. Following our example, the file name would be `CategoryItem.js`.

Once you find the React component in the app's code, it is time to add the new CSS Handle.
  
### Step 3 - Adding a new CSS Handle

The way you will contribute to a new CSS Handle depends on the React component's implementation and how it imports CSS files.

There are two different ways:

1. Using the `import {useCssHandles} from 'vtex.css-handles'` function;
2. Using the `import styles from './styles.css'` function.

Once in the file name after the React component, give it a good look and check which of the functions it is using to import CSS Files.

According to the function, follow the most suitable instructions stated below:

#### Using the `import {useCssHandles} from 'vtex.css-handles'` function

1. Look for the variable passed to the `useCssHandles` hook;

```jsx
const CSS_HANDLES = [
  'container',
  'element',
]
// ...
const handles = useCssHandles(CSS_HANDLES)
```

*In the example above, the variable passed to the* `useCssHandles` *hook is called* `CSS_HANDLES`.

2. Add a new string to the `CSS_HANDLES` array with the new CSS Handle name;

```diff
 const CSS_HANDLES = [
   'container',
   'element',
+  'headline',
 ]
```

*Following the example given above and considering the* `const handles = useCssHandles(CSS_HANDLES)` *function, the* `CSS_HANDLES` *variable would be an object in the following format*:
  
```js
{
  container: 'vtex-foobar-1-x-container',
  element: 'vtex-foobar-1-x-element',
  headline: 'vtex-foobar-1-x-headline',
}
```

3. Add the new CSS Handle (declared in the `CSS_HANDLES` array) to the HTML element missing a CSS Handle. Remember to use the `handle` variable when adding it;

```diff
- <div className="ph0 mr2">
+ <div className={`${handles.headline} ph0 mr2`}>
```
  
4. Save your changes;
5. Using your terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installment-and-command-reference/), log in to a VTEX account and use a Development workspace to [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) the app you are working on;
6. Access the account's website through the developer workspace (`{workspaceName}--{accountName}.myvtex.com`) and inpect it to verify if the new class is really being properly rendered, making the HTML element targetable.

Following our example, we would have something like:

```html
<div class="vtex-foobar-1-x-headline ph0 mr2">
```

#### Using the `import styles from './styles.css'` function
 
1. Open the CSS file referenced in the `import styles from './styles.css'` function;

```jsx
import styles from '../searchResult.css'
```

*Following our example, we would have to open the* `searchResult.css` *file.*

2. With the CSS file open, create a brand new empty class definition with the name of the CSS Handle that you wish to add. For example:

```css
.headline {}
```

3. Go back to the React component file and add the new CSS Handle (declared in the previous file) to the HTML element missing a CSS Handle. Remember to use the name of the function variable (in our example, `styles`) when adding it;

```diff
- <div className="ph0 mr2">
+ <div className={`${styles.headline} ph0 mr2`}>
```

4. Save your changes;
5. Using your terminal and the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installment-and-command-reference/), log in to a VTEX account and use a Development workspace to [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app) the app you are working on;
6. Access the account's website through the developer workspace (`{workspaceName}--{accountName}.myvtex.com`) and inpect it to verify if the new class is really being properly rendered, making the HTML element targetable.

Following our example, we would have something like:

```html
<div class="vtex-foobar-1-x-headline ph0 mr2">
```

### Step 4 - Adding modifiers

It's also possible to apply modifiers to a specific CSS Handle.

Handle modifiers work as identifiers. They are responsible for overriding the HTML element style according to the behavior assumed by them on the interface, according to user interaction. 

Let's suppose you have a handle called `handles.slide` for each slide of a slider and you want to customize the current visible slide via CSS. For this purpose, you should add a modifier to `handles.slide`, allowing the customization according to the user navigation.

1. Import the `applyModifiers` method:

`import {useCssHandles, applyModifiers} from 'vtex.css-handles'`

2. Instead of directly passing the handle, pass it through the `applyModifiers` method:

```diff
-<div class={{`${handles.slide}`}}">...</div>
+<div class={{`${applyModifiers(handles.slide, isCurrentSlide ? 'active' : undefined}`}}">...</div>
```

Which, for a hypothetical slider with three slides and the first one being focused, would result in:

```html
<div class="vtex-foobar-1-x-slide vtex-foobar-1-x-slide--active">...</div>
<div class="vtex-foobar-1-x-slide">...</div>
<div class="vtex-foobar-1-x-slide">...</div>
```

### Step 5 - Committing your changes

If the new class is being properly rendered, it means that everything is ready for you to create a new CSS Handle.

1. Using your code editor, commit your changes to a new branch;
2. Push your commit so that your changes are sent to the server and included in the history of the app you are developing.
  
### Step 6 - Updating the docs and opening the Pull Request

1. Access then the app's forked repository and switch to the branch in which you committed your changes in the previous step;
2. Open the `CHANGELOG.md` file;
3. Add a new entry under the `[Unreleased]` section clarifying which CSS Handles were created, such as:

```md
## [Unreleased]
### Added
- New CSS Handle `headline`.
```

3. Save your changes in the branch;
4. Using the same branch, update the block documentation (in the `docs` folder of the app's repository) with the new CSS Handles. Use the **Customization** section and the `CSS Handles` table for that. For example:

```diff
 | CSS Handles |
 | ----------- |
 | `container` |
 | `element`   |
+| `headline`  |
```

5. Lastly, save your changes in the branch and [open a Pull Request for the team](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork). In the Pull Request description, remember to provide a link to the workspace used in the development so all of your changes can be tested. For example: `https://john--storecomponents.myvtex.com`.

Once your PR was analyzed and approved, you would have contributed to the app's evolution and a new CSS Handle will be available to you and other Framework users. **Thank you!**
