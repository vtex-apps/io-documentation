# Policies

Policies are a set of permissions granted to a resource or a [role]() that allows or forbids them to execute a given set of actions in an account. In VTEX IO, policies are mostly based on [AWS's IAM policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html).

VTEX IO accepts two kinds of policies, which are role-based and resource-based. The former, as the name suggests, are policies associated with a role, such as an app. In this case, these policies must be declared in a `policies.json` file in the app's root folder. 

Resource-based policies, in turn, are policies assigned to a resource, such as an API endpoint. In this case, the resource itself may list who it trusts and provide information about the context in which it trusts those agents. Therefore, since the routes an app exports to the world are declared in a `service.json` file, so are the resource-based policies.

## Role-based policies

To create a role-based policy for an app, one may create a `policies.json` file in the app's root folder. The basic structure of this file is as the following:

```json
[
  {
    "name": "resolve-graphql",
    "description": "Allows access to resolve a graphql request",
    "statements": [
      {
        "effect": "allow",
        "actions": ["post", "get"],
        "resources": [
          "vrn:vtex.store-graphql:{{region}}:{{account}}:{{workspace}}:/_v/graphql"
        ]
      }
    ]
  }
]
```

Notice that, in this example, a policy named `resolve-graphql` that allows access to an app to resolve a GraphQL request was declared. 

Besides a `name` and a `description`, this policy contains the `statements` prop.

Statements are used in a way of stating: "**allow/do not allow** these **actions** to be performed on these **resources** under these **conditions**". 

Therefore, considering the given example, the declared `resolve-graphql` policy allows `POST` and `GET` requests to be performed on the `vrn:vtex.store-graphql:{{region}}:{{account}}:{{workspace}}:/_v/graphql` resource.

The keys that compose a statement are:

- `effect` - describes the effect of allowing (`allow`) or denying (`deny`) a resource to be accessed.
- `actions` - describes the actions related to a given effect and resource. 

> Depending on the resource, there may exist different actions one could perform on it. For RESTful APIs, this could map to HTTP verbs. However, actions are not restricted to it and the service may accept any string as an action.

- `resources` - contains the list of resources expressed by a [VTEX Resource Name (VRN)]() to which the statement refers to.

You can also optionally state `conditions` to designate that a given statement should only be considered if the context of the request satisfies the set of conditions that have been provided. 

Conditions are built with [condition operators](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html). In addition to it, `account` (tenant of the call), `workspace`, and `region` can also be used as `conditions` values.

## Resource-based policies

To create a resource-based policy, the resource itself must list who it trusts. Therefore, since the routes of a resource are declared in a `service.json` file, a *resource-based* policy must be declared in this file as a `routes` property.

One must have something similar to the following:

```json
{
    "routes": {
        "new-order": {
            "path": "/orders",
            "public": false,
            "policies": [{
                "effect": "allow",
                "actions": ["post"],
                "principals": [
                    "vrn:apps:*:*:*:app/example.marketplace@*"
                ]
            }]
        }
    }
}
```

Notice that, in this example, a resource-based policy related to the `/orders` route was declared. 
The `effect`, `actions` and `principals` props under `policies` can be translated as: "**allow/do not allow** these **actions** to be performed by these **principals** in this **route**", where principals can be understood as the applications able to make requests to a given resource.

Hence, for the given example, a policy related to the `/orders` resource allows the `example.marketplace` app to perform a `POST` request in its route.

The keys that compose this kind of policy are:

- `effect` - describes the effect of allowing (`allow`) or denying (`deny`) a principal to perform a set of actions on a route.
- `actions` - describes the actions related to a given effect, principal, and route. 
- `principals` - contains the list of principals able to perform requests to a given route or not. Like resources, `principals` are also expressed by a [VTEX Resource Name (VRN)]().
