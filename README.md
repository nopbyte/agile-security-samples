# Agile Security Examples

This repository contains a set of examples to interact with AGILE IDM (available here: https://github.com/Agile-IoT/agile-idm-web-ui).

AGILE IDM is an Oauth2 server that implements the following grant flows:

* authorization code: a web application obtains an authorization code after the user has logged in, and afterwards it executes calls (directly from server side) to exchange the authorization for an access token. In this flow, the browser does not access the access token, making it the most secure approach.
* implicit: a web application obtains the token after the user has logged in. In this case, the browser will obtain the token directly. In this case, the server neither requires to  execute server side code to exchange codes for tokens nor to execute server side code to authenticate itself. Although this approach can be easier to implement, there is an additional risk since the browser obtains the token.
* client credentials: this grant flow allows an application (without user interaction or web interface) to obtain an access token by providing the client id and its credentials.

The folders within this repository include several examples to illustrate applications using the different kind of authentication grants. Further, in the case of the authorization code grant, a complete application generating requests to AGILE IDM to register entities, groups, update attributes etc is also provided.


## Setup in Agile Security

Although there is no need to configure Agile security to execute the samples in this repository, we describe which configurations enable the tests to run.

Each kind of OAuth2 client requires different aspects. For example, Implicit authentication requires the client to register a callback but it does not require the client to provide its credentials. On the other hand, the client credentials flow requires a client to have a secret, but no callback, etc.

**These configurations must be updated when the security components are going to be used in production**





### Implicit

The implicit authentication enables applications that are not capable of generating server side requests to authenticate the client, to still rely on an identity provider.
A typical example of this, is a case in which an application that runs in a browser and executes JavaScript code. In this simplified authentication grant flow, the web browser
obtains a token directly from the authentication service through a redirection.

The key consideration when this authentication grant is used is that the browser obtains access to the token directly. On the contrary, in the authorization code flow, the browser only obtains an authorization code, which is normally useless unless the browser managed to obtain the secret of the client application (which should never be shared with the browser).

Agile security creates the following client during the first boot.

```
{  
  "id": "ImplicitAuthClient",
  "name": "ImplicitAuthClient",
  "redirectURI": "http://localhost:2000/"
}
```

This information is used in the implicit html file to obtain the user's token.

**note**: that this callback is different than the authorization code. It returns directly to a URL that servers HTML to the browser. In the case of an authorization code flow, this URL needs to redirect to an endpoint in the server that is capable of exchanging the authorization code for a valid access token after presenting the client credentials. In this case, the browser will get the access token directly after following the redirection to http://localhost:3010/index.html, therefore removing the burden on the server side to exchange the token. However, the browser (and the client side JavaScript code) needs to be trusted, otherwise this mechanism should not be used.
