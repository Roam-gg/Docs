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
| Attachment | Attachement for this section | [Attachment](design-Roam.md#Attachment) |
| theater | The theater a message is sent in | [Theater](design-Roam.md#Theater) |
| member | Member properities for a messages author | partial [User](design-Roam.md#Users) object |
| mention_everyone | Whether the message mentions everyone | boolean |
| mention_role | Any roles mentioned in this message | array of [roles](design-Roam.md#Roles) |
| reactions | Any reactions to a message | array of reaction objects |
| pinned | Whether a message has been pinned | boolean |


### News Article

| Field | Description | Type |
|-------|-------------|------|
| content | The text for this article | string (max length: 10,000) |
| flairs | The flairs attached to this article | List of [Flairs](design-Roam.md#flairs) |
| Attachment | Attachement for this section | [Attachment](design-Roam.md#Attachment) |
