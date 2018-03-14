# sigV4Client
A standalone client for signing API Gateway requests for Signature Version 4. For more details follow the steps from this chapter in the [Serverless Stack tutorial](https://serverless-stack.com/chapters/connect-to-api-gateway-with-iam-auth.html).


### How to use

You need [crypto-js](https://github.com/brix/crypto-js) installed.

Copy [**`sigV4Client.js`**](https://raw.githubusercontent.com/AnomalyInnovations/sigV4Client/master/sigV4Client.js) to your project.


Create a new `sigV4Client` instance.

``` js
const signedRequest = sigV4Client
  .newClient({
    accessKey: AWS.config.credentials.accessKeyId,
    secretKey: AWS.config.credentials.secretAccessKey,
    sessionToken: AWS.config.credentials.sessionToken,
    region: YOUR_API_GATEWAY_REGION,
    endpoint: YOUR_API_GATEWAY_URL
  })
  .signRequest({
    method,
    path,
    headers,
    queryParams,
    body
  });
```

And make the request.

``` js
await fetch(signedRequest.url, {
  headers: signedRequest.headers,
  method,
  body
});
```
