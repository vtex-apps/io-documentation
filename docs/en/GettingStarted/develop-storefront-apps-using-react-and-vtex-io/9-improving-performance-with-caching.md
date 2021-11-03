# 8. Improving performance with caching
 
Repeated searches for similar data can become an expensive and frustrating investment as they require a high number of responses from the server to deliver the requested information. 
 
That is why the **ability to use *cache* and reuse data previously obtained on the server can be a critical point for optimizing your front app's performance and, consequently, your website**.
 
The VTEX IO development platform already applies advanced *cache* techniques to the [Store Framework](https://developers.vtex.com/vtex-developer-docs/docs/getting-started-3) using the Apollo *cache* as a search and data management solution capable of interacting with VTEX's GraphQL services.
 
We highly recommended using the [Apollo solution](https://www.apollographql.com/docs/react/caching/cache-configuration/) in your app and, that way, define your own *cache* strategies that mold to the business scenario that applies to your store. 
 
![React Apollo overview](https://miro.medium.com/max/1400/1*Akd1I7jc0teE_mz15fnZog.jpeg)
 
Once implemented, the solution operates without major configurations: two GraphQL *requests* with the same *query* and variables reach the server only once for data collection.
 
You can read about [Apollo usage rules and policies](https://medium.com/@galen.corey/understanding-apollo-fetch-policies-705b5ad71980) to understand more about possible data collection scenarios using this solution.
 
For example, if you use the `cache-and-network` rule, you will be able to immediately return the requested data if it is *cached* and still query the server to confirm if any data has been changed since then.
 
