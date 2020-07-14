# VTEX Resource Name (VRN)

In VTEX IO, a VTEX Resource Name (VRN) is how we express a resource path.

Most of the time, a resource is simply the URL that is being called. However, this concept is broad, and, to name a few, a resource can be a proxy, an API segment, an app endpoint, etc. That's why, to make it more tangible, in VTEX IO, we express a resource by a VRN, which structure carries information about the resource itself and the context in which it is being accessed.

The format of a VRN is:

`vrn:{service}:{region}:{account}:{workspace}:{path}`

Which elements can be described as:

- `service` - the infrastructure service that holds the app's information.
- `region` - the region where the request was performed.
- `account` - the tenant account.
- `workspace` - the workspace used to perform a request.
- `path` - the specific endpoint of a request.

Example of real VRNs are:

- For a VTEX IO app: `vrn:apps:aws-us-east-1:vtex:example:/v2/apps`

- For an external service: `vrn:proxy:aws-us-east-1:vtex:example:api.visa.com/merchantlocator/v1/locator`

Notice that for services outside VTEX IO, the full URL must be provided and that the `service` is simply `proxy`.

<div class="alert alert-warning">
As in <code>vrn:apps:aws-us-east-1:vtex:example:/v2/apps/*</code>, a VRN may contain wildcards (<code>*</code>) to represent <strong>any</strong> value or variable. However, for security reasons, the wildcard is <strong>NOT</strong> allowed to replace the tenant of the request.
</div>
