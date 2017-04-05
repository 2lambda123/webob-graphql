# WebOb-GraphQL

[![Build Status](https://travis-ci.org/graphql-python/webob-graphql.svg?branch=master)](https://travis-ci.org/graphql-python/webob-graphql) [![Coverage Status](https://coveralls.io/repos/graphql-python/webob-graphql/badge.svg?branch=master&service=github)](https://coveralls.io/github/graphql-python/webob-graphql?branch=master) [![PyPI version](https://badge.fury.io/py/webob-graphql.svg)](https://badge.fury.io/py/webob-graphql)

Adds GraphQL support to your WebOb application.

## Usage

Just use the `serve_graphql_request` function from `webob_graphql`


### Pyramid

```python
from pyramid.view import view_config

from webob_graphql import serve_graphql_request


@view_config(
    route_name='graphql',
    # The serve_graphql_request method will detect what's the best renderer
    # to use, so it will do the json render automatically.
    # In summary, don't use the renderer='json' here :)
)
def graphql_view(request):
    return serve_graphql_request(request, schema)

	# Optional, for adding batch query support (used in Apollo-Client)
    return serve_graphql_request(request, schema, batch_enabled=True)
```

### Supported options
 * `schema`: The `GraphQLSchema` object that you want the view to execute when it gets a valid request.
 * `context`: A value to pass as the `context` to the `graphql()` function.
 * `root_value`: The `root_value` you want to provide to `executor.execute`.
 * `format_error`: If you want to use a custom error formatter.
 * `pretty`: Whether or not you want the response to be pretty printed JSON.
 * `executor`: The `Executor` that you want to use to execute queries.
 * `graphiql_enabled`: If `True` (default), may present [GraphiQL](https://github.com/graphql/graphiql) when loaded directly from a browser (a useful tool for debugging and exploration).
 * `render_graphiql`: A custom function for rendering GraphiQL (this function should have the arguments `result` and `params`).
 * `batch_enabled`: Enable batch support (for using in [Apollo-Client](http://dev.apollodata.com/core/network.html#query-batching) or [ReactRelayNetworkLayer](https://github.com/nodkz/react-relay-network-layer))
