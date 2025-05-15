# DIAGEN for Unreal

A high-quality, local-first dialogue generation plugin for Unreal Engine (5.2+), powered by LLMs.

---

## Table of Contents

1. [Explication about LLM](#1-explication-about-llm)
   - [1.1. Description (System Prompt)](#11-description-system-prompt)
   - [1.2. Input (User Prompt)](#12-input-user-prompt)
   - [1.3. History](#13-history)
   - [1.4. Training Dataset](#14-training-dataset)
   - [1.5. Parameters](#15-parameters)
     - [1.5.1. Diagen LLM Parameters](#151-diagen-llm-parameters)
     - [1.5.2. Diagen Prompt Parameters](#152-diagen-prompt-parameters)
     - [1.5.3. Temperature](#153-temperature)
     - [1.5.4. Context Size](#154-context-size)
     - [1.5.5. Toxicity Filtering](#155-toxicity-filtering)

---

## 1. Explication about LLM

Diagen uses a Large Language Model (LLM) trained on vast amounts of text to generate contextually relevant dialogue based on four main components:

- **System Prompt**
- **User Prompt**
- **History**
- **LLM Parameters**

This enables dynamic interactions between players, NPCs, and even the environment.

---

### 1.1. Description (System Prompt)

The system prompt gives initial context to the model, defining its "role" or expectations.

> _Example:_  
> `You are Abrogail, the ruthless and cunning Empress of Cheliax, feared across the realms. You speak with sharp, biting cynicism.`

Use the **Character Information Data Table** to make these prompts dynamic and reactive to in-game states.

---

### 1.2. Input (User Prompt)

Two types of prompts:

- **Questions** — Interactions with NPCs  
  _Example:_ `Hi! I'm Tom. How long have you been Queen?`

- **Instructions** — System actions or reactions  
  _Example:_ `You say that you demand this person to identify herself.`

> ⚠️ Without a system prompt or context, the LLM may produce unpredictable results.

---

### 1.3. History

For multi-turn conversations or adjustments ("Could you say that but softer?"), include history like this:
System Prompt
User #1 → Assistant #1
User #2 → Assistant #2
...
Current User → Assistant:


> Do not overload the context window — consider trimming older history entries if needed.

---

### 1.4. Training Dataset

Fine-tuning is not yet available in-app but can be requested via [contact@xandimmersion.com](mailto:contact@xandimmersion.com).

You can train the model with:
- Lore documents
- NPC speech patterns
- World events and history

This enables **in-character** responses across all interactions.

---

### 1.5. Parameters

#### 1.5.1. Diagen LLM Parameters

Used via `START DIAGEN LOCAL`:

| Parameter           | Default       | Description |
|---------------------|---------------|-------------|
| Model Name          | `baseXI7.gguf`| GGUF model filename |
| Context Max Size    | `2048`        | Must be a power of 2 |
| GPU Layers          | `-1`          | Auto-detection |
| Flash Attention     | `true`        | HuggingFace optimization |
| GPU Select          | `-1`          | Useful for multi-GPU |
| Utilization         | `1.0`         | GPU usage ratio |
| Max GPU Size (GB)   | `1.0`         | Used for param resolution |
| Port                | `8002`        | Communication port |

![LLM Setup Example](/docs/images/chapter_1_img_0.png)

> 📌 See also: [4.1 Prompting the Model](#41-prompting-the-model)

---

#### 1.5.2. Diagen Prompt Parameters

Set per prompt, not per model:

| Parameter               | Default | Description |
|-------------------------|---------|-------------|
| N Predict               | `80`    | Max token count |
| Temperature             | `2.0`   | Controls creativity |
| Dynamic Temp Range      | `0.0`   | Random variation around temperature |
| Top-K                   | `40`    | Max token choices |
| Top-P                   | `0.95`  | Cumulative probability threshold |
| Cache Prompt            | `true`  | Reuses shared segments |
| Repeat Penalty          | `1.0`   | Prevents loops |
| Frequency Penalty       | `0.8`   | Penalizes frequent terms |
| Presence Penalty        | `0.3`   | Penalizes previous mentions |
| Stop Tokens             | `[]`    | List of stop strings |

> 📌 Use `Diagen Prompt AI Model (Raw)` for full control.

---

#### 1.5.3. Temperature

| Range | Behavior |
|-------|----------|
| 0.2   | Safe, predictable |
| 0.8   | Creative, diverse |
| 2.0   | Chaotic, imaginative |

Used to balance storytelling vs logic-based tasks.

---

#### 1.5.4. Context Size

Controls how much memory the model uses during generation.

- **Short (e.g. 512):** Efficient, faster responses  
- **Long (2048+):** Better for storytelling, conversations

> ⚠ Increasing context may slow down generation or break older models.

---

#### 1.5.5. Toxicity Filtering

Tuning to reduce unsafe content.

| Level  | Behavior |
|--------|----------|
| 0.0    | No filter |
| 1.0    | Fully sanitized |

> You may use external filters or LLM layers to assist.

---

## 2. Diagen Files and Testing in the App (NO UNREAL)

To manage NPC dialogue dynamically, Diagen uses four key CSV files. These files allow you to customize:

- Character behavior based on states
- Dialogue triggers and responses
- Event-based interactions

Once you're satisfied with your test results online, you can export the files and integrate them into Unreal.

---

### 2.1. Explanation of State Tags

State tags are used to "activate" or "deactivate" contextual information about an NPC. Tags reflect the current situation, emotional state, or location.

> _Example:_ `angry`, `in_Brevoy`, `quest_of_the_frozen_flame`

These tags control the content retrieved from the Character Information Table.

---

### 2.2. Character Information (CI)

The **Character Information CSV** contains multiple rows with:

| Field        | Description                                     |
|--------------|-------------------------------------------------|
| `name`       | Reference name for the description              |
| `stateTags`  | Required tag(s) for this description to apply   |
| `description`| The actual content (merged into the system prompt) |

The active descriptions are **concatenated** at runtime to form the NPC’s contextual prompt.

> ✅ Use this to define personality, location, emotional state, etc.

---

### 2.3. Topic Detection

The **Topic Detection CSV** defines which subjects the LLM can detect and respond to based on the active state tags.

| Field        | Description                             |
|--------------|-----------------------------------------|
| `name`       | Unique topic identifier                 |
| `stateTags`  | Required tags to enable detection       |
| `description`| Description of the topic for detection  |

> 🧠 The model compares user input to these topics and returns a match if relevant.

---

### 2.4. Diagen Event Files

**Event Files** define interactive events with consequences. Each event may change state tags, return data, and optionally display fixed responses.

| Field              | Description |
|--------------------|-------------|
| `name`             | Unique identifier |
| `stateTags`        | Required tags to activate |
| `sayVerbatim`      | Exact phrase said by the NPC |
| `instruction`      | AI-generated variation |
| `returnTrigger`    | Returned variable |
| `repeatable`       | If event can reoccur |
| `globalStateTags`  | If tag changes affect all NPCs |
| `enable/disable`   | State tag updates |
| `actionEvents`     | Functions to call on trigger |

This enables you to create conditional quests, dynamic relationships, and interactive world responses.

---

### 2.5. State Tags Weight

Used to prioritize which **descriptions** from the CI file appear first when multiple match.

| Field    | Description                    |
|----------|--------------------------------|
| `name`   | The state tag name             |
| `weight` | Priority (higher = more likely) |

> 📌 Affects prompt structure and relevance in dialogue generation.


## 3. Integration in Unreal

Diagen is built to work seamlessly in Unreal Engine (v5.2+). The system is designed to operate **locally** (on the player’s machine) or **remotely** (via external server) depending on available hardware.

> ✅ Minimum Requirements (for local execution):  
> NVIDIA graphics card with at least **4GB of VRAM** (as of Jan. 2025)

The plugin is available for download via your account on the [X&Immersion Platform](https://create.xandimmersion.com/).

---

### 3.1. How to Install the Diagen Plugin

> 📦 This section assumes you're using the Unreal Engine 5.2+ version.

---

#### 🔽 Step-by-step Installation

1. **Go to** [create.xandimmersion.com](https://create.xandimmersion.com/)  
   Navigate to the **Plug-ins** section and select **Diagen**.  
   *(Note: public download may not yet be available)*

2. **Download the plugin** that matches your UE version.

3. **Extract the plugin** into your Unreal project root folder:
YourUnrealProject/
└── Plugins/
└── Diagen/


4. **Open the project in Unreal Editor**.

If you see a message saying:

> "The plugin was compiled with a different engine version..."

✅ Click **Yes** to recompile the plugin if you have C++ tools installed.  
The editor should start after successful compilation.

---

#### 🔑 Enter your API Key

1. Go to `Edit > Project Settings > Plugins > Diagen`
2. Paste your API key and hit **Enter**

If the API key is **valid for local execution**, a message will appear asking if you want to download the model.

- Click **OK** to start download (you cannot use the editor during this)
- Click **Cancel** to skip; the prompt will reappear on next startup

Once the model is downloaded and installed:

✅ You’re ready to use Diagen!

## 4. Usage in Unreal

> ⚠️ Diagen **requires** the local executable to be installed and running.  
> Without it, none of the Diagen features will work in Unreal Engine.

---

### 4.1. Prompting the Model

By default, the **Diagen Local Executable** is not running.

You must explicitly start it using Blueprint nodes:

- `START DIAGEN LOCAL`
- `STOP DIAGEN LOCAL`
- `Get Diagen Local Executable Status` (pure)

> ✅ Recommended:  
> Use `BeginPlay` and `EndPlay` to manage startup/shutdown of the local model process.

Once the local model is running, you can send prompts to the LLM.

---

#### 🧠 Prompting Methods

Use the Blueprint node:  
**`Diagen Prompt AI Model (Raw)`**

This sends raw data directly to the LLM with **no internal formatting**.

If you prefer the other prompt types (`Conversation`, `Topic Detection`, etc.), you’ll need to use the node:  
**`Create Prompt`** first to build a complete prompt structure.

---

### 📷 Images for Prompting

![Begin/End Play Diagen Nodes](/docs/images/chapter_16_img_9.png)  
![Prompt AI Model (Raw)](/docs/images/chapter_16_img_10.png)  
![Create Prompt Node](/docs/images/chapter_16_img_11.png)  
![Generated Response Example](/docs/images/chapter_16_img_12.png)

---

### 4.2. Manage NPCs

In-game, the knowledge and context of NPCs may change.  
Instead of manually editing the system prompt, Diagen provides helper nodes to dynamically manage this logic.

NPC data is stored in a **SessionStates array**.

> 💡 Use a single shared SessionStates array to manage all NPCs.

---

#### 👤 NPC Management Nodes

| Action           | Node                      |
|------------------|---------------------------|
| Add NPC          | `Add NPC`                 |
| Remove NPC       | `Remove NPC`              |
| Reset NPC        | `Reset NPC`               |
| List NPCs        | `Get Session NPC Names`   |

---

#### 🧩 State Tags Control

To manage an NPC's state tags:

| Action            | Node                      |
|-------------------|---------------------------|
| Add tag(s)        | `Append NPC State Tags`   |
| Remove tag(s)     | `Remove NPC State Tags`   |
| Clear all tags    | `Clear NPC State Tags`    |
| Set new tags      | `Set NPC State Tags`      |
| Check tags        | `Get NPC Enabled State Tags` / `Contains NPC State Tags` |

> ⚠️ Do **not** use `Bind All State Tags to NPC` — this is deprecated.

---

### 📷 Images for NPC Management

![Add/Remove/Reset NPC Nodes](/docs/images/chapter_17_img_13.png)  
![Session State Tags Nodes](/docs/images/chapter_17_img_14.png)  
![Get/Contains Tag Nodes](/docs/images/chapter_17_img_15.png)  
![Deprecated Node Warning](/docs/images/chapter_17_img_16.png)

---



