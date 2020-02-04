# Design: Mercury

## Channel

### Text Channel

| Field | Description | Type |
|-------|-------------|------|
| messages | The messages for this channel | List of [Text messages](#text-message) |

### News Channel

| Field | Description | Type |
|-------|-------------|------|
| messages | The articles for this channel | List of [News messages](#news-message) |
| allowed_flairs | The flairs that can be used in this channel | ?List of [Flairs](design-Roam.md#flairs) |

### Thread

| Field | Description | Type |
|-------|-------------|------|
| messages | The messages for this thread | List of [Text messages](#text-message)

## Message

### Text Message

| Field | Description | Type |
|-------|-------------|------|
| content | The text of the message | string (max length: 5,000) |

### News Article

| Field | Description | Type |
|-------|-------------|------|
| content | The text for this article | string (max length: 10,000) |
| flairs | The flairs attached to this article | List of [Flairs](design-Roam.md#flairs)
