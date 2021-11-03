# 4. Defining styles

After defining your theme's block, it is time to think about the style you want for it, defining colors, typography, among other elements that establish the visual identity of the app when it is rendered. 

To define the style of your component(s), we will use *Cascading Style Sheets* - **CSS**. 

In VTEX IO, there are three different tools for using CSS in a store:

- **Tachyons** - Main option for styling components from CSS classes.
- **CSS Modules** - Secondary option for styling components from CSS classes. It should only be used when the desired style cannot be configured using Tachyons.
- **CSS Handles** - Exports generic CSS classes to allow users that work with your component to customize it according to their respective scenarios.

Now that you know the difference between the tools that are available on the platform, you are ready to learn more about them. 

Below, you can find the instructions for each of these tools and their purpose.

>ℹ️ Customizing the style in a component requires basic CSS knowledge. We recommended that you check the [documentation](https://www.w3schools.com/css/default.asp) for this language before following the instructions detailed in this article.

## Using Tachyons

VTEX Tachyons is a functional CSS structure built on a [Tachyons](https://tachyons.io/) base.

The framework has single-purpose CSS classes that can be structured to build anything from complex layouts to responsive components. 

In practice, VTEX Tachyons helps you use CSS classes in your store-front app with little effort.

>ℹ️ To better understand VTEX Tachyons tokens for CSS classes, it is important to familiarize yourself with the Tachyons solution. Carefully read your [documentation](https://tachyons.io/#getting-started).

1. Open your app's code in your code editor.
2. In the `react` folder, access the file created for the component you want to style.
3. Access the [VTEX Tachyons documentation](https://vtex.github.io/vtex-tachyons/) and look for the most appropriate CSS classes according to the customization you want to apply.
4. In the React component code, declare the desired CSS classes. For example:

```css
const Example = () => (
  <div className="flex justify-center pv4 ph3 bg-base--inverted">
    <p>Hello, World!</p>
  </div>
)
```

5. Save your changes. 

## Using CSS Modules

CSS Modules is a CSS file in which CSS classes are designed according to the store-front app that exports the component.

>⚠️ By defining CSS classes this way, the CSS Modules tool becomes limiting when considering the scenarios for importing and exporting components between different apps. That is why we recommend only using VTEX Tachyons in your project. **Use CSS Modules only for cases not solved by Tachyons.**

1. In your app's `react` folder, create the `styles.css` file.
2. In this file, create the desired CSS classes (those not understood by Tachyons tokens). For example:

```css
.myButton {
   background-color: red;
}
```

3. Still in the `react` folder, access the component file being customized and import the `styles` file, created in step 1. For example:

```jsx
import styles from './styles.css'
```

4. It is also possible to import the `styles` file so that the generated CSS classes are private, that is, they are generated with a unique identifier (*hash*) instead of the traditional `vendor-app-major-x-format-classname`. For this, you need to do an import following the model below:

```jsx
import styleModule from './style.module.css'
```

5. From there, the `styles` imported for your component will be an object whose keys will be the names of the classes you created (`className`). For example:

```jsx
/* /react/MyButton.tsx */
import styles from './styles.css'

export default function MyButton() {
  return (
    <button className={styles.myButton}>
      My button
    </button>
  )
}
```

>ℹ️ Remember that the name of the created classes will depend on the *import* model you made (step 3 or step 4 in this section). 

6. Save the changes you made and [link](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) your app. 

When rendered and inspected, the component will now have the following HTML structure if you chose to follow the *import* model shown in step 3:

```html
<button class="vtex-my-app-name-0-x-myButton">My button</button>
```

## Using CSS Handles 

A CSS Handle is an **HTML element identifier**. That is why Handles are very handy when creating store themes, allowing your app users to apply CSS classes according to the visual identity they want.

To make Handles available for future app users, add `vtex.css-handles` to the `dependencies` list in the `manifest.json` file:

```diff
  "dependencies": {
+ "vtex.css-handles": "0.x"  
  }
```

Once `vtex.css-handles` is added as a dependency, your app is ready to generate CSS Handles.

However, when generating them, you will need to pay attention to how your app's React component(s) are imported and defined. 

There are two possible scenarios:

- ***Function components*** - React components are defined in your app using a function.
- ***Class components*** - React components are defined in your app using a class.

### Creating CSS Handles for function components

1. In your app's `react` folder, access the file of the React component you want.
2. Copy and paste the following code example in the file:

```jsx
import { useCssHandles } from 'vtex.css-handles'

const CSS_HANDLES = ['container', 'background', 'text', 'item'] as const
/* Using `as const` at the end hints to Typescript that this array
 * won't change, thus allowing autocomplete and other goodies. */

const Component: FC = () => {
  const handles = useCssHandles(CSS_HANDLES)  
```

3. In the `CSS_HANDLES` array, replace the exemple strings with new ones (according to the names of the *CSS Handles* you want). You can choose any name for the *CSS Handle*, but remember, it will be used with CSS classes by your app users to personalize HTML elements in stores. We recommend choosing intuitive names.

*Following the above example, the variable `(CSS_HANDLES)` will be an object using the following format:*
  
```json
{
  container: 'vtex-foobar-1-x-container',
  background: 'vtex-foobar-1-x-background',
  text: 'vtex-foobar-1-x-text',
  item: 'vtex-foobar-1-x-item',
}
```

>ℹ️ Note that the CSS Handles generated and stored in the object follow this pattern: `vtex-{appName}-{majorVersion}-x-{handleName}`.

4. Add the new *CSS Handle* to the desired CSS class–according to the HTML element to be customized by app users. Remember to use the `handle` variable when adding it and also the *CSS Handle* name defined in the `CSS_HANDLES` array (like `container`). For example:

```css
    <div className={handles.container}>
      <div className={`${handles.background} bg-red`}>
        <h1 className={`${handles.text} f1 c-white`}>Hello world</h1>
        <ul>
          {['blue', 'yellow', 'green'].map(color => (
            <li
              className={`${handles.item} bg-${color}`}>
              Color {color}
            </li>
          ))}
        </ul>
      </div>
    </div>
```

### Creating CSS Handles for class components

1. In your app's `react` folder, access the file of the React component you want.
2. Copy and paste the following code example in the file:

```jsx
import { withCssHandles } from 'vtex.css-handles'

const CSS_HANDLES = ['text'] as const

class ExampleComponent extends Component {
  render() {
    const { cssHandles } = this.props
 ```
 
>ℹ️ Since components defined as classes cannot use *hooks*, we will use an *HOC* called `withCssHandles`.

3. In the `CSS_HANDLES` *array*, replace the example strings with new ones (according to the names of the *CSS Handles* you want). You can choose any name for the *CSS Handle*, but remember, it will be used with CSS classes by your app users to personalize HTML elements. We recommend using intuitive names.

*Following the above example, the variable `{ cssHandles }` will be an object using the following format:*

```json
{
  text: 'vtex-foobar-1-x-text',
}
```

>ℹ️ Note that the CSS Handles generated and stored in the object follow this pattern: `vtex-{appName}-{majorVersion}-x-{handleName}`.

4. Add the new *CSS Handle* to the desired CSS class–according to the HTML element to be customized by app users. Remember to use the `handle` variable when adding it and also the *CSS Handle* name defined in the `CSS_HANDLES` array (like `text`). For example:

```css
<div className={`${cssHandles.text} f1 c-white`}>Hello world</div>
```

After saving your changes, your app will be able to not only export a predefined style according to the CSS classes you set up but also export *CSS Handles*, giving your users more customization flexibility.

>ℹ️ For more details on how *CSS Handles* can be used to define styles, access the documentation for [Using CSS Handles for store customization](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-using-css-handles-for-store-customization).
