# 6. Consuming data

Now you need to learn how this new component will talk with the *back-end* system, in other words, how it is going to **consume and insert data in the platform**. 

Communication between store-front apps and VTEX IO is done through **GraphQL APIs**.

## Understanding GraphQL

GraphQL is a language for APIs whose main advantage is the **possibility to request specific data through a single endpoint**, avoiding *overfetching* and *underfetching*.

To manage the data consumed in GraphQL, we will use a library called [**React Apollo**](https://www.npmjs.com/package/react-apollo) that provides native components to perform data searches.

The main components in this library are:

| Name | Description |
|-----|-----|
|[useQuery](https://www.apollographql.com/docs/react/data/queries/) | *React Hook* which, when executed, queries the server using the *GraphQL API* and returns what was requested in the *query* variables. | 
|[useMutation](https://www.apollographql.com/docs/react/data/mutations/) | *React Hook* which returns a function that, when executed, communicates with the server from the *GraphQL API* in order to send *updates* and overwrite data. |

The `useQuery` *React Hook* returns an object that contains the following properties:

 - `loading` (`boolean`) - Returns `true` if the *GraphQL API* is still being executed. Otherwise, it returns `false`.
 - `error` (`any`) - Only assumes a value when an error occurs when communicating with the server.
 - `data` (`any`) - Contains the object returned from the *query* execution.

The `useMutation` *React Hook* returns an *array* containing:

- A function that can be called at any time to communicate with the server.
- An object that represents the current state of *mutation* that has the properties `loading`, `error`, and `data`.

Keeping in mind the objects received by the `useQuery` and `useMutation` *React Hooks*, it is possible to define what you want to render in *React* for the specific `loading` and `error` conditions, in addition to managing the content returned by queries made in the API (stored in `data`).

>ℹ️ To better understand the detailed instructions below, we recommended having a basic knowledge of the GraphQL language. If you are not familiar with the solution, we recommended checking the [documentation](https://graphql.org/learn/) and reading it carefully before proceeding to the next steps.

## Installing the React Apollo library

Using your terminal, access your app's directory and run the command shown below to install the `npm` *React Apollo* library: 

```sh
yarn add react-apollo
```

## Making queries in GraphQL

For your component to render the information provided by the VTEX IO platform, you have to query the data stored on the server using *GraphQL APIs*.

![GraphQL-query](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/GettingStarted/develop-storefront-apps-using-react-and-vtex-io/assets/consuming-data-1.png?raw=true)

We will use the `useQuery` *React Hook* to do this:

1. Open your app's code in the code editor of your choice.
2. In the `react` folder, access the` HelloData.tsx` file or create it if it does not already exist.
3. In this file, copy and paste the basic model below to build your *GraphQL query*:

```jsx
import { useQuery } from 'react-apollo'
import QUERY_VALUE from './helloData.gql'

const HelloData = () => {
  const { loading, error, data } = useQuery(QUERY_VALUE)

  if (loading) {
    return 'Loading…'
  }
  if (error) {
    return `Error ${error}`
  }

  return `Done fetching ${data}`
}

export default HelloData
```

Note that the `QUERY_VALUE` property is being imported from another file called `helloData.gql`. The `.gql` extension hints that it is a file written in *GraphQL*. The content of this file varies depending on the *query* that the app will send as a request.

A simple example for `helloData.gql` would be:

```gql
query hello {
  hero {
    name  
    height
  }
}
```

The response, depending on the database, could be something like:

```json
{
  "hero": {
    "name": "Luke Skywalker",
    "height": 1.72,
  }
}
```

Notice how the `useQuery` React Hook returns an object with `loading`, `error`, and `data` as parameters, which are filled from the query done on the server. By holding the values of these parameters, it is possible to **condition what is rendered in the interface**.

According to the example above, if `loading` returns `true`, the message `Loading...` will be rendered. If an error occurs, the message `Error {error description}` will be rendered instead. Finally, if the `data` parameter receives the values of the executed *query* correctly, the message `Done fetching {data obtained from the query}` will be rendered.

>ℹ️ Check [this](https://www.apollographql.com/docs/react/data/queries/) practical example of a GraphQL query.


## Mutating in GraphQL

In addition to *queries*, *mutations* are another type of operation available for GraphQL APIs. 

*Mutations* are used to insert or modify data that already exists on the platform; they are used to send *updates* to the server.

![GraphQL-mutation](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/GettingStarted/develop-storefront-apps-using-react-and-vtex-io/assets/consuming-data-2.png?raw=true)

1. Open your app's code in the code editor of your choice.
2. In the `react` folder, access the `HelloMutation.tsx` file or create it if it does not already exist.
3. In this file, copy and paste the basic model below to run a *mutation* `gql` using the *React* component:

```jsx
import { useMutation } from 'react-apollo'
import MUTATION_VALUE from './helloMutation.gql'

const HelloMutation = () => {
  const [doSomething] = useMutation(MUTATION_VALUE)

  return <button onClick={() => { doSomething() }}>Click me</button>
}

export default HelloMutation
```

In this case, unlike the `useQuery` *hook* where the *query* is executed immediately, the call to the server will only be made after calling the function returned by the `useMutation` *hook* (`doSomething` in this example).

It is possible to add *mutation* parameters as `doSomething` function variables.

Let us say, for example, that one of the *mutation* variables you are running is the name of a city (`cityName`). One way to pass this variable would be:

```diff
- return <button onClick={() => { doSomething() }}>Click me</button>
+ return <button onClick={() => { doSomething({ variables: { cityName: 'Rio' ) }}>Click me</button>
```

>ℹ️ Check [this](https://www.apollographql.com/docs/react/data/mutations/) practical example of a GraphQL mutation.


## Debugging queries and mutations in GraphQL

To test GraphQL *queries* and *mutations*, we will use the GraphQL IDE app.

To install this app on your VTEX account, run the following command on your terminal:

```sh
vtex install vtex.admin-graphql-ide
```

Once the app is installed, follow the steps outlined below:

1. Access the VTEX admin for the account you are using.
2. In the sidebar, go to **Apps**.
3. Look for GraphQL IDE in the installed apps list.
4. In the `Choose your app from the list below` field, select the name of the app where you want to debug/test. In this case, you need to choose the name of the app you are developing. 

>ℹ️ Remember that, until now, the front app you have been developing has been living in your local files, being connected to the VTEX platform only by the `link`. To find the name of your app in this listing and be able to debug, it needs to be already available (published) and properly installed in the account's Master workspace. The necessary settings to make your app publicly available are described in the last section of this walkthrough.


5. On the left side of the text editor, type the *query* or *mutation* that you want to run for testing purposes. 
6. Then click on the *play* button, and the API query response will appear in the text editor to the right. 

If you need help, there is a `docs` tab on the right corner of your screen that describes the queries and mutations available for the selected app.

![GraphQL IDE example](https://camo.githubusercontent.com/7e7dc6c6c4463c904d1442fca59730dbc2d24082/68747470733a2f2f692e696d6775722e636f6d2f68734d747843322e706e67)
*The example above shows how to use the GraphQL IDE Admin to query an internal route in the `vtex.rewriter` app.*
