# Design: Terra

## Channels

### Timeline

| Field | Description | Type |
|-------|-------------|------|
| messages | The status updates for the timeline | List of [Status Updates](#status-update) |

## Messages

### Status Update

| Field | Description | Type |
|-------|-------------|------|
| content | The status update's content | string (max length: 65,536 characters) |
| media | The images/video attached to this update | List of [Attachments](design-Roam.md#attachment) |
| emotion | The [emotion](#emotion) attached to the status update | [Emotion](#emotion) |
| activity | The [activity](#activity) attached to the status update | [Activity](#activity) |
| mentions | The [egos](analysis-Roam.md#egos) mentioned in this status update | List of [Egos](design-Roam.md#egos) |
| location | The location attached to this status update | Geographic Coords |
| background | The background used for this status update | url |

## Activity

TODO: Add activity

## Emotion

TODO: Add emotion
