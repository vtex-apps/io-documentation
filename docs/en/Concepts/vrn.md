# VTEX Resource Name (VRN)

A VTEX Resource Name (VRN) is how the VTEX IO platform expresses the resource path called in a request. 

A resource can be accessed by sending a request to its Uniform Resource Locator (URL). However, the resource concept is broad, and, to name a few, a resource can be a proxy, an API segment, an app endpoint, etc. 

Therefore, in VTEX IO, we identify and express a resource by using a VRN, which structure carries essential information about the resource itself and the context in which it is being accessed.

The format of a VRN is `vrn:{service}:{region}:{account}:{workspace}:{path}` whose elements can be described as:

- `service` - the infrastructure service that holds the app's information.
- `region` - the region from where the request was performed.
- `account` - the VTEX account responsible for performing the request.
- `workspace` - the workspace used to perform a request.
- `path` - the specific endpoint of a request.

Example of real VRNs are:

- For a VTEX IO app: `vrn:apps:aws-us-east-1:vtex:example:/v2/apps`

- For an external service: `vrn:proxy:aws-us-east-1:vtex:example:api.visa.com/merchantlocator/v1/locator`

Notice that for services outside VTEX IO, the full URL must be provided and that the `service` is simply `proxy`.

<div class="alert alert-warning">
As in <code>vrn:apps:aws-us-east-1:vtex:example:/v2/apps/*</code>, a VRN may contain wildcards (<code>*</code>) to represent <strong>any</strong> value or variable. However, for security reasons, the wildcard is <strong>NOT</strong> allowed to replace the tenant of the request.
</div>
