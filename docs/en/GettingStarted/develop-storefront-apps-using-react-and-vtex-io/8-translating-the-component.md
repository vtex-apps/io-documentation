# 7. Translating the component
 
Before thinking about brand globalization, it is very important to first look into **content internationalization on your website**.
 
**Messages** is the VTEX IO app that translates store components, working directly on block code so that the development cycle is not limited by the necessary versioning flow from one language to another.
 
Once implemented in the app, Messages automatically identifies and interprets passive text messages for translation, reducing obstacles in the evolution process of your code–except in cases where you have already entered a customized translation manually.
 
## Configuring Messages
 
For Messages to work as expected, we will use the [`react-intl`](https://formatjs.io/docs/react-intl) library. Serving as a translation engine, this highly versatile library has several advanced internationalization features (*i18n*) for your *front* app.
 
1. Open your app's code in the code editor of your choice.
2. Access the `react` folder and then run the command `yarn add react-intl@3 && yarn add @types/react-intl@3 --dev`.
3. Access the `manifest.json` file and add the `messages` builder to the `builders` list, as shown in the following example:
 
```diff
{
  ...
  "builders": {
	"react": "3.x",
	"docs": "0.x",
+ "messages": "1.x"
  },
  ...
}
```
 
4. Save your code changes.
 
All set! Having all the `react-intl` dependencies installed and the Messages [builder](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-builders/) configured, we can proceed to the next steps.
 
## Allowing automatic translations
 
To understand how VTEX IO translations work in practice, consider the React `HelloWorld` component imported in article 3 of this series:
 
```ts
import React from 'react'
 
const HelloWorld = () => <div>Hello World!</div>
 
export default HelloWorld
```
 
Note that, regardless of the language used on the store page, the `Hello World!` text will be rendered in the component.
 
In order to have the `Hello World!` text automatically translated when the page language changes, we have to use the `FormattedMessage` component from the `react-intl` package to specify which strings should be translated into other languages.
 
As a parameter for the `FormattedMessage` component, we will have a unique ID (`id`) associated with a specific string declared in your app:
 
1. Substitute the `HelloWorld` component code with the code below:
 
```ts
import React from 'react'
import { FormattedMessage } from 'react-intl'
 
const HelloWorld = () => {
  return (
	<div>
  	<FormattedMessage id="store/my-app.hello"/>
	</div>
  )
}
 
export default HelloWorld
```
 
>⚠️ Note that in the example above we use the <code>FormattedMessage</code> component by associating it to the `"store/my-app.hello"` ID, which we created for our example. Since each ID has to be linked to a single string only, it is necessary to define the `FormattedMessage` component in this folder as many times as necessary in accordance with the translatable strings.
 
>ℹ️ When creating an `id`, consider using the <code>store/</code> or <code>admin/</code> prefixes (depending on your app's functionality) followed by the app name (< code>my-app</code>) and, finally, a short word that can identify this string. For example, `store/my-app.hello`.
 
2. In your app's root directory, create a `messages` folder.
3. In the newly created folder, create a new `.json` file named using the ISO code for the desired language. For example: `pt`, `en`, `fr`.
4. In the desired language file, such as `messages/en.json`, associate the `id` used in the `FormattedMessage` component with the desired string:
 
```json
{
  "store/my-app.hello" : "Hello World!"
}
```
 
5. Save all your code changes.
 
When you [*link*](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) your app again and change the page language, you will notice that the text `Hello World!` is automatically translated into the UI thanks to the `react-intl` library component and Messages.
 
>ℹ️ To test these effects in the store linked to your VTEX account, access `https://{workspaceName}-{accountName}.myvtex.com` and add the query string `cultureInfo` with desired language value. For example, to check your page in Brazilian Portuguese type: `https://{workspaceName}-{accountName}.myvtex.com/?cultureInfo=pt-BR`, substituting `{workspaceName}` and `{accountName}` with the development workspace name and your VTEX account name, respectively.
 
## Overwriting automatic translations
 
Depending on your business scenario, you may want to change an automatic translation with a customized one.
 
In this section, we will teach you how to override Messages’ automatic translations using the same example as before:
 
1. In the `Messages` folder, access the file you want for the translation language that will be overwritten (`messages/pt.json`, for example).
2. In this file, define a new translation for the same `id` previously linked to the desired string. For example:
 
```json
{
  "store/my-app.hello" : "Olá, pessoal!"
}
```
 
By linking the same `id` to another translation, you are telling VTEX IO to ignore Messages’ automatic translation and consider only the one you defined manually.
 
[*Link*](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-linking-an-app/) your app again and change the page language to Portuguese to see how the translation you defined is rendered!
 
## Advanced translations
 
Internationalizing a component can mean more than translating its strings. For example, it can include changing price and percentage formatting.
 
Having your app's purpose in mind, you can (and should) make some adjustments to the rendered messages when they contain:
 
- Price representations;
- Variable values;
- Gender and number agreement dependencies
- Percentage representations;
- Dynamic messages, such as error messages.
 
### Adjusting price representations
 
Price formatting for describing prices varies from country to country. If the app you are developing includes price variables, it is essential to set it up to handle different internationalization scenarios.
 
To automate these price changes in the translation flow, you need to add the `vtex.format-currency` library to your app's dependencies:
 
1. Access the `manifest.json` file and add `vtex.format-currency` to the `dependencies` list:
 
```diff
  dependencies: {
+ "vtex.format-currency": "0.x"
  }
```
 
2. Access the file created in the `react` folder for the imported React component.
3. Once you are in it, import the `FormattedCurrency` component from `vtex.format-currency`.
4. Use the `<FormattedCurrency value={price} />` format to indicate that the variable `price` should be treated as the price notation value. For example:
 
```ts
import React from 'react'
import { FormattedCurrency } from 'vtex.format-currency'
 
const PriceComponent = () => {
  const price = 10.50
 
  return (
	<div>
  	<FormattedCurrency value={price} />
	</div>
  )
}
 
export default PriceComponent
```
 
4. Save your code changes.
 
### Adjusting variable values
 
It is common to have a variable in the middle of the message that the component is rendering.
 
Consider our `HelloWorld` example. To render a greeting following the format `Hello, {userName}!`, we have to use **variable interpolation**.
 
Given you have already added the `react-intl` package to your app's dependencies, as explained earlier in this article, follow the instructions below: 
 
1. Access the file created in the `react` folder for the imported React component.
2. Once you are in it, import the `FormattedMessage` component from `react-intl`, setting the variable `user` (sent as a component parameter) using the following standard format: `<FormattedNumber id={id} values={{ user: user }}/>`. For example:
 
```ts
import React from 'react'
import { FormattedMessage } from 'react-intl'
 
const HelloUser = () => {
  const user = 'John'
 
  return (
	<div>
  	<FormattedMessage id='store/my-app.hello-user' values={{ user: user }} />
	</div>
  )
}
 
export default HelloUser
```
 
3. Access the file containing Messages’ translations for the desired language (`messages/en.json` for example).
4. For the `FormattedMessage` `id` (in our example, `store/my-app.hello-user`), define the string that will be rendered in English using the value passed in `user`:
 
```json
{
	"store/my-app.hello-user" : "Hello {user}!"
}
```
 
5. Save your code changes.
 
>ℹ️ If concatenating the string seems complicated, we recommend reading this [documentation](https://format-message.github.io/icu-message-format-for-translators/index.html). It will help your learning process, explaining more details about formatting messages using ICU and variable interpolation.
 
### Adjusting gender and number agreement
 
A variable's gender and number have a direct impact on string concatenation.
 
For example, when you do a search, it may return nothing, return one result, or even several results at the same time. That means the answer that we want to render for the user will not remain constant, varying depending on the search itself and the results that are found.
 
If we analyze this case, it turns out we could render `No products found`, `One product found`, and `X products found`, respectively.
 
To make the messages in your app agree in gender and number in their given scenario, we will use **variable interpolation**.
 
Given you have already added the `react-intl` package to your app's dependencies, as explained at the beginning of this article, follow the instructions below:
 
1. Access the file created in the `react` folder for the imported React component.
2. Import the `FormattedMessage` component from `react-intl`, setting the `myQuantity` variable (sent as a component parameter). Use the following format: `<FormattedNumber id={id} values={{ quantity: myQuantity }}/>`. For example:
 
```ts
import React from 'react'
import { FormattedMessage } from 'react-intl'
 
const PluralSingularComponent = () => {
  const myQuantity = 1
 
  return (
	<div>
  	<FormattedMessage id='store/my-app.pluralsingular' values={{ quantity: myQuantity }} />
	</div>
  )
}
 
export default PluralSingularComponent
```
 
3. Access the file containing Messages’ translations for the desired language (`messages/en.json`, for example).
4. For the ` FormattedMessage` `id` (`store/my-app.pluralsingular` in our example), define the string that will be rendered in English as per the value returned by `myQuantity`:
 
```json
{
	"store/my-app.pluralsingular" : "{quantity, plural, =0 {No product found} one{One product found} other{# products found}}"
}
```
 
5. Save your code changes.
 
>ℹ️ If concatenating the string seems complicated, we recommend reading this <a href="https://format-message.github.io/icu-message-format-for-translators/index.html">documentation</a>. It will help your learning process, explaining more details about formatting messages using ICU and variable interpolation.
 
### Adjusting percentage representation
 
Like prices, percentages are expressed in different ways depending on where you are.
 
If the app you are developing has variables with percentages, it is essential to set it up to handle different internationalization scenarios.
 
Given you have already added the `react-intl` package to your app's dependencies, as explained at the beginning of this article, follow the instructions below: 
 
1. Access the file created in the `react` folder for the imported React component.
2. Import the `FormattedNumber` component from `react-intl`, defining the `value` and `style` properties with the following format: `<FormattedNumber value={variable} style="percent"/>`. For example:
 
```ts
import React from 'react'
import { FormattedNumber } from 'react-intl'
 
const PercentageComponent = () => {
  const percent = 0.1
 
  return (
	<div>
  	<FormattedNumber value={percent} style="percent" />
	</div>
  )
}
 
export default PercentageComponent
```
 
3. Save your code changes.
 
### Adjusting dynamic messages
 
There are cases where you cannot predefine the message displayed by the block because it depends directly on actions taken by users during navigation. A common case of dynamic messages on the interface is HTTP error messages.
 
Given you have already added the `react-intl` package to your app's dependencies, as explained at the beginning of this article, follow the instructions below: 
 
1. Access the file created in the `react` folder for the imported React component.
2. Import the `FormattedMessage` component from` react-intl`, defining the `errorCode` variable (sent as a component parameter) to match the HTTP status code returned. For example:
 
```ts
import React from 'react'
import { FormattedMessage, defineMessages } from 'react-intl'
 
const messages = defineMessages({
  404: {
	id: 'store/my-app.errors.404',
  },
  500: {
	id: 'store/my-app.errors.500',
  },
})
 
const ErrorMessage = ({ errorCode = 500 }) => {
  return {
	<div>
  	<FormattedMessage id={messages[errorCode].id} />
	</div>
  }
}
 
export default ErrorMessage
```
 
3. Save your code changes.
 
>ℹ️ Note that we use a variable to choose the `id` used in the `FormattedMessage` component, making the message dynamic. To declare dynamic messages in your block's code, you need to describe all possible exported messages in an object passed in the `defineMessages` function from the `react-intl` package. This function, which returns the same object without changes, is useful for analyzing the code statically, ensuring that Messages delivers only the messages necessary for the browser to render.
