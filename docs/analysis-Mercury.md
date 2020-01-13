# Mercury: Messaging Service

Mercury is an IM and DM service designed to encourage communication between users by leveraging its integration with the other services of the Roam platform.

## Servers

Roam as a platform is built around making it easier to grow and communicate with your communities. In aim of this goal, Roam will provide instant messaging to allow people within communities to communicate in real time.

### Integrations

Communities that have pages on [Terra](analysis-Terra.md) or boards on [Venus](analysis-Venus.md) can connect them to servers on Mercury. Users on Venus may see messages from a designated [channel](#channels) alongside their board's feed. Users who follow groups or pages on Terra will be able to access connected servers through the group/page and designated statuses will appear in news channels of connected servers.

### Families

Similarly to boards on Venus, servers can be linked together into families. Families are a way of grouping servers together so that users can find similar servers easily. Families have their own pages which moderators can style, these pages include family news channels and links to all family members.

#### Moderators

Families have moderators similar to servers, however unlike servers families do not have owners. The moderators all have equal permissions. Whenever a server joins the family a new moderator for the family will be picked from the server's users by the server's moderators, if someone who is already a family moderator is picked the server is just added.

### Ownership

By default a user who creates a server will be set as its owner, however, multiple people can be set as owners through the server settings. If an organisation creates a server multiple owners can be set from creation.

Owners always have all permissions no matter what roles they may have or channel overrides. Owners are the only users who can delete a server.

### Channels

Channels will provide a way for servers to split discussion into several places based on topic. This allows users to communicate about different things without stepping on each other.

#### Text Channels

Text channels will function like regular IM chats.

#### News Channels

News channels will allow users to easily find and view news pertaining to the server or any relevant Venus boards/Terra pages/groups. Posting of news will be restricted at the discretion of server moderators.

#### Channel Sharing

Server moderators will be able to share channels between two or more servers. Additionally channels can be shared with a server's family. All the members of servers that a channel is shared in maintain their roles when in the channel. There is only one set of permission overrides for the channel, which is the same across all servers.

### Permissions

Permissions allow owners of a server or family to specify what users can or cannot do. These permissions will include sending messages, adding mentions to certain roles and deleting messages.

#### Roles

Roles allow owners to attach a specific set of permissions to a user. Roles can be mentioned to notify everyone who has the role. Every server will come with two default roles and has a special role. These roles are: moderator, newscaster and everyone. Everyone is a special role as it cannot be deleted and all users have it. Moderator is a default that grants users the ability to delete messages and other features that will allow them to moderate channels. Newscaster will allow users to post in news channels. Roles can be created and named as owners or users with the appropriate permissions allow. A user can have more than one role.

#### Channel Overrides

Permissions are set serverwide but can be overridden in a channel to grant or remove permissions from users only in that channel. Permissions for each role can be overridden within channels.

## Threads

Sometime in a conversation users may want to respond to a specific message without clogging up the main channel. Mercury provides a way to do this through threads. Threads allow users to reply to a message in its on own dedicated channel with the option of also sending the message in the main channel. Threads can be joined by users, only users who have joined the thread will recieve notifications from it.

## Integration

Users that use Terra can choose to have their most recent status update appear on their profile in Mercury.
