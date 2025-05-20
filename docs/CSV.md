# Diagen CSV Files

Use these CSV files to prototype NPC behavior before Unreal integration.

**[← Table of contents](/README.md#table-of-contents)**

### On this page

[Explanation of State Tags](#explanation-of-state-tags)<br/>
[Character Information (CI)](#character-information-ci)  <br/>
[Topic Detection](#topic-detection)  <br/>
[Diagen Event Files](#diagen-event-files)  <br/>
[State Tags Weight](#state-tags-weight)  <br/>

<br/>

## Explanation of State Tags

State tags enable/disable context for NPCs.

> Example: `angry`, `in_Brevoy`, `quest_of_the_frozen_flame`

> [!NOTE]
> You can find more information about Diagen state tags on the [API reference](/docs/API_reference/Diagen_state_tags.md).

<br/>

## Character Information (CI)

CSV fields:

- `name`: Identifier for description  
- `stateTags`: Comma-separated tags required  
- `description`: Text to include in system prompt  

Descriptions merge at runtime based on active tags.

> [!NOTE]
> You can find more information about the CI Table on the [API reference](/docs/API_reference/Classes_structs_enums.md#character-information-table-ci-table).

<br/>

## Topic Detection

Defines dialogue triggers based on user input and tags.

| Field        | Description                            |
|--------------|----------------------------------------|
| `name`       | Topic ID                               |
| `stateTags`  | Active tags needed to detect topic     |
| `description`| Text prompt used for detection         |

> [!NOTE]
> You can find more information about the Topic Table on the [API reference](/docs/API_reference/Classes_structs_enums.md#topic-table).

<br/>

## Diagen Event Files

Configure in-game events and their effects:

| Field             | Description                                                  |
|-------------------|--------------------------------------------------------------|
| `name`            | Unique event key                                            |
| `stateTags`       | Tags required for event availability                         |
| `sayVerbatim`     | Exact NPC phrase                                            |
| `instruction`     | LLM-generated variation                                     |
| `returnTrigger`   | Value returned to game logic                                |
| `repeatable`      | Boolean: can re-trigger?                                     |
| `globalStateTags` | Boolean: apply tag changes to all NPCs                      |
| `enable/disable`  | Tags to add/remove upon trigger                             |
| `actionEvents`    | Blueprint functions to call                                 |

> [!NOTE]
> You can find more information about the Event Table on the [API reference](/docs/API_reference/Classes_structs_enums.md#diagen-event-table).

<br/>

## State Tags Weight

Prioritize which CI descriptions take precedence.

| Field    | Description                    |
|----------|--------------------------------|
| `name`   | Tag name                       |
| `weight` | Priority (higher = more urgent)|

<br/>