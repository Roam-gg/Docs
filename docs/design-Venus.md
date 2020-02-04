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
| content | The content of the post | List of [feed message content](#post-content) (max size: 40,000 characters OR 50MB whichever is hit first) |

#### Post Content

Either:

##### Image content

| Field | Description | Type |
|-------|-------------|------|
| source | The source for the image | url |
| content | The raw btyes for the image | png/gif/jpg/mp4 |

##### Text content

| Field | Description | Type |
|-------|-------------|------|
| content | The content of the text section | string |

### Comment

| Field | Description | Type |
|-------|-------------|------|
| content | The content of this comment | string |
| replies | The replies to this comment | List of [comments](#comment) |
