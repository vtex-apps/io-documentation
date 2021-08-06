# Roles

Roles are uniquely identifiable names given to request sources. 

Whenever a request is performed in the VTEX IO platform, the source of this action, which can be the user or app responsible for performing that request, automatically receives a unique role.

In the sequence, to detect whether or not the request source is authorized to perform that particular request, and also to determine if the call can go through, VTEX IO platform checks if the source role contains the required policies attached.

>ℹ️ As a single request source can have different permissions within the same account, each role can also have multiple policies attached to it.

Since apps and users are able to perform a request on the platform, both of them mandatorily receive roles. However, notice the following: app and user roles are structured in different formats.

For example: an user making a request would receive a role similar to `user:f1sd8705-b34f-48ff-a113-2b8bb8c22411`, or `user:<e-mail>`. Installed and linked apps, in turn, would receive roles as `app:vtex.auth-server@1.0.0` and `link:vtex.auth-server@1.0.0`.
