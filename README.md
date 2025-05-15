
Trim old history to preserve tokens.

[Back to Table of Contents](#table-of-contents)

### 1.4. Training Dataset

Fine-tuning is currently unavailable in-app but can be arranged via [contact@xandimmersion.com](mailto:contact@xandimmersion.com).

Use custom lore, character backstories, and dialogue logs for more authentic responses.

[Back to Table of Contents](#table-of-contents)

### 1.5. Parameters

#### 1.5.1. Diagen LLM Parameters

Configure global LLM settings with `START DIAGEN LOCAL`:

![LLM Setup Example](docs/images/chapter_1_img_0.png)

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

[Back to Parameters](#15-parameters)

#### 1.5.2. Diagen Prompt Parameters

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

[Back to Parameters](#15-parameters)

#### 1.5.3. Temperature

| Value | Behavior                          |
|-------|-----------------------------------|
| `0.2` | Deterministic, focused            |
| `0.8` | Creative, varied                  |
| `2.0` | Novel, higher risk of incoherence |

[Back to Parameters](#15-parameters)

#### 1.5.4. Context Size

- **Short** (512): fast, concise  
- **Long** (2048+): detailed narratives  

Beware of token window limits.

[Back to Parameters](#15-parameters)

#### 1.5.5. Toxicity Filtering

| Level | Effect                         |
|-------|--------------------------------|
| `0.0` | No filtering                   |
| `1.0` | Strict safe content            |

Consider external moderation layers if needed.

[Back to Table of Contents](#table-of-contents)

---

## 2. Diagen Files and Testing in the App (NO UNREAL)

Use these CSV files to prototype NPC behavior before Unreal integration.

### 2.1. Explanation of State Tags

State tags enable/disable context for NPCs.

![State Tags Example](docs/images/chapter_7_img_1.png)

> Example: `angry`, `in_Brevoy`, `quest_of_the_frozen_flame`

[Back to Table of Contents](#table-of-contents)

### 2.2. Character Information (CI)

CSV fields:

- `name`: Identifier for description  
- `stateTags`: Comma-separated tags required  
- `description`: Text to include in system prompt  

![Character Information CSV Example](docs/images/chapter_10_img_2.png)

Descriptions merge at runtime based on active tags.

[Back to Table of Contents](#table-of-contents)

### 2.3. Topic Detection

Defines dialogue triggers based on user input and tags.

| Field        | Description                            |
|--------------|----------------------------------------|
| `name`       | Topic ID                               |
| `stateTags`  | Active tags needed to detect topic     |
| `description`| Text prompt used for detection         |

![Topic Detection CSV Example](docs/images/chapter_11_img_3.png)

[Back to Table of Contents](#table-of-contents)

### 2.4. Diagen Event Files

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

![Diagen Event CSV Example](docs/images/chapter_12_img_4.png)

[Back to Table of Contents](#table-of-contents)

### 2.5. State Tags Weight

Prioritize which CI descriptions take precedence.

| Field    | Description                    |
|----------|--------------------------------|
| `name`   | Tag name                       |
| `weight` | Priority (higher = more urgent)|

![State Tags Weight Example](docs/images/chapter_13_img_5.png)

[Back to Table of Contents](#table-of-contents)

---

## 3. Integration in Unreal

Diagen runs **locally** or **remotely** in UE5.2+.

> **Minimum**: NVIDIA GPU with ≥ 4 GB VRAM

### 3.1. How to Install the Diagen Plugin

1. Download from [create.xandimmersion.com](https://create.xandimmersion.com/)  
2. Place under `YourProject/Plugins/Diagen/`  
3. Launch Unreal Editor  
4. In `Edit > Project Settings > Plugins > Diagen`, paste your API Key  
5. Confirm download of local model

![Unreal Plugin Install Prompt](docs/images/chapter_15_img_6.png)

[Back to Table of Contents](#table-of-contents)

---

## 4. Usage in Unreal

> **Diagen requires** the local executable.

### 4.1. Prompting the Model

Use `BeginPlay` / `EndPlay` to manage the local process:

- `START DIAGEN LOCAL`  
- `STOP DIAGEN LOCAL`  
- `Get Diagen Local Executable Status` (pure)

Send prompts with:

![BeginPlay/EndPlay Nodes](docs/images/chapter_16_img_9.png)

- **Raw**: `Diagen Prompt AI Model (Raw)`  
  ![Prompt AI Model Raw](docs/images/chapter_16_img_10.png)

- **Structured**: use `Create Prompt` before other prompt nodes  
  ![Create Prompt Node](docs/images/chapter_16_img_11.png)

Streamed response:

![Generated Response Example](docs/images/chapter_16_img_12.png)

[Back to Table of Contents](#table-of-contents)

### 4.2. Manage NPCs

Use a single shared **SessionStates** array for all NPCs.

#### NPC Lifecycle

| Action      | Blueprint Node            |
|-------------|---------------------------|
| Add NPC     | `Add NPC`                 |
| Remove NPC  | `Remove NPC`              |
| Reset NPC   | `Reset NPC`               |
| List NPCs   | `Get Session NPC Names`   |

![Add/Remove/Reset NPC Nodes](docs/images/chapter_17_img_13.png)

#### State Tag Management

| Action             | Blueprint Node                  |
|--------------------|---------------------------------|
| Append tag(s)      | `Append NPC State Tags`         |
| Remove tag(s)      | `Remove NPC State Tags`         |
| Clear all tags     | `Clear NPC State Tags`          |
| Set new tags       | `Set NPC State Tags`            |
| Query tags         | `Get NPC Enabled State Tags` / `Contains NPC State Tags` |

![Session State Tags Nodes](docs/images/chapter_17_img_14.png)  
![Get/Contains Tag Nodes](docs/images/chapter_17_img_15.png)  

> ⚠️ `Bind All State Tags to NPC` is deprecated.  
> ![Deprecated Node Warning](docs/images/chapter_17_img_16.png)

[Back to Table of Contents](#table-of-contents)
