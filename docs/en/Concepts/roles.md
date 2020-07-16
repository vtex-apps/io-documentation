# Roles

Roles are uniquely identifiable names given to request sources. 

Whenever a request is performed in the VTEX IO platform, the source of this action, which can be the user or app responsible for performing that request, automatically receives a unique role.

In the sequence, to detect whether or not the request source is authorized to perform that particular request, and also to determine if the call can go through, VTEX IO platform checks if the source role contains the required policies attached.
Since the same user can have different permissions within the same account, each role can have multiple policies attached.

A role can be given to a user or an app. The general rule is to have an identity provider, such as `user`, `app`, or `link`, followed by an identity.

For example: an user making a request would receive a role similar to `user:f1sd8705-b34f-48ff-a113-2b8bb8c22411`, or `user:<e-mail>`. Installed and linked apps, in turn, would receive roles as `app:vtex.auth-server@1.0.0` and `link:vtex.auth-server@1.0.0`.
