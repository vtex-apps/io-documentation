# Support apps

A Support app enables app developers to support users having trouble with an app functionality. It behaves as a **client support tool** and must be related to a regular app or service. 

Once installed in a VTEX account, these apps empower pre-defined groups of users with specific [roles](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-roles/) to securely log in, use, and perform a different set of actions related to that role.

Hence, if you're a developer, by publishing a support app with the adequate [policies](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-policies/), you can give support to your app users through the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) and help them hand-in-hand on their own workspace.

A Support app may always include a `support.json` file, designating the accesses a role will have in the VTEX account that installed the main app.

Check the following example of what a `support.json` file looks like:

```json
{
    "Support Agent": [
        { "name": "admin-read-only" }
    ],

    "App Developer": [
        { "name": "admin-read-only" },
        { "name": "oms-read-only" },
        { "name": "read-oms-logs" },
        {
            "name": "link-app",
            "attrs": { "appName": "vendor.appName" }
        }
    ]
}
```

Notice that the `support.json` file indicates the list of policies attached to a given role. 

In this example, `Support Agent` is a role that is given to the users who do the basic troubleshooting when a problem is reported. However, according to the attached policies, if the `Support Agent` cannot solve the problem, the `App Developer` can enter the account, link apps, add loggings and try to reproduce a bug.
