# Roam

## Structs

## API

Roam as a service is built around connections, for this reason instead of using a REST API the roam API will use GraphQL.

### Theater

[Boards from Venus](analysis-Venus.md#Boards) and [Servers from Mercury](analysis-Mercury.md#Servers) will be merged into one object called a Theater. Theaters will have Channels that serve as both [feeds](analysis-Venus.md#Feeds) and [channels](analysis-Mercury.md#Channels).

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this Theater | snowflake |
| name | The name of this Theater (is unique) | string |
| channels | The [channels](#base-channel) of this Theater | List of [Channels](#base-channel) |
| roles | The [roles](#roles) of this Theater | List of [Roles](#roles) |

### Base Channel

These are fields common to all channels

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this Channel | snowflake |
| name | The name of this channel | string |
| overrides | The permission overrides | Dictionary with [role ids](#roles) for keys and integers for values |

#### Theater Text Channel

| Field | Description | Type |
|-------|-------------|------|
| messages | The messages for this channel | List of [Text messages](#text-message) |

#### Theater Feed Channel

| Field | Description | Type |
|-------|-------------|------|
| messages | The posts for this channel | List of [Feed messages](#feed-message) |

##### Multi Feed Channel

| Field | Description | Type |
|-------|-------------|------|
| sources | The sources for this channel  | List of [Feed Channels](#theater-feed-channel)

#### Theater News Channel

| Field | Description | Type |
|-------|-------------|------|
| messages | The articles for this channel | List of [News messages](#news-message) |

#### Thread Channel

| Field | Description | Type |
|-------|-------------|------|
| messages | The messages for this thread | List of [Text messages](#text-message)

### Message

#### Base Message

All message type inherit these fields

| Field | Description | Type |
|-------|-------------|------|
| id | The id of this message | snowflake |

#### Text Message

| Field | Description | Type |
|-------|-------------|------|
| content | The text of the message | string (max length: 5,000) |

#### Feed Message

| Field | Description | Type |
|-------|-------------|------|
| title | The title of the post | string (max length: 100) |
| content | The content of the post | List of [feed message content](#feed-message-content) (max size: 40,000 characters OR 50MB whichever is hit first) |

##### Feed Message Content

Either:

###### Image content

| Field | Description | Type |
|-------|-------------|------|
| source | The source for the image | url |
| content | The raw btyes for the image | png/gif/jpg/mp4 |

###### Text content

| Field | Description | Type |
|-------|-------------|------|
| content | The content of the text section | string |

### Users

There are three different types of "user" on the platform: humans, bots, and organisations. Organisations cannot use Venus or Mercury so they are treated differently. We shall categorise these types of users by what they can use.

- Clients can access and use Terra's features

- Users can access and use Venus & Mercury's features

```
         Client
        /      \
    User        Organisation
   /    \
Bot      Person
```

| Field | Description | Type |
|-------|-------------|------|
| id | this user's unique id | snowflake |
| email? | the __verified__ email address tied to this user | string |
| egos | The [egos](#egos) this user has | List of [egos](#egos) |

#### Egos

Roam wants to allow anonimity where desired, to this end roam will have Egos. Egos are a way of a user having multiple "accounts" that they can switch between. To other users these Egos appear completely disconnected so if looks as if there is two different users.

Only Egos are accessible through the API except for the requesting user. They may request their own user account.

| Field | Description | Type |
|-------|-------------|------|
| id | the unique id of this ego |
| name | the username for this ego | string (max length: 32 characters) |
| discriminator | the discriminator for this ego | int (min: 0, max: 9,999) |

### Roles

| Field | Description | Type |
|-------|-------------|------|
| id | The id of the role | snowflake |
| name | The name of the role | string (max length: 32 characters) |
| colour | The colour of the role | integer |
| permissions | The permissions for this user | integer |
| mentionable | Whether this role can be mentoined in messages | boolean |
