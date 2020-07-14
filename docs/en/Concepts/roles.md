# Roles

Roles are uniquely identifiable names given to the actors of a request. This means that, in VTEX IO, whenever a request is performed, the actor of this action receives a role. In the sequence, to determine whether or not that call can go through, the role is translated into a set of policies.

Since the same user can have different permissions within the same account, each role can have multiple policies attached.

A role can be given to a user or an app. The general rule is to have an identity provider, such as `user`, `app`, or `link`, followed by an identity.

For example: an user making a request would receive a role similar to `user:f1sd8705-b34f-48ff-a113-2b8bb8c22411`, or `user:<e-mail>`. Installed and linked apps, in turn, would receive roles as `app:vtex.auth-server@1.0.0` and `link:vtex.auth-server@1.0.0`.
