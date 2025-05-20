# DIAGEN for Unreal

A high-quality, local-first dialogue generation plugin for Unreal Engine (5.2+), powered by LLMs.

---

## Table of Contents

- [Quickstart](/docs/Quickstart.md)
  - [Installation](/docs/Quickstart.md#installation)
  - [Usage](/docs/Quickstart.md#usage)
- [Explication about LLM](/docs/LLM.md)  
  - [Description (System Prompt)](/docs/LLM.md#description-system-prompt)  
  - [Input (User Prompt)](/docs/LLM.md#input-user-prompt)  
  - [History](/docs/LLM.md#history)  
  - [Training Dataset](/docs/LLM.md#training-dataset)  
  - [Parameters](/docs/LLM.md#parameters)  
    - [Diagen LLM Parameters](/docs/LLM.md#diagen-llm-parameters)  
    - [Diagen Prompt Parameters](/docs/LLM.md#diagen-prompt-parameters)  
    - [Temperature](/docs/LLM.md#temperature)  
    - [Context Size](/docs/LLM.md#context-size)  
    - [Toxicity Filtering](/docs/LLM.md#toxicity-filtering)  
- [Diagen CSV Files](/docs/CSV.md)  
   - [Explanation of State Tags](/docs/CSV.md#explanation-of-state-tags)  
   - [Character Information (CI)](/docs/CSV.md#character-information-ci)  
   - [Topic Detection](/docs/CSV.md#topic-detection)  
   - [Diagen Event Files](/docs/CSV.md#diagen-event-files)  
   - [State Tags Weight](/docs/CSV.md#state-tags-weight)  
- [API Reference](/docs/API_reference/README.md)
  - [LLM Prompting](/docs/API_reference/LLM_prompting.md)
  - [Local Executable](/docs/API_reference/Local.md)
  - [Stream](/docs/API_reference/Stream.md)
  - [Diagen Session](/docs/API_reference/Diagen_session.md)
  - [Diagen Topics and Events](/docs/API_reference/Diagen_topics_events.md)
  - [Diagen State Tags](/docs/API_reference/Diagen_state_tags.md)
  - [Utilities](/docs/API_reference/Utilities.md)
  - [Delegates (Events)](/docs/API_reference/Delegates.md)
  - [Classes, structs and enums](/docs/API_reference/Classes_structs_enums.md)

### What is Diagen?

This tool is designed to craft dynamic and immersive dialogues that reflect the NPCs' knowledge and emotions. It supports three key use cases:
* **Player ↔ NPC Interaction:** Create engaging and responsive conversations between players and NPCs.
* **NPC ↔ NPC Interaction:** Develop authentic and contextually rich exchanges between NPCs.
* **Environment ↔ NPC Interaction:** Generate dialogues that respond to environmental cues or changes, enhancing world immersion.

![Diagen Ximm Logo](/docs/images/embedded_1_0.png)