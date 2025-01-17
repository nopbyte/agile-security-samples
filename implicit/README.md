# Implicit Authentication Example

## Run

Start agile-security (as a Node.js app), or by doing docker-compose up on the main folder.

And subsequently run the oauht2 client example by executing this in the root of the oauth2 client example project:
```
  node index.js
```
Then visit http://localhost:2000/

##Overview

Assuming that an oauth2 client has been registered in AGILE IDM, the flow to obtain an access token for any AGILE user using the implicit grant is depicted in the following picture.

<table align="center">
	<tr>
		<td><img src="images/tutorial-example-implicit.jpg" /></td>
	</tr>
	<tr align="center">
		<td>
			AGILE IDM interaction with Oauth2 clients
		</td>
	</tr>
</table>

From step 1 to 3, the authentication between IDM and the Oauth2 client occurs; however, it must be noted that in case AGILE IDM relies on another identity provider, such as google, to authenticate the user, additional steps will take place between step 2 and 3. In each step the following actions take place:

1. the user opens the Oauth2 client application, but he/she is not authenticated yet.

2. the Oauth2 client App redirects the user to AGILE IDM presenting its client id and a redirect URL that will be called by IDM on successful authentication of the user (if this URL matches the registration of the oauth client). Subsequently, the user authenticates with AGILE IDM using any of the authentication providers available.

3. On successful user authentication, IDM redirects the user with an access token and token type including the token and the token type as an URL fragment according to RFC 6749. At this point the browser can parse the URI and obtain the token and the token type to use it afterwards.

From this point on, the browser can use this token to interact with IDM, or with any other AGILE component that has been integrated with AGILE IDM.
