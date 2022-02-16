---
title: How to create and use Clients on VTEX IO?
description: "Understand what are clients used for on VTEX IO platform and learn how to create custom clients for your specific requirements"
date: "2020-04-28"
tags: ["clients", "services", "development", "api", "external", "node"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/new-docs-and-fix/docs/en/Recipes/development/how-to-create-and-use-clients.md"
---

# Managing Clients

In this guide, you will learn how to create [clients](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-clients) and how to use them in your implementations. 

## Before you start
- Being familiar with the [concept of Clients](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-clients)

So, what to do with *clients*? You **create them**, extending some base code. IO Node Services already ship with some **default clients**, mostly to our internal services, that you may use right away. Check them [here](https://github.com/vtex/node-vtex-api/blob/ccf4d8f8d3208007c4bfd558baf979df8d825af8/src/clients/IOClients.ts).

Before talking about *how we create clients*, let's *recap* how we use them. If you are familiar with IO services, you already know that your implementation **exports functions** that receive a ***context*** object. These functions can be a **resolver function to a GraphQL field**, a **middleware to an HTTP server** or an **event handler**, and, in all of them, you receive a `ctx`_(or however you wanna call it)_  object of type [`Context`](https://github.com/vtex/node-vtex-api/blob/master/src/service/worker/runtime/typings.ts), and it is inside of `ctx.clients` where you'll find each client.

```typescript
export const authorize = async (ctx: Context) {
	const { clients: { licenseManager } } = ctx
	...
	const data = await licenseManager.canAccessResource(/*...*/)
}
```

## Creating clients

1. The [`@vtex/api`](https://github.com/vtex/node-vtex-api/) SDK provides a structured way to create clients, and the first thing to do is **identify the type of communication you want to implement.** As of now, we support these out of the box:

| Type | Use case |
|--|--|
| `AppClient` | Communication with other IO Services via *plain-old* HTTP calls |
| `AppGraphQLClient` | Communication with other IO GraphQL services |
| `ExternalClient` | Communication with external API's |
| `JanusClient` | Communication with VTEX Core Commerce API's through Janus Router |
| `InfraClient` | Communication with VTEX IO Infra services |

> ⚠️
> 
> When using clients, do not forget to add the **appropriate policies** on your `manifest.json`. Incorrect policies may result in request blocking.

2. After finding the *base* client you are looking for, you need to implement a **Typescript class that extends the type of this base client**. You may place them wherever you want, but we advise you to put them on `node/clients`.

Let's take a look on the anatomy of an *ExternalClient* to the *Github API*:

`node/clients/github.ts`
![Github API Client example](https://i.imgur.com/rcSivwD.png)

**Reference** 
1 - Look, it's one of the types from the **table above**.

2 - Take a look [here](https://github.com/vtex/node-vtex-api/blob/4f17dba5d750dae6603c606187c888fbd91fd18c/src/HttpClient/typings.ts#L58) to check everything you can configure.

3 - Read more about **app's pricing** [here](https://help.vtex.com/tutorial/app-pricing-options--2ZKBKxLe08Q6seA6sCi6o2).

4 - There are a lot of other methods available, you can check them on [**HttpClient**].(https://github.com/vtex/node-vtex-api/blob/master/src/HttpClient/HttpClient.ts)

> ⚠️
> 
> You're free to add data handling logic inside your client's methods (*i.e:* mapping fields, or filtering data), but be careful to not lose track of the client's responsabilities.

## Using clients on implementations

After you've learned how to create **great clients**, it's time to **ship them**, so you may **use it on your implementations**. It's easy as well!

> ℹ️
> 
> If you want to jump to an example, check how the *StatusClient* is setup on [service-example](https://github.com/vtex-apps/service-example).

**Let's suppose you've created the Github client** we've described above!
 
1. Make sure you've **exported** the *client* from its module. _(Either [default or named export](https://medium.com/@etherealm/named-export-vs-default-export-in-es6-affb483a0910))_
2. Create a `node/clients/index.ts` file.
3. Paste the following snippet on it. _(If you've used named export on Step 2, change the import clause)_
```typescript
import { IOClients } from '@vtex/api'
import GithubClient from './github.ts'

export class Clients extends IOClients {
  public get status() {
    return this.getOrSet('github', GithubClient)
  }
}
```
4. Now, **import the Clients class** on `node/index.ts` (the service *entrypoint*).
5. Create or edit a `clients` object of type `ClientsConfig<Clients>` _(from @vtex/api)_ like so:
```typescript
	const clients: ClientsConfig<Clients> = {
	  implementation: Clients,
	  options: {
	    default: {
	      retries: 2,
	      timeout: 2000,
	    },
	  },
	}
```
6. Use the `clients` variable on the **Service** exported:
```typescript
export default new Service<Clients, State>({
  clients,
  routes: {
    ...
  },
})
```
7. **Optional:** Place this **type declaration** on the same `node/index.ts` file. It helps you type the implementation functions.
```typescript
declare global {
  type Context = ServiceContext<Clients, State>
}
```
8. **That's it** :sparkles:! Now you can, on your functions, **access your client** from the `ctx`. 
```typescript 
export const authorize = async (ctx: Context) {
	const { clients: { github } } = ctx
	...
	const data = await github.getUser(/*...*/)
}
```

## Want to dive deeper?

If you didn't find what you were looking for here, try **learning by example**. We are already doing some advanced thing on our default clients, like **file upload**, **use of disk cache** and more:
 - [AppsClient](https://github.com/vtex/node-vtex-api/blob/master/src/clients/infra/Apps.ts)
