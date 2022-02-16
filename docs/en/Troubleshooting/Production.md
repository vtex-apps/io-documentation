## My store translation is not behaving as expected

<details>
<summary>My store is being translated when it shouldn't</summary>

### Checking the default locale

Access the API `http://portal.vtexcommercestable.com.br/api/tenant/tenants?q={account}` and check the `defaultLocale` file.

>⚠️ Remember to replace the value between curly brackets with your VTEX account name.

If the `defaultLocale` value doesn't agree with your store locale, please [open a support ticket](https://help-tickets.vtex.com/smartlink/sso/login/zendesk) notifying this issue.
</details>

## My routes are not behaving as expected

<details>
<summary>My redirect path doesn't work</summary>

### Checking if the redirect is saved in the Rewriter

1. Using the terminal and the VTEX IO CLI, run `vtex install vtex.admin-graphql-ide@3.x` to install the GraphiQL IDE in your account.
2.  Access the GraphiQL IDE through your account admin.
3. From the dropdown list, choose the `vtex.rewriter@1.x` app.
4. Run the following query, replacing `{URL}` with the `from` path you're having trouble with:

```gql
{
   redirect {
     get(path: "/{URL}") {
        from
        to
     }
   }
}
```

The expected answer is a JSON object containing all the redirects related to that path. Take the following example:

```json
{
  "data": {
    "redirect": {
      "get": {
        "from": "/about-us",
        "to": "/my-store"
      }
    }
  }
}
``` 

#### If the query doesn't return the redirect path

Open your account admin and go to *Store Setup > CMS > Pages > Redirects*. Then, save the desired URL redirects.

>ℹ️ For more information, check our doc on [managing URL redirects.](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-managing-url-redirects/)

#### If the query returns the redirect path

Check if your store theme, or some other app, defined a route with the same path you're trying to save your redirect.

If this route is already declared, the redirect will be ignored.
</details>

## My store is presenting inconsistencies

<details>
<summary>Product price is different on Search Results and Product Detail pages</summary>

>ℹ️ The Search Results and Product Details pages have different indexing processes. This can lead to differences in the price.

1. [Reindex](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-understanding-how-store-url-indexing-works) the products presenting inconsistencies.

2. Check out the value declared for the [Search Result](https://developers.vtex.com/vtex-developer-docs/docs/vtex-search-result)'s `simulationBehavior` prop. If set as `skip`, change it to `default`.

>ℹ️ When the `simulationBehavior` is set as `skip`, the Search Results page displays the cold price based on the user cache. In order to fetch and display the latest price registered in the catalog, change it to `default`.
</details>