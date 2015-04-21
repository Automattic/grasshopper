# grasshopper

## A WordPress.com REST API + D3.js example

This is a simple demo app that uses the <a href="https://developer.wordpress.com/docs/api/">WordPress.com REST API</a> to graph a site's recent views using <a href="d3js.org">D3.js</a> / <a href="c3js.org">C3.js</a>.

See it in action <a href="https://automattic.github.io/grasshopper/">here</a>!

![Screenshot](https://cldup.com/tnTXMsmCCA.png)

### Authentication

The app uses <a href="https://developer.wordpress.com/docs/rest-api-javascript/">implicit oAuth</a> to retrieve a token via the oAuth flow without having to store a secret.

This token is returned in the URL when the oAuth flow redirects back to our app. Since we've requested scope for a single site, the Site ID is also returned as a URL parameter.

### Loading Data

Using the `d3.json()` function, we can use the token to make an authenticated request to the <a href="https://developer.wordpress.com/docs/api/1.1/get/sites/%24site/stats/">/stats</a> endpoint of the REST API.

The token is passed in an Authorization header:

```.header( 'Authorization', 'BEARER ' + decodeURIComponent( token ) )```

### Graphing The Data

Once the API call returns, we simply pass the returned data to `c3.generate()` to plot it on a graph.
