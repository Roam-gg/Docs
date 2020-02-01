# Authentication

Roam will use Oauth2 for authenticating against the API. It will also silghtly extend to allow bots to interface with Roam's services.

## Scopes

| Name | Description |
|------|-------------|
| bot | Authorize a bot to join a Server |
| ego | Allows accessing your ego |
| identity | Allows reading your account details (including all egos)* |
| servers | Allows the application to see the servers you are a member of |
| servers.join | Allows the application to add the user to servers |
| messages.read | Allows the application to read users sent messages |
| friends | Allows the application to see your friends |

* Application must be verified by Roam to use this scope.

Both `servers.join` and `bot` require your application to have a linked bot account. Your bot must also be in a server you attempt to add a user into.

## Bot accounts

Bot accounts are handled differently, they are given API tokens through the Applications page, they use this token with their requests to authenticate.

## Verification

The identity scope can be potentially misused at it removes the anonmity of the user, therefore before an application can be used with roam it must be verified. To verify an application the appilication owner will enter a url/email on the application page, they wiil be placed on a waiting list. Roam will attempt to view the source for the application by checking the url or by asking with the email address's owner. Once checked Roam will either accept or deny the request. If accept the application can now use the protected scopes. If denied the application owner cannot attempt verification again for 2 weeks.
