GraphQL HTTP Server Middleware
==============================

This is the same as express-graphql, except it accepts an option for specifying
which domain to host the static resources of GraphiQL, so that it could be rendered
in an offline environment.

## Installation

```sh
yarn add express-graphql-offline
```


## Simple Setup

Just mount `express-graphql` as a route handler:

```js
const express = require('express');
const graphqlHTTP = require('express-graphql');

const app = express();

app.use('/graphql', graphqlHTTP({
  schema: MyGraphQLSchema,
  graphiql: true,
  graphiqlCDN: '127.0.0.1:8080'
}));

app.listen(4000);
```

## Options

The `graphqlHTTP` function accepts the following options:

  * **`schema`**: A `GraphQLSchema` instance from [`GraphQL.js`][].
    A `schema` *must* be provided.

  * **`graphiql`**: If `true`, presents [GraphiQL][] when the GraphQL endpoint is
    loaded in a browser. We recommend that you set
    `graphiql` to `true` when your app is in development, because it's
    quite useful. You may or may not want it in production.

  * **`graphiqlCDN`**: Specify the cdn domain of the static assets. Default domain is `cdn.jsdelivr.net`.

  * **`rootValue`**: A value to pass as the `rootValue` to the `graphql()`
    function from [`GraphQL.js/src/execute.js`](https://github.com/graphql/graphql-js/blob/master/src/execution/execute.js#L119).

  * **`context`**: A value to pass as the `context` to the `graphql()`
    function from [`GraphQL.js/src/execute.js`](https://github.com/graphql/graphql-js/blob/master/src/execution/execute.js#L120). If `context` is not provided, the
    `request` object is passed as the context.

  * **`pretty`**: If `true`, any JSON response will be pretty-printed.

  * **`formatError`**: An optional function which will be used to format any
    errors produced by fulfilling a GraphQL operation. If no function is
    provided, GraphQL's default spec-compliant [`formatError`][] function will be used.

  * **`extensions`**: An optional function for adding additional metadata to the
    GraphQL response as a key-value object. The result will be added to
    `"extensions"` field in the resulting JSON. This is often a useful place to
    add development time metadata such as the runtime of a query or the amount
    of resources consumed. This may be an async function. The function is
    given one object as an argument: `{ document, variables, operationName, result, context }`.

  * **`validationRules`**: Optional additional validation rules queries must
    satisfy in addition to those defined by the GraphQL spec.
