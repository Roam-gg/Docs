# Roam

## API

Roam as a service is built around connections, for this reason instead of using a REST API the roam API will use GraphQL.

## Theater

[Boards from Venus](analysis-Venus.md#Boards) and [Servers from Mercury](analysis-Mercury.md#Servers) will be merged into one object called a Theater. Theaters will have Channels that serve as both [feeds](analysis-Venus.md#Feeds) and [channels](analysis-Mercury.md#Channels).

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this Theater | snowflake |
| name | The name of this Theater (is unique) | string |
| channels | The [channels](#channel) of this Theater | List of [Channels](#channel) |
| roles | The [roles](#roles) of this Theater | List of [Roles](#roles) |
| flairs | The flairs that this server has | List of [Flairs](#flairs) |

## Channel

These are fields common to all channels, other channel types are [Feeds](design-Venus.md#feed), [Multi-Feeds](design-Venus.md#multi-feed), [Text Channels](design-Mercury.md#text-channel), [News Channels](design-Mercury.md#news-channel), and [Threads](design-Mercury.md#thread).

| Field | Description | Type |
|-------|-------------|------|
| id | The unique id of this Channel | snowflake |
| name | The name of this channel | string |
| overrides | The permission overrides | Dictionary with [role ids](#roles) for keys and integers for values |

## Message

All message type inherit these fields, other message types are: [Posts](design-Venus.md#post), [Comments](design-Venus.md#comment), [Text Messages](design-Mercury.md#text-message), and [News Articles](design-Mercury.md#news-article)

| Field | Description | Type |
|-------|-------------|------|
| id | The id of this message | snowflake |

## Users

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

### Egos

Roam wants to allow anonimity where desired, to this end roam will have Egos. Egos are a way of a user having multiple "accounts" that they can switch between. To other users these Egos appear completely disconnected so if looks as if there is two different users.

Only Egos are accessible through the API except for the requesting user. They may request their own user account.

| Field | Description | Type |
|-------|-------------|------|
| id | the unique id of this ego |
| name | the username for this ego | string (max length: 32 characters) |
| discriminator | the discriminator for this ego | int (min: 0, max: 9,999) |

## Roles

Each Theater can have roles that allow it to restrict what users can do on their services:
There are three special roles: `@everyone`, `@members`, and `@public`. These roles cannot be removed. Everyone represents all users on the platform, members represents all users that have joined a server. And public represents all the users that can view a server but have not joined.

| Field | Description | Type |
|-------|-------------|------|
| id | The id of the role | snowflake |
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
