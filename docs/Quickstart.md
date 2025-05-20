# Quickstart

**[← Table of contents](/README.md#table-of-contents)**

### On this page

[Installation]()<br/>
[Usage]()<br/>
    [Prompting the Model]()<br/>
    [Manage NPCs]()<br/>
    [State Tag Management]()<br/>

## Installation

1. Download from [create.xandimmersion.com](https://create.xandimmersion.com/) 

![Download diagen image](/docs/images/embedded_15_6.png)

2. Place under `YourProject/Plugins/Diagen/`  

![Place diagen image](/docs/images/embedded_15_7.png)
![Place diagen image 2](/docs/images/embedded_15_8.png)

3. Launch Unreal Editor

    * **If the following message appear:**
    * ![Launch editor warning image](/docs/images/embedded_16_9.png)
    * *This means that the Engine version of the plugin does not match your project engine version. If you have the C/C++ Build tools installed for Unreal, you can click “Yes” and the Diagen plugin should compile for your version of the Engine. After compiling or if the plugin was already compiled, the editor should start.*

![Launch editor image](/docs/images/embedded_16_10.png)

4. In `Edit > Project Settings > Plugins > Diagen`, paste your API Key  

![Diagen plugin settings image](/docs/images/embedded_16_11.png)

5. Hit Enter and Confirm download of local model

![Diagen model download image](/docs/images/embedded_16_12.png)

<br/>

## Usage

> **Diagen requires** the local executable installed.

### Prompting the Model

Use `BeginPlay` / `EndPlay` to manage the local process:

- [START DIAGEN LOCAL](/docs/API_reference/Local.md#start-diagen-local-executable) with the [Diagen Prompt Config](/docs/API_reference/Classes_structs_enums.md#diagen-prompt-config)
- [STOP DIAGEN LOCAL](/docs/API_reference/Local.md#stop-diagen-local-executable)
- [Get Diagen Local Executable Status](/docs/API_reference/Local.md#get-diagen-local-executable-status---pure) *(pure)*

![BeginPlay/EndPlay Nodes](/docs/images/embedded_17_14.png)

Prompt with:

- **Raw**: [Diagen Prompt AI Model (Raw)](/docs/API_reference/LLM_prompting.md#diagen-prompt-ai-model-raw)

  ![Prompt AI Model Raw](/docs/images/embedded_17_15.png)

- **Structured**: use [Create Prompt](/docs/API_reference/LLM_prompting.md#create-prompt) followed by [Diagen Prompt AI model (Conversation)](/docs/API_reference/LLM_prompting.md#diagen-prompt-ai-model-conversation)  

  ![Create Prompt Node](/docs/images/embedded_17_16.png)

> [!NOTE]
> You can find more information about how to prompt the LLM model on the [API Reference](/docs/API_reference/LLM_prompting.md)

<br/>

### Manage NPCs

Use a shared **[SessionState](/docs/API_reference/Classes_structs_enums.md#session-state)** array combined with the following nodes to manage NPC lifecycle:

| Action    | Blueprint Node          |
|-----------|-------------------------|
| Add NPC   | [Add NPC](/docs/API_reference/Diagen_session.md#add-npc) |
| Remove NPC| [Remove NPC](/docs/API_reference/Diagen_session.md#remove-npc) |
| Reset NPC | [Reset NPC](/docs/API_reference/Diagen_session.md#reset-npc) |
| List NPCs | [Get Session NPC Names](/docs/API_reference/Diagen_session.md#get-session-npc-names) |

![Manage npc nodes](/docs/images/embedded_18_17.png)
![List npc node](/docs/images/embedded_18_18.png)

> [!NOTE]
> You can find more information about how to manage NPCs on the [API Reference](/docs/API_reference/Diagen_session.md)

<br/>

### State Tag Management

| Action          | Blueprint Node                    |
|-----------------|-----------------------------------|
| Append tags     | [Append NPC State Tags](/docs/API_reference/Diagen_state_tags.md#append-npc-state-tags) |
| Remove tags     | [Remove NPC State Tags](/docs/API_reference/Diagen_state_tags.md#remove-npc-state-tags) |
| Clear all tags  | [Clear NPC State Tags](/docs/API_reference/Diagen_state_tags.md#clear-npc-state-tags) |
| Set new tags    | [Set NPC State Tags](/docs/API_reference/Diagen_state_tags.md#set-npc-state-tags) |
| Query tags      | [Get NPC Enabled State Tags](/docs/API_reference/Diagen_state_tags.md#get-npc-state-tags) / [Contains NPC State Tags](/docs/API_reference/Diagen_state_tags.md#contains-npc-state-tags) |

![State tags nodes 1](/docs/images/embedded_18_19.png)
![State tags nodes 2](/docs/images/embedded_19_20.png)

> [!NOTE]
> You can find more information about how to manage NPC tags on the [API Reference](/docs/API_reference/Diagen_state_tags.md)