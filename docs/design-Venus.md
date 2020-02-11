# Design: Venus

## Channels

### Feed

| Field | Description | Type |
|-------|-------------|------|
| messages | The posts for this channel | List of [Feed messages](#post) |
| allowed_flairs | The flairs that can be used in this channel | ?List of [Flairs](design-Roam.md#flairs) |

### Multi-Feed

| Field | Description | Type |
|-------|-------------|------|
| sources | The sources for this channel  | List of [Feed Channels](#feed)

## Messages

### Post

| Field | Description | Type |
|-------|-------------|------|
| title | The title of the post | string (max length: 100) |
| content | The content of the post | List of [Post Content](#post-content) (max size: 40,000 characters OR 50MB whichever is hit first) |
| theater | The theater the post is created in | [Theater](design-Roam.md#Theater) |
| comments | The list of top level comments for a post | List of [Comments](#Comment) |
| upvotes | The amount of upvotes for the posts | integer |
| downvotes | The amount of downvotes for the post | integer |
|total_votes | The total amount of votes recieved | integer |
| rant | The rank used for ordering the post | float |

#### Post Content

Either an [Attachment](design-Roam.md#Attachment) or a:

##### Text content

| Field | Description | Type |
|-------|-------------|------|
| title | The title of this section | ?string |
| content | The content of the text section | string |

### Comment

| Field | Description | Type |
|-------|-------------|------|
| content | The content of this comment | string |
| replies | The replies to this comment | List of [comments](#comment) |
| total_votes | The total amount of votes received | integer |
| upvotes | The amount of upvotes for the posts | integer |
| downvotes | The amount of downvotes for the post | integer |
| post | The [post](#post) that this comment was made on | [Post](#post) |
| rank | The rank used for ordering | float |
