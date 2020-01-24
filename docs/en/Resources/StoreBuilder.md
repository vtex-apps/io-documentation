# Store/Pages Builders

This is a quick overview on how the Store/Pages builder that powers Store Framework works.

Be sure to have the source-code for both builders at hand while reading this, since there will be several references to it along this document.

## Where to begin

OK, so what is the entrypoint to the Store builder? Where does it all begin? What code gets executed when I link an app that uses it? Well, simple enough, the entrypoint can be found at `/node/build/store/index.ts`. This is the code that gets executed when you start the Store build process.

asjbnxkjasnxHere is a quick overview of this file:

1. Constants for dependencies that will be added to the manifest of the app being built, in build-time, and the default `FILE_PATHS` for the files that will be picked up by the builder.
2. A `success` function which will be executed by the builder after the build process is done and everything went well. 
3. The `addDependencies` function is executed right before the actual build and appends the dependencies from the `DEPENDENCIES` constant into the app's manifest.
4. Then comes the actual build function `createBuildSteps(FILE_PATHS)` . Notice that `createBuildSteps` is imported from `pages/1.x`. This is the function that does all the work, we'll take a look at it in a bit.
5. Finally, a new `Builder` is exported. This is done by every single builder, and basically exports the configuration for the Store builder. Notice that the first configuration parameter is `build`, where the result from the call to `createBuildSteps` is passed.

So that's all there is to the entrypoint file in the Store builder! But there is a lot happening in this line: `const build = createBuildSteps(FILE_PATHS)`, and to understand it we need to take a look at the Pages builder.

## Pages builder

The `createBuildSteps` function imported by Store builder lifes at: `node/build/pages/1.x/index.ts`. This file has a few more functions and we're looking into them as necessary. Let's go straight to `createBuildSteps`. This functions is responsible for defining each step in the build process that handles the files inside `/store`. When it is done, it returns an array of functions, where each of of them is a build step.

### createBuildSteps

This functions is responsible for defining each step in the build process that handles the files inside `/store`. When it is done, it returns an array of functions, where each of of them is a build step.

#### createParseFiles

The first step is `createParseFiles`. In this step, we use the current `appId` and `paths` from the build context (`ctx`) . The `paths` gives us access to the files being sent to Builder Hub, as raw text files. Next, we use these variables to instanciate a new `DependencyManager` for this `rawPagesContext` and sets a `files` attribute that is created by a call to `getFiles`, which is a function responsible for traversing the `/store` directory, assembling the `blocks.json` file (basically merging all files inside of the `/store/blocks` directory into a single file), and also using the parsers exported by `node/build/pages/1.x/parser.ts` to parse all files and finally returning an Object of type `RawPagesFiles`, which looks like this:

```typescript
// Type definitions for each field can be found at
// node/build/pages/1.x/parser.ts
export interface RawPagesFiles {
  blocks: RawBlocks
  plugins: RawPlugins
  interfaces: RawInterfaces
  routes: RawRoutes
  contentSchemas: JSONSchema6
}
```

So after this step, our `instanceCtx` has atributes `dependencyManager` (more on that later) and `files`. We then return the build context. This `instanceCtx` will be used in the final step to assemble the build result files, that are read by Builder Hub and Pages GraphQL.

#### resolve

In this step we use the `dependencyManager` and the `files` from the previous step to create a new `Resolver`, which is used to populate the `pages` attribute in `instanceCtx`. We'll take a deeper look into `Resolver` later on.

Next, we update the routes defined in the current build context and add a new `contentTypes` attribute to `instanceCtx`, which is used by `vtex.rewriter`.

#### maybeAppendDependency

This step checks for routes defined by the current app being built, and if it does define routes, we add `'vtex.render-server': '8.x',` to its dependencies. If no routes are defined by the app, this step does nothing.

#### writeAssets

This is the last step in the build process. In `writeAssets`, we use the current `instanceCtx`, which has been assembled in the previous steps to create the final build result files that will be sent to the `/dist` directory in the registry. These files (and their content) are:

- `dist/vtex.builder-hub/build.json` - which contains `pages.build`
- `dist/vtex.pages-graphql/blocks.json` - which contains `pages.blocks`
- `dist/vtex.pages-graphql/routes.json` - which contains `pages.routes`
- `dist/vtex.pages-graphql/plugins.json` - which contains `pages.plugins`
- `dist/vtex.pages-graphql/interfaces.json` - which contains `pages.interfaces`
- `dist/vtex.pages-graphql/contentSchema.json` - which contains `pages.contentSchema`
- `dist/vtex.rewriter/build.json` - which contains `instanceCtx.contentTypes`

Notice the repositories each of these files are being saved to. Each app in IO has permission to access the files of another app in the registry if the name of the requestor app matches the directory it is trying to access. In this case, every file that is generated by the builder and put into `dist/pages-graphql` can be accessed by `pages-graphql`.

### DependencyManager

The `DependencyManager` is the module responsive for analysing 

