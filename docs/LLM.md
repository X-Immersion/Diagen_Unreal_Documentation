# Explication about LLM

**[← Table of contents](/README.md#table-of-contents)**

### On this page

[Description (System Prompt)](#description-system-prompt)<br/>
[Input (User Prompt)](#input-user-prompt)  <br/>
[History](#history)  <br/>
[Training Dataset](#training-dataset)  <br/>
[Parameters](#parameters)  <br/>
    [Diagen LLM Parameters](#diagen-llm-parameters)  <br/>
    [Diagen Prompt Parameters](#diagen-prompt-parameters)  <br/>
    [Temperature](#temperature)  <br/>
    [Context Size](#context-size)  <br/>
    [Toxicity Filtering](#toxicity-filtering)  <br/>

## Explication about LLM

Diagen uses a Large Language Model (LLM) trained on vast amounts of text to generate contextually relevant dialogue based on four main components:

- **System Prompt**  
- **User Prompt**  
- **History**  
- **LLM Parameters**

This enables dynamic interactions between players, NPCs, and the environment.

<br/>

## Description (System Prompt)

The system prompt provides context and defines the “role” or style of the LLM.  
You can generate it dynamically from the Character Information Table.

> _Example:_  
> `You are Abrogail, the ruthless and cunning Empress of Cheliax, feared across the realms. You speak with sharp, biting cynicism.`

<br/>

## Input (User Prompt)

Two types:

- **Questions**: directed at NPCs  
  _Example:_ `Hi! I'm Tom. How long have you been Queen?`
- **Instructions**: commands for in-world reactions  
  _Example:_ `You say that you demand this person to identify herself.`

> ⚠️ Unprompted LLMs may answer unpredictably without initial context.

<br/>

## History

For multi-turn conversations, include prior exchanges:
* System Prompt
* User #0
* Assistant #0
* User #1
* Assistant #1
* ...
* User Current
* `assistant:`

Trim old history to preserve tokens.

<br/>

## Training Dataset

Fine-tuning is currently unavailable in-app but can be arranged via [contact@xandimmersion.com](mailto:contact@xandimmersion.com).

Use custom lore, character backstories, and dialogue logs for more authentic responses.

<br/>

## Parameters

![LLM Config Parameters](/docs/images/embedded_7_1.png)

### Diagen LLM Parameters

Configure global LLM settings with the node [Start Diagen Local Executable (START DIAGEN LOCAL)](/docs/API_reference/Local.md#start-diagen-local-executable):



| Parameter            | Default        | Description                                                      |
|----------------------|----------------|------------------------------------------------------------------|
| **Model Name**       | `baseXI7.gguf` | GGUF model file in `Plugins/Diagen/Local/models/`                |
| **Context Max Size** | `2048`         | Power of 2; max 8196                                             |
| **GPU Layers**       | `-1`           | Automatic selection                                              |
| **Flash Attention**  | `true`         | Speed optimization                                               |
| **GPU Select**       | `-1`           | For multi-GPU setups                                             |
| **Utilization**      | `1.0`          | GPU usage ratio (100%)                                           |
| **Max GPU Size GB**  | `1.0`          | For internal resource calculation                                |
| **Port**             | `8002`         | HTTP port for engine ↔ LLM communication                         |

> [!NOTE]  
> You can find more details on the LLM parameters by looking at the [Diagen Subsystem Config](/docs/API_reference/Classes_structs_enums.md#diagen-subsystem-config) struct.

<br/>

### Diagen Prompt Parameters

Per-prompt overrides in all `Diagen Prompt AI Model` nodes:

| Parameter               | Default | Description                          |
|-------------------------|---------|--------------------------------------|
| **N Predict**           | `80`    | Max tokens to generate; `-1` = none  |
| **Temperature**         | `2.0`   | Controls randomness/creativity       |
| **Dynamic Temp Range**  | `0.0`   | ± variation around temperature       |
| **Top-K**               | `40`    | Limit token selection to top K       |
| **Top-P**               | `0.95`  | Cumulative probability threshold     |
| **Cache Prompt**        | `true`  | Reuses common prefix for speed       |
| **Repeat Penalty**      | `1.0`   | Penalizes repeated tokens            |
| **Frequency Penalty**   | `0.8`   | Reduces frequent term repetition     |
| **Presence Penalty**    | `0.3`   | Reduces reuse of prior tokens        |
| **Stop Tokens**         | `[]`    | List of strings to halt generation   |

> [!NOTE]  
> You can find more details on the prompt parameters by looking at the [Diagen Prompt Config](/docs/API_reference/Classes_structs_enums.md#diagen-prompt-config) struct.

<br/>

### Temperature

| Value | Behavior                          |
|-------|-----------------------------------|
| `0.2` | Deterministic, focused            |
| `0.8` | Creative, varied                  |
| `2.0` | Novel, higher risk of incoherence |

![Temperature image](/docs/images/embedded_10_2.png)

<br/>

### Context Size

- **Short** (512): fast, concise  
- **Long** (2048+): detailed narratives  

Beware of token window limits.

<br/>

### Toxicity Filtering

| Level | Effect                         |
|-------|--------------------------------|
| `0.0` | No filtering                   |
| `1.0` | Strict safe content            |

Consider external moderation layers if needed.