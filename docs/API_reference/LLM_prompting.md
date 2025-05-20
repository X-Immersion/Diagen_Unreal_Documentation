# LLM Prompting

**[← API Reference](/docs/API_reference/README.md)**

## On this page

The following nodes can be used to prompt the LLM model for a given task (conversation, topic detection, topic validation) or by giving all the LLM parameters (raw).

* [Create Prompt](#create-prompt)<br/>
* [Diagen Prompt AI model (Conversation)](#diagen-prompt-ai-model-conversation)<br/>
* [Diagen Prompt AI model (Raw)](#diagen-prompt-ai-model-raw)<br/>
* [Diagen Prompt AI model (Topic detection)](#diagen-prompt-ai-model-topic-detection)<br/>
* [Diagen Prompt AI model (Topic validation)](#diagen-prompt-ai-model-topic-validation)<br/>
* [Diagen LLM Topic Detection](#diagen-llm-topic-detection)<br/>
* [Diagen LLM Topic Validation](#diagen-llm-topic-validation)<br/>
* [Instruction to Verbatime](#instruction-to-verbatime)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Create Prompt

C++ Function: 
```cpp
static void UDiagenLlmBPLibrary::CreatePrompt()
```

Create a LLM prompt for the given NPC, based on the current [Session](./Classes_structs_enums.md#session-state). The NPC prompt history is included (if any). The [prompt](./Classes_structs_enums.md#prompt-message) output array can then be used with the nodes [Diagen Prompt AI model (Conversation)](#diagen-prompt-ai-model-conversation) and [Instruction to Verbatime](#instruction-to-verbatime).

![Node Create Prompt](/docs/images/node_create_prompt.png)

### Parameters

| Name                  | Type           | Default value     | Description |
| --------------------- | -------------- | ----------------- | ----------- |
| Session States        | const TArray<[FSessionState](./Classes_structs_enums.md#session-state)>& | - | The current session state array |
| NPC Name              | const FString& | *empty string*    | The name of the NPC. It must have been added to the session |
| Message               | const FString& | *empty string*    | The message prompted to the LLM |
| Character Information | UDataTable*    | `nullptr`         | The [CI table](./Classes_structs_enums.md#character-information-table-ci-table) used to create the NPC system prompt |
| Overwrite Description | const FString& | *empty string*    | If provided, override the system prompt with the given value |
| Max Characters        | const int32    | `0`               | The system prompt max character. Have no effect if `Overwrite Description` is provided |

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Prompt        | TArray<[FPromptMessage](./Classes_structs_enums.md#prompt-message)>& | The generated prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen Prompt AI model (Conversation)

C++ Function: 
```cpp
static FGuid UDiagenLlmBPLibrary::Prompt()
```

Prompt the LLM model with the given prompt messages. If Diagen executable is busy, the prompt will be added to a queue and automatically processed by the LLM when available. When the LLM response have been generated, the event [On Response](./Delegates.md#on-diagen-response) will be executed. You can use the node [Bind Event to Diagen Stream](./Stream.md#bind-event-to-diagen-stream) with the event [On Diagen Stream Response Part](./Delegates.md#on-diagen-stream-response-part) to get the LLM stream response.

![Node Diagen Prompt AI model Conversation](/docs/images/node_diagen_prompt_ai_model_conversation.png)

### Parameters

| Name                  | Type           | Default value        | Description |
| --------------------- | -------------- | -------------------- | ----------- |
| Prompt                | const TArray<[FPromptMessage](./Classes_structs_enums.md#prompt-message)>& | - | The system prompt, prompt history *(optional)* and prompt message |
| Diagen Prompt Config  | const [FDiagenPromptConfig](./Classes_structs_enums.md#diagen-prompt-config)& | *default prompt config* | The LLM prompt configuration |
| Optional GUID         | const FGuid&  | `{00000000-0000-0000-0000-000000000000}` | Force to use a specific GUID with this prompting. If not set or invalid, a new GUID will be generated and returned |
| Logs                  | const bool    | `true`                | Indicate if UE logs should be printed to the console |
| On Response           | const [FOnDiagenResponse](./Delegates.md#on-diagen-response) | -  |  Delegate event called when the model have generated the sentence (or if an error occured). |

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Return Value  | FGuid       | The GUID used for this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen Prompt AI model (Raw)

C++ Function: 
```cpp
static FGuid UDiagenLlmBPLibrary::PromptRaw()
```

Prompt the LLM model with the given prompt parameters. If Diagen executable is busy, the prompt will be added to a queue and automatically processed by the LLM when available. When the LLM response have been generated, the event [On Response](./Delegates.md#on-diagen-response) will be executed. You can use the node [Bind Event to Diagen Stream](./Stream.md#bind-event-to-diagen-stream) with the event [On Diagen Stream Response Part](./Delegates.md#on-diagen-stream-response-part) to get the LLM stream response.

![Node Diagen Prompt AI model Raw](/docs/images/node_diagen_prompt_ai_model_raw.png)

### Parameters

| Name                  | Type           | Default value         | Description |
| --------------------- | -------------- | --------------------- | ----------- |
| System Prompt         | const FString& | *empty string*        | The system prompt used |
| User Prompt History   | const TArray\<FString>& | *empty array* | The user prompt history (previous prompts for same context). Can be empty. |
| LLM Response History  | const TArray\<FString>& | *empty array* |  The LLM response history (previous responses for same context). Can be empty. |
| Prompt                | const FString& | *empty string*        | The current user prompt |
| Diagen Prompt Config  | const [FDiagenPromptConfig](./Classes_structs_enums.md#diagen-prompt-config))& | *default prompt config* | The LLM prompt configuration |
| Optional GUID         | const FGuid&  | `{00000000-0000-0000-0000-000000000000}` | Force to use a specific GUID with this prompting. If not set or invalid, a new GUID will be generated and returned |
| Logs                  | const bool    | `true`                 | Indicate if UE logs should be printed to the console |
| On Response           | const [FOnDiagenResponse](./Delegates.md#on-diagen-response) | -   |  Delegate event called when the model have generated the sentence (or if an error occured). |

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Return Value  | FGuid       | The GUID used for this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen Prompt AI model (Topic detection)

C++ Function: 
```cpp
static FGuid UDiagenLlmBPLibrary::PromptTopic()
```

> [!IMPORTANT]  
> In most scenarios, do not use this node directy but instead use [Diagen LLM Topic Detection](#diagen-llm-topic-detection). The node will internaly call this function.

Prompt the LLM model for topic detection. If Diagen executable is busy, the prompt will be added to a queue and automatically processed by the LLM when available. When the LLM response have been generated, the event [On Response](./Delegates.md#on-diagen-topic-response) will be executed.

![Node Diagen Prompt AI model Topic Detection](/docs/images/node_diagen_prompt_ai_model_topic_detection.png)

### Parameters

| Name                  | Type           | Default value         | Description |
| --------------------- | -------------- | --------------------- | ----------- |
| Prompt                | const TArray<[FPromptMessage](./Classes_structs_enums.md#prompt-message)>& | - | The system prompt (for topic detection) and prompt message |
| Topic Pairs           | const TArray<[FTopicTriggerPair](./Classes_structs_enums.md#topic-trigger-pair)>& | - | The list of topics to detect |
| Diagen Prompt Config  | const [FDiagenPromptConfig](./Classes_structs_enums.md#diagen-prompt-config))& | *default prompt config* | The LLM prompt configuration |
| Optional GUID         | const FGuid&  | `{00000000-0000-0000-0000-000000000000}` | Force to use a specific GUID with this prompting. If not set or invalid, a new GUID will be generated and returned |
| Logs                  | const bool    | `true`                 | Indicate if UE logs should be printed to the console |
| On Response           | const [FOnTopicResponse](./Delegates.md#on-diagen-topic-response) | -   |  Delegate event called when the model have generated the sentence (or if an error occured). |

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Return Value  | FGuid       | The GUID used for this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen Prompt AI model (Topic validation)

C++ Function: 
```cpp
static FGuid UDiagenLlmBPLibrary::PromptTopicValidation()
```

> [!IMPORTANT]  
> In most scenarios, do not use this node directy but instead use [Diagen LLM Topic Validation](#diagen-llm-topic-validation). The node will internaly call this function.

Prompt the LLM model for topic validation. If Diagen executable is busy, the prompt will be added to a queue and automatically processed by the LLM when available. When the LLM response have been generated, the event [On Response](./Delegates.md#on-diagen-topic-validation-response) will be executed.

![Node Diagen Prompt AI model Topic Validation](/docs/images/node_diagen_prompt_ai_model_topic_validation.png)

### Parameters

| Name                  | Type           | Default value         | Description |
| --------------------- | -------------- | --------------------- | ----------- |
| Prompt                | const TArray<[FPromptMessage](./Classes_structs_enums.md#prompt-message)>& | - | The system prompt (for topic validation) and prompt message |
| Topic Pairs           | const [FTopicTriggerPair](./Classes_structs_enums.md#topic-trigger-pair)& | -  | The detected topic that needs to be validated |
| Diagen Prompt Config  | const [FDiagenPromptConfig](./Classes_structs_enums.md#diagen-prompt-config))& | *default prompt config* | The LLM prompt configuration |
| Optional GUID         | const FGuid&  | `{00000000-0000-0000-0000-000000000000}` | Force to use a specific GUID with this prompting. If not set or invalid, a new GUID will be generated and returned |
| Logs                  | const bool    | `true`                 | Indicate if UE logs should be printed to the console |
| On Response           | const [FOnTopicValidationResponse](./Delegates.md#on-diagen-topic-validation-response) | -   |  Delegate event called when the model have generated the sentence (or if an error occured). |

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Return Value  | FGuid       | The GUID used for this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen LLM Topic Detection

C++ Function: 
```cpp
static FGuid UDiagenTopicBPLibrary::CallLlmTopicDetection()
```

Prompt the LLM model for topic detection. If Diagen executable is busy, the prompt will be added to a queue and automatically processed by the LLM when available. When the LLM response have been generated, the event [On Response](./Delegates.md#on-diagen-topic-response) will be executed.

![Node Diagen LLM Topic Detection](/docs/images/node_diagen_llm_topic_detection.png)

### Parameters

| Name              | Type           | Default value         | Description |
| ----------------- | -------------- | --------------------- | ----------- |
| Sentence          | const FString& | *empty string*        | The input sentence of a conversation to detect the topic from |
| NPC Name          | const FString& | *empty string*        | The name of the NPC |
| Speaker Name      | const FString& | *empty string*        | The name of speaking person. Can be either the Player or the NPC, depending on which topic you want to detect |
| Session States    | const TArray<[FPromptMessage](./Classes_structs_enums.md#prompt-message)>& | - | The current session state array |
| Topics Table      | UDataTable*    | `nullptr`             | The [Topic table](./Classes_structs_enums.md#topic-table) containing the topics |
| Optional GUID     | const FGuid&   | `{00000000-0000-0000-0000-000000000000}` | Force to use a specific GUID with this prompting. If not set or invalid, a new GUID will be generated and returned |
| Logs              | const bool     | `true`                | Indicate if UE logs should be printed to the console
| On Response       | const [FOnTopicResponse](./Delegates.md#on-diagen-topic-response)& | -   | Delegate event called when the model have generated the sentence (or if an error occured).

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Return Value  | FGuid       | The GUID used for this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen LLM Topic Validation

C++ Function: 
```cpp
static FGuid UDiagenTopicBPLibrary::CallLlmValidateTopicDetection()
```

Prompt the LLM model for topic validation. If Diagen executable is busy, the prompt will be added to a queue and automatically processed by the LLM when available. When the LLM response have been generated, the event [On Response](./Delegates.md#on-diagen-topic-validation-response) will be executed.

![Node Diagen LLM Topic Validation](/docs/images/node_diagen_llm_topic_validation.png)

### Parameters

| Name              | Type           | Default value         | Description |
| ----------------- | -------------- | --------------------- | ----------- |
| Sentence          | const FString& | *empty string*        | The input sentence of a conversation to validate the topic from |
| Topic Index       | const FString& | *empty string*        | The index of the topic to validate (response from Topic Detection) | 
| Speaker Name      | const FString& | *empty string*        | The name of speaking person. Can be either the Player or the NPC, depending on which topic you want to validate |
| Topic Pairs       | const TArray<[FTopicTriggerPair](./Classes_structs_enums.md#topic-trigger-pair)>& | *empty array* | The list of topics to validate (response from Topic Detection) |
| Optional GUID     | const FGuid&   | `{00000000-0000-0000-0000-000000000000}` | Force to use a specific GUID with this prompting. If not set or invalid, a new GUID will be generated and returned |
| Logs              | const bool     | `true`                | Indicate if UE logs should be printed to the console
| On Response       | const [FOnTopicValidationResponse](./Delegates.md#on-diagen-topic-validation-response)& | -   | Delegate event called when the model have generated the sentence (or if an error occured).

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Return Value  | FGuid       | The GUID used for this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Instruction to Verbatime

C++ Function: 
```cpp
static FGuid UDiagenTriggerBPLibrary::InstructionToVerbatime()
```

Prompt the LLM model to transform an instruction to a verbatim. If Diagen executable is busy, the prompt will be added to a queue and automatically processed by the LLM when available. When the LLM response have been generated, the event [On Response](./Delegates.md#on-diagen-response) will be executed. You can use the node [Bind Event to Diagen Stream](./Stream.md#bind-event-to-diagen-stream) with the event [On Diagen Stream Response Part](./Delegates.md#on-diagen-stream-response-part) to get the LLM stream response.

![Node Instruction to Verbatime](/docs/images/node_instruction_to_verbatime.png)

### Parameters

| Name                  | Type           | Default value         | Description |
| --------------------- | -------------- | --------------------- | ----------- |
| Prompt                | const TArray<[FPromptMessage](./Classes_structs_enums.md#prompt-message)>& | - | The system prompt. Prompt history and user message will be ignored |
| Instruction           | const FString& | *empty string*        | The instruction to convert to verbatim |
| Diagen Prompt Config  | const [FDiagenPromptConfig](./Classes_structs_enums.md#diagen-prompt-config))& | *default prompt config* | The LLM prompt configuration |
| Optional GUID         | const FGuid&  | `{00000000-0000-0000-0000-000000000000}` | Force to use a specific GUID with this prompting. If not set or invalid, a new GUID will be generated and returned |
| Logs                  | const bool    | `true`                 | Indicate if UE logs should be printed to the console |
| On Response           | const [FOnDiagenResponse](./Delegates.md#on-diagen-response) | -   |  Delegate event called when the model have generated the sentence (or if an error occured). |

### Return values

| Name          | Type        | Description |
| ------------- | ----------- | ----------- |
| Return Value  | FGuid       | The GUID used for this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>
