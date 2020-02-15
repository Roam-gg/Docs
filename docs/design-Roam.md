# Roam

## API

## IDs

IDs in a decentralized application are slightly more complex than a centralized application. A user may request a resource on a remote node, this means that ID's do not only have to act as an reference to the resource, but also as a reference to the source node. This is why all ids on roam are URNs following this format: `urn:{node_id}:{resource_id}`

Each resource ID is a [snowflake](https://developer.twitter.com/en/docs/basics/twitter-ids), using snowflakes guarantees uniqueness with all other resource ids on at least the node and potentially the entire network.

Node ids are UUIDs.

Roam as a service is built around connections, for this reason instead of using a REST API the roam API will use GraphQL.

## Family

Theater's can be grouped together in families, theater's in the same family can share their resources between each other. Each family has it's own owners.

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this family | URN |
| name | The name of this family | string |
| theaters | The [theaters](#theater) this board has | List of [Theaters](#theater) |
| roles | The [roles](#roles) this board has | List of [Roles](#roles) |
| channels | The [news channels](design-Mercury.md#news-channel) for the family | List of [News Channels](design-Mercury.md#news-channel) |
| emojis | This Theater's custom emojis | List of [Emojis](#emoji) |

## Theater

[Boards from Venus](analysis-Venus.md#Boards) and [Servers from Mercury](analysis-Mercury.md#Servers) will be merged into one object called a Theater. Theaters will have Channels that serve as both [feeds](analysis-Venus.md#Feeds) and [channels](analysis-Mercury.md#Channels).

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this Theater | URN |
| name | The name of this Theater (is unique) | string (length: 2-100 Characters) |
| channels | The [channels](#channel) of this Theater | List of [Channels](#channel) |
| roles | The [roles](#roles) of this Theater | List of [Roles](#roles) |
| flairs | The [flairs](#flairs) that this server has | List of [Flairs](#flairs) |
| family | The [family](#family) this theater belongs to | [Family](#family) |
| shared_channels | The [channels](#channel) that this theater has from other theaters/its family | List of [Channels](#channel) |
| shared_roles | The [roles](#roles) that this theather has from other theaters/its family | List of [Roles](#roles) |
| icon | The Theater's icon | ?icon hash |
| banner | The Theater's banner | ?banner hash |
| emojis | This Theater's custom emojis | List of [Emojis](#emoji) |

### Mutations

#### createTheater

Returns a new [Theater](#theater) on success.

##### Input

| Field | Description | Type |
|-------|-------------|------|
| name | The name for the new theater | string (length: 2-100 Characters) |
| icon | base64 128x128 image for the new theater | string |
| banner | base64 16:9 image for the new theater | string |
| roles | Roles for the new theater | List of [Roles](#roles) |
| channels | Channels for the new theater | List of Partial Channels |

##### Partial Channel

| Field | Description | Type |
|-------|-------------|------|
| name | The name for the new channel | string |
| type | The type for the new channel | string |

#### updateTheater

Returns the updated [Theater](#theater) on a success.

##### Input

| Field | Description | Type |
|-------|-------------|------|
| id | The id of the [Theater](#theater) to update | URN |
| name | The theater's new name | ?string (length: 2-100 Characters) |
| icon | base64 128x128 image | ?string |
| banner | base64 16:9 image | ?string |

#### deleteTheater

Returns the deleted [Theater](#theater) on a success.

##### Input

Takes the theater's id.

## Channel

These are fields common to all channels, other channel types are [Feeds](design-Venus.md#feed), [Multi-Feeds](design-Venus.md#multi-feed), [Text Channels](design-Mercury.md#text-channel), [News Channels](design-Mercury.md#news-channel), [Threads](design-Mercury.md#thread), and [Timelines](design-Terra.md#timeline).

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this Channel | URN |
| name | The name of this channel | string |
| last_message | The last message sent in the channel | [Message](#message) |
| overrides* | The permission overrides | List of [Overide Objects](#overrides) |

* overrides are not present in user's timelines.

### Overrides

| Field | Description | Type |
|-------|-------------|------|
| subject | the role/ego that is being overriden | [Role](#roles) or [Ego](#egos) |
| permissions | the permissions to override with | integer |

## Message

All message type inherit these fields, other message types are: [Posts](design-Venus.md#post), [Comments](design-Venus.md#comment), [Text Messages](design-Mercury.md#text-message), and [News Articles](design-Mercury.md#news-article)

| Field | Description | Type |
|-------|-------------|------|
| id | The id of this message | URN |
| author | The [ego](#egos) that created this message (null if ego/user was deleted) | ?[Ego](#egos) |
| channel | Channel the message was sent in |  |
| attachment | Any [Attached](#Attachment) files |  |
| timestamp | Time a message was sent | ISO8601 timestamp |
| edit_timestamp | Time a message was edited | ISO8601 timestamp |
| history | The history of all edits made to a post | ?message |
| embeds | Embedded content | array of embed objects |
| nonce | Validating a message has been sent | integer or string |

## Users

There are three different types of "user" on the platform: humans, bots, and organisations. Organisations cannot use Venus or Mercury so they are treated differently. We shall categorise these types of users by what they can use.

* Clients are the base type, they can access Roam's Terra service
  * Organisations have a page on Terra, they can be DMed by other users but cannot send messages unsolicited. They are marked clearly to other users as brands.
* Users can also use Roam's Venus and Mercury Services
  * Persons are normal accounts
  * Bots are clearly marked to make other users aware that they are automated, they do not have profiles and instead have information pages.

```
         Client
        /      \
    User        Organisation
   /    \
Bot      Person
```

The following objects are not publicly accessible and are only documented for reference:

### Client

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id for this client | URN |

### Organisation

| Field | Description | Type |
|-------|-------------|------|
| name | The name of the organisation | string |
| verified | whether this organisation is verified | boolean |

### Person

| Field | Description | Type |
|-------|-------------|------|
| email | The __verified__ email address tied to this user | ?string |
| egos | The [egos](#egos) this user has | List of [egos](#egos) |
| verified | Whether this user is verified | boolean |
| displayed_verification | The [ego](#egos) the verification status (if present) is displayed | [Ego](#egos) |
| displayed_flags | Which [ego](#egos) to display flags on (if applicable) | [Ego](#egos) |
| flags | The flags that this user has | integer |
| hashp | The users hashed & salted password | bcrypt hash |

### Bot

| Field | Description | Type |
|-------|-------------|------|
| ego | The [ego](#ego) this bot uses | [Ego](#ego) |

## Egos

Roam wants to allow anonimity where desired, to this end roam will have Egos. Egos are a way of a user having multiple "accounts" that they can switch between. To other users these Egos appear completely disconnected so if looks as if there is two different users.

Only Egos are accessible through the API except for the requesting user. They may request their own user account.

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this ego |
| name | The username for this ego | string (max length: 32 characters) |
| verified | Whether this ego is verfied or not | boolean |
| flags | The flags for this ego | integer |
| discriminator | The discriminator for this ego | int (min: 0, max: 9,999) |
| avatar | The avatar hash for this ego | string |
| bot | whether this ego is part of an OAuth2 application | boolean |

### User Flags

| Flag | Value (2<sup>x</sup>) |
|------|-----------------------|
| None | 0 |
| Emperors | 1 |
| Roam Employee | 2 |
| Roam Partner | 3 |
| System | 4 |
| Hosts | 5 |
| Top Posts | 6 |
| Bottom Post | 7 |
| Bug Collector | 8 |

## Roles

Each Theater can have roles that allow it to restrict what users can do on their services:
There are three special roles: `@everyone`, `@members`, and `@public`. These roles cannot be removed. Everyone represents all users on the platform, members represents all users that have joined a server. And public represents all the users that can view a server but have not joined.

| Field | Description | Type |
|-------|-------------|------|
| id | The id of the role | URN |
| name | The name of the role | string (max length: 32 characters) |
| colour | The colour of the role | integer |
| permissions | The permissions for this user | integer |
| mentionable | Whether this role can be mentoined in messages | boolean |

## Flairs

Each Theater can have its ovn flairs that are used to categorise posts in [feeds](design-Venus.md#feed) and [news](design-Mercury.md#news-channel) channels. Each [feed](design-Venus.md#feed) and [news](design-Mercury.md#news-channel) channel also has a list of allowed flairs for the [channel](#channel), [messages](#message) that have flairs not in this list are rejected by the server. The list can also be null, when it is all flairs are allowed.

| Flairs | Description | Type |
|--------|-------------|------|
| name | The name of this flair | string |
| colour | The colour of the flair | integer |

## Emoji

| Field | Description | Type |
|-------|-------------|------|
| id | The id for the emoji | URN |
| name | The name of the emoji | string |
| roles | The roles allowed to use this emoji | List of [Roles](#roles) |
| ego | The ego that created this emoji | [Ego](#egos) |
| require_colons | Whether this emoji requires colons around it | boolean |
| animated | Whether this emoji is animated | boolean |

## Permissions

| Permissions | Value (2<sup>x</sup>) | Description | District |
|-------------|-----------------------|-------------|----------|
| SEND_MESSAGES | 0 | Allows users to send a message in a text channel or thread | M, V |
| CREATE_POST | 1 | Allows Users to create a post on a feed | V |
| CAN_VOTE | 2 | Allows users to vote up or down a post | V |
| CREATE_COMMENT | 3 | Allows users to comment on a post | V |
| CREATE_STATUS_UPDATE | 4 | Allows users to create a status update on a groups timeline | T |
| REACT_TO_STATUS | 5 | Allows users to react to status updates | M |
| ATTACH_FILES | 6 | Allows users to upload images and files | M, V, T(Groups) |
| READ_MESSAGE_HISTORY | 7 | Allows users to read message history | M |
| FAMILY_MODERATOR | 8 | Allows all permissions and bypasses channel and server overrides within a family of Theaters | M, V, T |
| MANAGE_FAMILY | 9 | Allows a user to manage and edit a family | M, V, T|
| ADMINISTRATOR | 10 | Allows all permissions and bypasses channel overrides within a theater | M, V, T |
| MANAGE_SERVER | 11 | Allows a user to manage and edit a server | M, V, T |
| SEND_NEWS_UPDATE | 12 | Allows a user to create a news update | M, V |
| MANAGE_NEWS_CHANNEL | 13 | Allows a user to manage and edit a news channel | M, V |
| MANAGE_MESSAGES | 14 | Allows a user to delete orther users messages | M, V, T |
| VIEW_CHANNEL | 15 | Allows a users to view a channel | M, V |
| BAN_MEMBERS | 16 | Allows a user to ban a member of a Theater | M, V, T |
| KICK_MEMBERS | 17 | Allows a user to kick a member of a theater | M, V, T |
| CREATE_INVITE | 18 | Allows a user to create an invite for a theater | M, V, T |
| MANAGE_CHANNELS | 19 | Allows a user to manage and edit a channel | M, V, T |
| MANAGE_ROLES | 20 | Allows a user to manage and edit roles | M, V, T |
| CREATE_THREAD | 21 | Allows a user to create a thread | M |
| MANAGE_THREAD | 22 | Allows a user to manage and edit a thread | M |
| AUTO-EMBED_LINK | 23 | Links sent with this permissions will be auto-embedded | M, T |
| ADD_REACTIONS | 24 | Allows users to add reactions to messages | M |  
| SHARE_CHANNEL | 25 | Allows a user to share a channel between multiple servers | M, V, T(Org) |
| MANAGE_FLAIRS | 26 | Allows a user to manage and edit flairs | M, V |
| MENTION_EVERYONE | 27 | Users with this permission can mention everyone within a server | M |
| CHANGE_OWN_NICKNAME | 28 | Allows a user to change their nickname | M, T |
| MANAGE_NICKNAMES | 29 | Allows a user to manage and edit other users nicknames | M, T |
| VIEW_AUDIT_LOGS | 30 | Allows a user to view audit logs | M, V, T |
| MANAGE_PAGE | 31 | Allows a user to manage and edit a page | T(Org) |
| MANAGE_POSTS | 32 | Allows a user to manage and delete other users posts | V |
| USE_EXTERNAL_EMOJIS | 33 | Allows a user to use custom emojis | M, V, T |
| MANAGE_EMOJIS | 34 | Allows a user to manage and edit emojis | M, V, T |
| SCHEDULE_EVENT | 35 | Allows a user to schedule an event | T(Groups) |
| START_POLL | 36 | Allows a user to begin a poll | M, V, T |

## Attachment

| Field | Description | Type |
|-------|-------------|------|
| id | ID of the attachment | URN |
| filename | Name of the attached file | string |
| size | Attachment size in bytes | integer |
| url | Source url of attachment | string |
| proxy_url | Proxied url of attachment | string |
| height | Height of attachment | ?integer |
| width | Width of attachment | ?integer |
