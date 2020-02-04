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

| Emotion | Emoji |
|---------|-------|
| ACCOMPLISHED |  |
| ALIVE |  |
| ALONE |  |
| AMAZED |  |
| AMAZING |  |
| AMUSED |  |
| ANGRY |  |
| ANNOYED |  |
| ASHAMED |  |
| ASLEEP |  |
| AWESOME |  |
| AWFUL |  |
| BAD |  |
| BEAUTIFUL |  |
| BETTER |  |
| BLESSED |  |
| BLISSFUL |  |
| BORED |  |
| BROKEN |  |
| CALM |  |
| CHILL |  |
| COLD |  |
| COMFORTABLE |  |
| CONCERNED |  |
| CONFIDENT |  |
| CONFUSED |  |
| CONSTRAINED |  |
| COOL |  |
| CRAZY |  |
| CURIOUS |  |
| CUTE |  |
| DELIGHTED |  |
| DETERMINED |  |
| DISAPPOINTED |  |
| DOWN |  |
| DRAINED |  |
| EMOTIONAL |  |
| ENERGISED |  |
| EXCITED |  |
| EXHAUSTED |  |
| FABULOUS |  |
| FANTASTIC |  |
| FED_UP |  |
| FESTIVE |  |
| FIRED_UP |  |
| FREE |  |
| FRESH |  |
| FRUSTRATED |  |
| FUNNY |  |
| FURIOUS |  |
| GLAD |  |
| GOOD |  |
| GOOFY |  |
| GRATEFUL |  |
| GREAT |  |
| GUILTY |  |
| HAPPY |  |
| HEARTBROKEN |  |
| HOPEFUL |  |
| HORRIBLE |  |
| HUMAN |  |
| HUNGRY |  |
| HURT |  |
| HYPED |  |
| HYPER |  |
| INCOMPLETE |  |
| IN_LOVE |  |
| INSPIRED |  |
| IRRITATED |  |
| JOLLY |  |
| JOYFUL |  |
| LAZY |  |
| LONELY |  |
| LOST |  |
| LOVED |  |
| LOVELY |  |
| LOW |  |
| LUCKY |  |
| MEH |  |
| MISCHIEVOUS |  |
| MISSING |  |
| MOTIVATED |  |
| NOSTALGIC |  |
| OK |  |
| OLD |  |
| OPTIMISTIC |  |
| PAINED |  |
| PEACEFUL |  |
| PERPLEXED |  |
| POSITIVE |  |
| PRETTY |  |
| PROFESSIONAL |  |
| PROUD |  |
| PUMPED |  |
| PUZZLED |  |
| REFRESHED |  |
| RELAXED |  |
| ROUGH |  |
| SAD |  |
| SAFE |  |
| SARCASTIC |  |
| SATISFIED |  |
| SHY |  |
| SICK |  |
| SILLY |  |
| SLEEPY |  |
| SORRY |  |
| SPECIAL |  |
| STRESSED |  |
| STRONG |  |
| STUPID |  |
| SUPER |  |
| SURPRISED |  |
| TERRIBLE |  |
| THANKFUL |  |
| THOUGHTFUL |  |
| TIRED |  |
| USELESS |  |
| WEIRD |  |
| WELCOME |  |
| WELL |  |
| WONDERFUL |  |
| WORRIED |  |
| WORSE |  |
| YOUNG |  |

## Activity

| Activity | Emoji |
|----------|-------|
|CELEBRATING |  |
| WATCHING |  |
| EATING |  |
| DRINKING |  |
| TRAVELLING_TO |  |
| ATTENDING |  |
| LISTENING_TO |  |
| LOOKING_FOR |  |
| THINKING_ABOUT |  |
| READING |  |
| PLAYING |  |
| SUPPORTING |  |
| WORKING_ON |  |

