# Managing application logs

Being aware of what happens inside an application is important for debugging. Therefore, application logs are used by developers to keep track of errors, warnings, and informative events. 

To this end, VTEX IO offers a logging service to facilitate the process of developing and debugging an application on the platform. 

VTEX IO logging service collects information from the cloud infrastructure, where VTEX applications run, and provides the applications' logs through VTEX IO CLI - our CLI. 

The following step-by-step shows how to implement VTEX IO logging service in your applications and how to retrieve the logs these apps produce.

# Step by step

## Implementing VTEX IO Logging Service

>ℹ️ The VTEX IO Logging Service was designed for node applications and is not yet available for other applications on the platform.

Assuming that you are familiar with how a service node function is implemented on the VTEX IO platform, consider the example below: 

```js
const helloWorld = (Context: ctx) => {
  const { vtex: { logger } } = ctx

  logger.info('Hello World!')
}
```
In this example, our `helloWorld` function receives as a parameter an object with a [**Context**](https://github.com/vtex/node-vtex-api/blob/master/src/service/worker/runtime/typings.ts#L34) interface, which contains many implementations inherent to the platform. 

One of those implementations is called `vtex` - an object containing all [VTEX IO infrastructure](https://github.com/vtex/node-vtex-api/blob/master/src/service/worker/runtime/typings.ts#L116) related metadata, such as `account`, `workspace`, `tenant`, `settings`, and some service implementations. In this case, we used the `logger` service, which is an implementation inside `vtex` responsible for generating log messages.

After declaring the function, the `logger` object is [destructured](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#destructuring) from the `vtex` context and, in the sequence, `logger.info` is called to save the informational `Hello World!` message in the log. 

The Logging Service also supports the `warn`,  `error`, and `debug` methods, having different levels that can be used to filter your application logs. For example:

```js
  const helloWorld = (Context: ctx) => {
  const { vtex: { logger } } = ctx

  logger.warn('Warning the world!')

  logger.error('Error!!!')

  logger.debug('Verbose debug message!')
}
```

>ℹ️ Every exception that happens inside a VTEX IO service application is intercepted and automatically logged with a `logger.error` implementation.

## Retrieving application logs

Every log written by a running application with our logger implementation is collected and stored for 7 days. Those logs can be retrieved by the [VTEX CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference).

Using VTEX IO's CLI:
1. Log in to your VTEX account;
2. Run the command `vtex logs --all` to retrieve logs from every application installed in your account. 

>ℹ️ We suggest running `vtex logs --all > {mylogfile.logs}` to save the log messages in a local file. Remember to replace `{mylogfile.logs}` with the most suitable name for you.

```
vtex logs --all
18:15:26.779 - info: Connecting to logs stream for store components
18:15:26.782 - info: Press CTRL+C to abort

18:15:43.856 - info: Listening to store components logs

  info: { status: 403,
  code: 'FORBIDDEN',
  name: 'ForbiddenError',
  level: 'error',
  message: 'This username is already registered with another email',
  stack:
   'ForbiddenError: This username is already registered with another email[ErrorStack...]
  routeId: 'login' }
  ```
To retrieve logs from a specific application, use the command  `vtex logs {account}.{serviceAppExample}`, replacing `account` with your account name and `serviceAppExample` with the specific application name.

>ℹ️ If you want to see log messages that you have previously retrieved, run `vtex logs --past`. You can run `vtex logs --help` to check out other log commands.
