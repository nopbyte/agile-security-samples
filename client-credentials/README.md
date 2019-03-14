# Client Credentials sample

## Overview

Assuming that an oauth2 client has been registered in AGILE IDM, the flow to obtain an access token for the client using the client credentials flow is depicted in the following picture.

<table align="center">
	<tr>
		<td><img src="images/tutorial-example-client-cred.jpg" /></td>
	</tr>
	<tr align="center">
		<td>
			AGILE IDM grant with client credentials grant
		</td>
	</tr>
</table>


1. the client calls AGILE IDM, and provides the credentials using the HTTP Basic authentication protocol, and specifying the client credential grant type. Afterwards AGILE IDM delivers an access token to the application, in case it has provided the proper credentials.

From this point on, the application can use this token to interact with IDM, or with any other AGILE component that has been integrated with AGILE IDM.

## Authenticating with the Client Application

We have included a basic comman line  application that authenticates the client, and afterwards queries the client information as well as the user information.
In  case of the client credentials flow the owner of the client is represented as the user authenticated.

The sample application can be executed from a terminal to authenticate the client we just created like this:

```
node authenticateClient.js  --client ClientCredentialsClient  --secret Ultrasecretstuff
```

It is also possible to execute the authentication script providing additional arguments such as protocol, port, and host like this:

```
node authenticateClient.js  --client ClientCredentialsClient  --secret Ultrasecretstuff --host 127.0.0.1 --protocol http -- port 3000
```

## CURL

Alternatively one could authenticate a client using tools to generate http requests such as curl.

```
curl  -X POST -u ClientCredentialsClient:Ultrasecretstuff -d grant_type=client_credentials http://localhost:3000/oauth2/token
```

The previous command line call would use the proper HTTP Basic authentication mechanism to authenticate the client to AGILE IDM (assuming it is running in localhost in port 3000). The expected result looks like the following:

```
{
  "access_token":"1A9HeY99gSYTA2o0MxIhi8pM0UVG ... rWXvrc9nqSdlj1vsEQE3INQyR0bRODEl",
  "token_type":"Bearer"
}
```
