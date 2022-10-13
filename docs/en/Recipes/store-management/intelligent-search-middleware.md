---
title: Intelligent Search middleware
description: "This guide will show you how to create a middleware for the Intelligent Search API. This way, you will be able to change the request that comes from the client."
date: "2022-07-18"
tags: ["search", "intelligent", "middleware"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/store-management/intelligent-search-middleware.md"
---

# Intelligent Search middleware

In some situations you may want to change the Intelligent Search API request that comes from the client. For example: "If the client searches for shoes, I want to promote the `productId` 123". This is possible with the Intelligent Search Middlewares.

# Creating an IS (Intelligent Search) API middleware

To create an Intelligent Search API middleware, you need to create a new VTEX IO app from the [`vtex.is-api-middleware-resolver`](https://github.com/vtex-apps/is-api-middleware-resolver) boilerplate and customize it to establish your own rules, according to the following steps:

1. Clone the `vtex.is-api-middleware-resolver` app into your machine:

```sh
git clone https://github.com/vtex-apps/is-api-middleware-resolver
```

2. Open the `vtex.is-api-middleware-resolver` project in any code editor of your preference.

3. Go to the `manifest.json` file and replace the `vendor` value with the name of your VTEX account.

4. Go to the `node/resolvers` folder and open the `before.ts` file.

5. Replace the `before` definition with your own rules. See the following example where we promote the product `123` if the query is `shoes`.

```ts
export default async function before(
  _: unknown,
  args: SearchParams,
  __: Context
): Promise<SearchParams> {
  if (args.query === "shoes") {
    const myDynamicRules: DynamicRule[] = [
      {
        action: "promote",
        type: "id",
        value: "123",
      },
    ];

    return { ...args, dynamicRules: myDynamicRules };
  }

  return args;
}
```

You can check the schema that the `before` expects on the [is-api-middleware-graphql](https://github.com/vtex-apps/is-api-middleware-graphql) repository.


6. Test your app by running the following query:

``` GraphQL
query before(
	$selectedFacets: [SelectedFacetInput]
    $query: String
    $page: Int
    $count: Int
    $sort: String
    $operator: Operator
    $fuzzy: String
    $allowRedirect: Boolean
    $regionId: String
    $simulationBehavior: SimulationBehavior
    $hideUnavailableItems: Boolean
    $dynamicRules: [DynamicRuleInput]
) {
  before(selectedFacets: $selectedFacets
    query: $query
		page: $page
		count: $count
		sort: $sort
		operator: $operator
		fuzzy: $fuzzy
		allowRedirect: $allowRedirect
		regionId: $regionId
		simulationBehavior: $simulationBehavior
		hideUnavailableItems: $hideUnavailableItems
		dynamicRules: $dynamicRules)
    @context(provider: "vtex.intelligent-search-api-middleware-graphql") {
		query
		page
		count
		sort
		operator
		fuzzy
		allowRedirect
		regionId
		simulationBehavior
		hideUnavailableItems
		dynamicRules {
			action
			type
			value
		}
  }
}
```

From now on, every time a user searches for `shoes`, the Intelligent Search will promote the product `123`.
