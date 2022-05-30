# Managing application logs

VTEX IO provides a logging service that allows developers to keep track of errors, warnings, and informative events within an application. The VTEX IO Logging Service collects data from the cloud infrastructure where VTEX applications run and delivers them via the VTEX IO CLI.

In the following section, you'll learn how to implement the VTEX IO Logging Service in your apps and how to retrieve their logs.

>ℹ️ The VTEX IO Logging Service is currently available for Node apps only.

---

## Before you start

To complete this guide, you must have the VTEX IO CLI installed in your machine. For more information, please refer to [this document](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-install).

---

# Step by step

## Implementing the VTEX IO Logging Service

1. Open your Node app in any code editor of your preference.
2. Define an object with the `Context` interface as a parameter of a function you wish to provide logging messages. Take the following example:

```js
const helloWorld = (Context: ctx) => {
  const { vtex: { logger } } = ctx

  logger.info('Hello World!')
}
```

In this example, the `helloWorld` function receives an object with a [**Context**](https://github.com/vtex/node-vtex-api/blob/master/src/service/worker/runtime/typings.ts#L34) interface as a parameter. 

>ℹ️ The `Context` interface contains many implementations inherent to the VTEX IO platform. One of those implementations is called `vtex` - an object containing all [VTEX IO infrastructure](https://github.com/vtex/node-vtex-api/blob/master/src/service/worker/runtime/typings.ts#L116) related metadata, such as `account`, `workspace`, `tenant`, `settings`, and some service implementations. In the previous example, we used the `logger` service, which is an implementation inside `vtex` responsible for generating log messages.

3. [Destructure](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#destructuring) the `logger` object from the `vtex` context and use its methods (i.e., `error`, `warn`, `info`, and `debug`) to provide error, warning, debugging, or informative messages in the log. Take the following example:

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

Every log written by a running application with the VTEX IO logging service is collected and stored for 7 days. These logs can be retrieved by the [VTEX IO CLI](https://developers.vtex.com/vtex-developer-docs/docs/vtex-io-documentation-vtex-io-cli-installation-and-command-reference) as in the following:

1. Log in to your VTEX account.
2. Install the Logs plugin for the VTEX IO CLI by running the following command:

```
vtex plugins add logs
```

3. Check if the installation of the Logs plugin was successful by running `vtex logs --help`.
4. Retrieve logs from all apps installed in your account by running the following command:

```
vtex logs --all
```

As an output, you should see a message similar to the following:

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

>ℹ️ You can also retrieve logs from a specific app installed in your account by running the following command: `vtex logs {account}.{serviceAppExample}`. Remeber to replace `account` with your account name and `serviceAppExample` with the desired app name.


We suggest running `vtex logs --all > {mylogfile.logs}` to save the log messages in a local file. Replace `{mylogfile.logs}` with the most suitable name for you. 

Also, if you want to see log messages that you have previously retrieved, run `vtex logs --past`.
