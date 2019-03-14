
# User credentials

This authorization flow lets an application post user credentials (and client id and secret) to obtain a token on behalf of the user.

In this kind of flow, the client must provide its client id and credentials, as well as the username and password for the user.

## CURL

To do this try the following curl line

```
curl -H 'Content-Type: application/x-www-form-urlencoded' -X POST --user 'AuthCodeClient:Ultrasecretstuff' -d 'grant_type=password&username=admin&password=secret' localhost:3000/oauth2/token
```
This uses HTTP authentication for the client (AuthCodeClient with password Ultrasecretstuff) and passes the username and password using query parameters in the URL.


The previous command line call would use the proper HTTP Basic authentication mechanism to authenticate the client to AGILE IDM (assuming it is running in localhost in port 3000). The expected result looks like the following:

```
{
  "access_token":"1A9HeY99gSYTA2o0MxIhi8pM0UVG ... rWXvrc9nqSdlj1vsEQE3INQyR0bRODEl",
  "token_type":"Bearer"
}
```
