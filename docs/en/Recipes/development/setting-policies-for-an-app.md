# Setting policies for an app

[Policies]() are permissions granted to a VTEX IO app that allows it to execute a given set of actions once installed in an account.

The next section presents a step by step on how to declare the permissions your app may need.

## Step by step

1. Open your app directory in your code editor.
2. Open the `manifest.json` file and, **according to your scenario**, check the "Referencing a policy" or "Referencing a set of policies" section to declare the policies your app may need.
3. Save your changes.

### Referencing a policy

For each policy, one must declare:

- a `name`, which is a unique identifier of a given policy.
- a `reason`, which may briefly describe the policy.

>:warning: **Keep in mind:** The `reason` may aid the person who wants to install the app in taking the decision of installing it or not.

- `attrs` (optional), which may contain the `host` and the `path` of a service's URL that needs to be called.

Take the following example:

```json
"policies": [
    {
        "name": "example-read-write",
        "reason": "Store the zip code of the user."
    },
    {
        "name": "outbound-access",
        "reason": "Automatically compute shipping prices for a logged user who gave us their zip code.",
        "attrs": {
            "host": "{example}.com",
            "path": "/api/logistics/shipping"
        }
    }
]
```

Notice that, in this example, two policies were declared:

- `example-read-write`, which stores the zip code of a user.
- `outbound-access`, which automatically computes shipping prices for a logged user who provided his zip code. Note that, in this case, attributes such as `host` and `path` are necessary to communicate with a specific logistics service.

### Referencing a set of policies

We also allow an app to export a `policies.json` file, containing a given set of policies. To reference one of those in your app manifest, you may set the `name` value as the app name that declared the `policies.json` followed by the policy name, as in `{account}.{app-name}@{version}:{policy-name}`.

Check the example below:

```json
"policies": [
    { "name": "vtex.app-name:catalog-proxy" }
]
```

Notice that `catalog-proxy` is the `name` of a policy previously declared in a `policies.json` file of the `app-name` app.

## Modus Operandis

Once you performed the desired changes in the `policies` of your app's `manifest.json` file, a set of permissions will be granted to your app. 

Therefore, the act of installing your app may consider the acceptance of those permissions.
