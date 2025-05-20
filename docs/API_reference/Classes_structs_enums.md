# [UCLASS()](#classes---uclass), [USTRUCT()](#structures---ustruct) and [UENUM()](#enumerations---uenum)

**[← API Reference](/docs/API_reference/README.md)**

## On this page

Here you can find details about C++ classes, structs and enums that can be used in Blueprints.

* [Classes](#classes---uclass)<br/>
    * [Diagen Plugin Settings](#diagen-plugin-settings)<br/>

* [Structs](#structures---ustruct)<br/> 
    * [Diagen Subsystem Config](#diagen-subsystem-config)<br/>
    * [Diagen Prompt Config](#diagen-prompt-config)<br/>
    * [Prompt Message](#prompt-message)<br/>
    * [NPC Description Priority](#npc-description-priority)<br/>
    * [Session State](#session-state)<br/>
    * [Topic Trigger Pair](#topic-trigger-pair)<br/>

* [Structs - Data Table Row](#structures-for-data-table---ustruct)<br/>
    * [Character Information Table (CI Table)](#character-information-table-ci-table)<br/>
    * [Diagen Event Table](#diagen-event-table)<br/>
    * [Topic Table](#topic-table)<br/>
    * [State Tags Weight Table](#state-tags-weights-table)<br/>
    * <i style="color: red">**Deprecated**</i> - [Trigger Option Table](#trigger-option-table---deprecated)<br/>
    * <i style="color: red">**Deprecated**</i> - [Prefix Option Table](#prefix-option-table----deprecated)<br/>
    * <i style="color: red">**Deprecated**</i> - [Suffix Option Table](#suffix-option-table----deprecated)<br/>
    * <i style="color: red">**Deprecated**</i> - [Initial Session States Table](#initial-session-states-table----deprecated)<br/>

* [Enums](#enumerations---uenum)<br/>
    * [Diagen Subsystem Status](#diagen-subsystem-status)<br/>
    * [Session Attribute Type](#session-attribute-type)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

# Classes - UCLASS()

The following classes can be used in blueprint, as an Unreal UObject.

## Diagen Plugin Settings

C++ Declaration: 
```cpp
ULCASS(BlueprintType, DefaultConfig)
class DIAGEN_API UDiagenPluginSettings : public UDeveloperSettings {...}
```

This class is used to handle the plugin settings that can be changed through the Unreal Editor.

> [!TIP]
> Go to *Edit* > *Project Settings...* > *Plugins* > *Diagen* to change the plugin settings. If you change your API-key, your local executable rights will be checked. 

![Diagen Plugin Settings Set](/docs/images/class_diagen_plugin_settings_2.png)

<br/>

> [!TIP]
> Use the node **Get Defaults** to retrieve the Diagen plugin settings within your Blueprints (if needed). Select *Diagen* as the class to get defaults for.

![Diagen Plugin Settings Get](/docs/images/class_diagen_plugin_settings.png)

### Variables

| Name          | Type          | Editor        | Blueprint | Default value     | Description           |
| ------------- | ------------- | ------------- | --------- | ----------------- | --------------------- |
| Api Endpoint  | FString       | Edit Anywhere | Read-only | `https://diagen-api.xandimmersion.com/` | The Diagen API endpoint. This is only used to verify you licence validity!       |
| Api-Key       | FString       | Edit Anywhere | Read-only | *empty string*    | The Diagen API key.   |

<!------------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

# Structures - USTRUCT()

The following structs can be used in blueprint, as a variable.

## Diagen Subsystem Config

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct FDiagenSubsystemConfig {...}
```

This struct is used to set all parameters for the Diagen executable startup, using the node [Start Diagen Local Executable (START DIAGEN LOCAL)](./Local.md#start-diagen-local-executable). 

![Struct Subsystem Config](/docs/images/struct_diagen_subsystem_config.png)

### Variables

| Name              | Type      | Editor        | Blueprint  | Default value        | Description           |
| ----------------- | --------- | ------------- | ---------- | -------------------- | --------------------- |
| ModelName         | FString   | Edit Anywhere | Read+Write | `baseXI7.gguf`       | The GGUF model filename. The model must be placed in Plugins/Diagen/Local/models |
| Context Max Size  | int32     | Edit Anywhere | Read+Write | `2048`               | The size of the whole prompt context. Do not use a value higher than then one used to train the LLM model |
| GPU Layers        | int32     | Edit Anywhere | Read+Write | `-1` *(auto select)* | The amount of layers that will be offloaded to the GPU |
| Flash Attention   | bool      | Edit Anywhere | Read+Write | `true`               | Use flash attention algorithm. [More info](https://huggingface.co/docs/text-generation-inference/conceptual/flash_attention) |
| GPU Select        | int32     | Edit Anywhere | Read+Write | `-1` *(auto select)* | The GPU used by the LLM model. Can be useful in case of multiple GPU available |
| Utilization       | float     | Edit Anywhere | Read+Write | `1.0`                | This parameter is not used inside the plugin yet |
| Max GPU Size (GB) | float     | Edit Anywhere | Read+Write | `1.0`                | When the GPU parameters are set to -1, this value is used as sa *soft limit* to determine the GPU to use. You can use this parameter to ignore very large GPU selection if you have multiple |
| Port              | int32     | Edit Anywhere | Read+Write | `8002`               | The port used to communicate between the LLM and the game |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen Prompt Config

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct FDiagenPromptConfig {...}
```

This struct is used to specify the prompt configuration when using one of the LLM prompt nodes:
* [Diagen Prompt AI model (Conversation)](./LLM_prompting.md#diagen-prompt-ai-model-conversation)<br/>
* [Diagen Prompt AI model (Raw)](./LLM_prompting.md#diagen-prompt-ai-model-raw)<br/>
* [Diagen Prompt AI model (Topic detection)](#diagen-prompt-ai-model-topic-detection)<br/>
* [Diagen Prompt AI model (Topic validation)](#diagen-prompt-ai-model-topic-validation)<br/>
* [Instruction to Verbatime](./LLM_prompting.md#instruction-to-verbatime)<br/>

![Struct Prompt Config](/docs/images/struct_diagen_prompt_config.png)

### Variables

| Name              | Type      | Editor        | Blueprint  | Default value        | Description           |
| ----------------- | --------- | ------------- | ---------- | -------------------- | --------------------- |
| N Predict         | int32     | Edit Anywhere | Read+Write | `80`                 | The maximum length (in tokens) of the LLM response. If the LLM generation exceed this value, the generation will interrupt immediatly. Set it to `-1` for no limit |
| Temperature       | float     | Edit Anywhere | Read+Write | `0.8`                | Set the randomness of the generated text. It affects the probability distribution of the model's output tokens |
| Dyna temp range   | float     | Edit Anywhere | Read+Write | `0.0`                | Dynamic temperature range. Adjust the temperature according to the following formula: <br/> $[temperature - dynaTempRange; temperature + dynaTempRange]$  |
| Top K             | int32     | Edit Anywhere | Read+Write | `40`                 | Limit the next token selection to the K most probable tokens. Set it to `0` to disable sampling |
| Top P             | float     | Edit Anywhere | Read+Write | `0.95`               | Limit the next token selection to a subset of tokens with a cumulative probability above a threshold P. Set it to `1.0` to disable sampling |
| Cache Prompt      | bool      | Edit Anywhere | Read+Write | `true`               | Re-use common prefix prompting in KV cache from previous prompt requests if possible |
| Repeat Penalty    | float     | Edit Anywhere | Read+Write | `1.0`                | Control the repetition of token sequences in the generated text. Set it to `1.0` to disable repeat penalty |
| Frequency Penalty | float     | Edit Anywhere | Read+Write | `0.8`                | Repeat alpha frequency penalty. Set it to `0.0` to disable frequency penalty |
| Presence Penalty  | float     | Edit Anywhere | Read+Write | `0.3`                |  Repeat alpha presence penalty. Set it to `0.0` to disable presence penalty |
| Stop              | TArray\<FString> | Edit Anywhere | Read+Write | *empty array* | The list of stopping strings. When the LLM model generates an element that is on the list, the generation is immediately stopped and returned. Stop elements can be punctuation, characters, words or even sentences. Please note that the stop element will NOT be included in the response! |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Prompt Message

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct FPromptMessage {...}
```

This struct is used to contain one part of the prompt message, with its role. Most of the time, this is used within an array, like with the node [Diagen Prompt AI model (Conversation)](./LLM_prompting.md#diagen-prompt-ai-model-conversation).

![Struct Prompt Message](/docs/images/struct_prompt_message.png)

### Variables

| Name      | Type      | Editor        | Blueprint  | Default value    | Description           |
| --------- | --------- | ------------- | ---------- | ---------------- | --------------------- |
| Role      | FString   | Edit Anywhere | Read+Write | *empty string*   | The message prompt role associated. Can be `system`, `user` or `assistant` |
| Content   | int32     | Edit Anywhere | Read+Write | *empty string*   | The message content. |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## NPC Description Priority

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct FNpcDescriptionPriority {...}
```

This struct is used to sort all system prompt parts according to their description. More generally, it can be used with the node [Sort NPC Description Priority Array](./Utilities.md#sort-npc-description-priority-array) to sort an array of string based on the string priority (weight). 

![Struct NPC Description Priority](/docs/images/struct_npc_description_priority.png)

### Variables

| Name          | Type      | Editor        | Blueprint  | Default value    | Description           |
| ------------- | --------- | ------------- | ---------- | ---------------- | --------------------- |
| Description   | FString   | Edit Anywhere | Read+Write | *empty string*   | The string element    |
| Priority      | int       | Edit Anywhere | Read+Write | `0`                | The string weight (can be negative) |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Session State

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct FSessionState {...}
```

This struct is used to store all session information for one NPC. There are a lot of Diagen nodes that uses a session state array in order to read and write NPC information from/to the current session. 

![Struct Session State](/docs/images/struct_session_state.png)

### Variables

| Name              | Type                  | Editor        | Blueprint | Default value | Description                       |
| ----------------- | --------------------- | ------------- | --------- | ------------- | --------------------------------- |
| NPC Name          | FName                 | Edit Anywhere | Read-Only | *empty string*| The NPC name                      |
| Send Trigger      | TArray\<FName>        | Edit Anywhere | Read-Only | *empty array* | No information available for this |
| Enable State Tags | TArray\<FString>      | Edit Anywhere | Read-Only | *empty array* | The list of tags associated with this NPC (can change during game execution) |
| All State Tags    | TMap\<FString, int>   | Edit Anywhere | Read-Only | *empty array* | **DEPRECATED** - Do not use anymore! |
| Enable Topics     | TArray\<FName>        | Edit Anywhere | Read-Only | *empty array* | The list of topics associated with this NPC (can change during game execution) |
| Executed Diagen Event | TArray\<FName>    | Edit Anywhere | Read-Only | *empty array* | The list of Diagen events trigerred for this NPC (can change during game execution) |
| History           | TArray\<FString>      | Edit Anywhere | Read-Only | *empty array* | The NPC LLM messages and responses history |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Topic Trigger Pair

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct FTopicTriggerPair {...}
```

This struct is used to define the relationship between a topic and its trigger. 

![Struct Topic Trigger Pair](/docs/images/struct_topic_trigger_pair.png)

### Variables

| Name          | Type      | Editor        | Blueprint  | Description           |
| ------------- | --------- | ------------- | ---------- | --------------------- |
| Topic         | FString   | Edit Anywhere | Read-Write | The name of the topic (this is the raw name) |
| Trigger       | FString   | Edit Anywhere | Read+Write | The name of the trigger (return trigger) |
| Content       | FString   | Edit Anywhere | Read+Write | The topic description |

<!------------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

# Structures for Data Table - USTRUCT()

The following structs can be used in Data Table, as a row.

## Character Information Table (CI Table)

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FCharacterInformationTable : public FTableRowBase {...}
```

You can use this Data Table format to store the system prompt message parts related to the tags required in order to get the message part. <br/>

If you want to have more Data Table columns, like a weight, a NPC name (or multiple), a link to some UObjects or else, we do recommand to create your own Data Table structure (you can create it directly in Blueprint, not in C++) and then implement your own logic to create the system prompt based on one NPC and its variables.

![Struct CI Table](/docs/images/struct_ci_table.png)

### Variables

| Name          | Type      | Editor        | Blueprint  | Description           |
| ------------- | --------- | ------------- | ---------- | --------------------- |
| State Tags    | FString   | Edit Anywhere | Read-Only  | The list of tags, in a JSON array format. You can use a TArray\<FString> instead |
| Description   | FString   | Edit Anywhere | Read-Only  | The system prompt message part |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Diagen Event Table

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FDiagenEventsTable : public FTableRowBase {...}
```

You can use this Data Table format to store all information about a Diagen event. They are mostly used with the nodes [Trigger Diagen Event](./Diagen_topics_events.md#trigger-diagen-event) and [Instruction to Verbatime](./LLM_prompting.md#instruction-to-verbatime).

![Struct Event Table](/docs/images/struct_diagen_event_table.png)

### Variables

| Name                  | Type              | Editor        | Blueprint | Description           |
| --------------------- | ----------------- | ------------- | --------- | --------------------- |
| Say Verbatime         | FString           | Edit Anywhere | Read-Only | A sentence to says when the event is triggered. It replaces the instruction when it is set. |
| Instruction           | FString           | Edit Anywhere | Read-Only | The LLM instruction related to the event. You can use the node [Instruction to Verbatime](./LLM_prompting.md#instruction-to-verbatime) to generate a verbatim based on the instruction |
| Required State Tags   | TArray\<FString>  | Edit Anywhere | Read-Only | State tags required to list the event in the available list. Note that is does not prevent the event from being triggered |
| Return Trigger        | FString           | Edit Anywhere | Read-Only | The trigger returned by the event |
| Repeatable            | bool              | Edit Anywhere | Read-Only | Indicate if the event can be trigerred multiple time |
| Global State Tags     | bool              | Edit Anywhere | Read-Only | Indicate if this event should change the tags of all NPC or not |
| Enable State Tags     | FString           | Edit Anywhere | Read-Only | The JSON list of tags to enable when the event is triggered. You can use a TArray\<FString> instead |
| Diable State Tags     | FString           | Edit Anywhere | Read-Only | The JSON list of tags to diable when the event is triggered. You can use a TArray\<FString> instead |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Topic Table

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FTopicsTable : public FTableRowBase {...}
```

You can use this Data Table format to store all information about a Diagen topic. They are mostly used with the nodes [Enable NPC Topic(s)](./Diagen_topics_events.md#enable-npc-topics) and [Diagen LLM Topic Detection](./LLM_prompting.md#diagen-llm-topic-detection).

![Struct Topic Table](/docs/images/struct_topic_table.png)

### Variables

| Name          | Type      | Editor        | Blueprint | Description           |
| ------------- | --------- | ------------- | --------- | --------------------- |
| State Tags    | FString   | Edit Anywhere | Read-Only | The list of tags, in a JSON array format. You can use a TArray\<FString> instead |
| Description   | FString   | Edit Anywhere | Read-Only | The system prompt message part |
| Threshold     | float     | Edit Anywhere | Read-Only | The message weight |
| Return Trigger| FString   | Edit Anywhere | Read-Only | The trigger associated with this topic |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## State Tags Weights Table

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FStateTagWeightsTable : public FTableRowBase {...}
```

You can use this Data Table format to store the weight for a topic or an event. The row name must match the Diagen event/topic row name. You could also directly add this information into the respective Data Table.

![Struct State Tag Weight Table](/docs/images/struct_weight_table.png)

### Variables

| Name          | Type      | Editor        | Blueprint | Description           |
| ------------- | --------- | ------------- | --------- | --------------------- |
| Weight        | int       | Edit Anywhere | Read-Only | The event/topic weight. You must implement your own weight restriction(s) |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Trigger Option Table - <i style="color: red">**Deprecated**</i>

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FTriggerOptionsTable : public FTableRowBase {...}
```

You can use this Data Table format to store all information about a Diagen trigger. It is not directly used with the Diagen plugin, but you can use it for your own logic if needed. 

![Struct Trigger Table](/docs/images/struct_trigger_options_table.png)

### Variables

| Name          | Type              | Editor        | Blueprint | Description           |
| ------------- | ----------------- | ------------- | --------- | --------------------- |
| NPC           | FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Trigger Name  | FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Say Verbatime | TArray\<FString>  | Edit Anywhere | Read-Only | **Deprecated**        |
| Instruction   | TArray\<FString>  | Edit Anywhere | Read-Only | **Deprecated**        |
| Return Trigger| FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Repeatable    | bool              | Edit Anywhere | Read-Only | **Deprecated**        |
| Enable Prefix | FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Enable Suffix | TArray\<FString>  | Edit Anywhere | Read-Only | **Deprecated**        |
| Disable Suffix| TArray\<FString>  | Edit Anywhere | Read-Only | **Deprecated**        |
| Victory       | int32             | Edit Anywhere | Read-Only | **Deprecated**        |
| Defeat        | int32             | Edit Anywhere | Read-Only | **Deprecated**        |
| Chance        | TArray\<float>    | Edit Anywhere | Read-Only | **Deprecated**        |
| Diable Topics | TArray\<FString>  | Edit Anywhere | Read-Only | **Deprecated**        |
| Enable Topics | TArray\<FString>  | Edit Anywhere | Read-Only | **Deprecated**        |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Prefix Option Table  - <i style="color: red">**Deprecated**</i>

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FPrefixOptionsTable : public FTableRowBase {...}
```

You can use this Data Table format to store all information about Prefix option. It is not directly used with the Diagen plugin, but you can use it for your own logic if needed. 

![Struct Prefix Table](/docs/images/struct_prefix_table.png)

### Variables

| Name          | Type              | Editor        | Blueprint | Description           |
| ------------- | ----------------- | ------------- | --------- | --------------------- |
| NPC           | FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Prefix Content| FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Model Name    | FString           | Edit Anywhere | Read-Only | **Deprecated**        |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Suffix Option Table  - <i style="color: red">**Deprecated**</i>

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FSuffixOptionsTable : public FTableRowBase {...}
```

You can use this Data Table format to store all information about Suffix option. It is not directly used with the Diagen plugin, but you can use it for your own logic if needed. 

![Struct Suffix Table](/docs/images/struct_sufix_table.png)

### Variables

| Name          | Type              | Editor        | Blueprint | Description           |
| ------------- | ----------------- | ------------- | --------- | --------------------- |
| NPC           | FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Suffix Content| FString           | Edit Anywhere | Read-Only | **Deprecated**        |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Initial Session States Table  - <i style="color: red">**Deprecated**</i>

C++ Declaration: 
```cpp
USTRUCT(BlueprintType)
struct DIAGEN_API FinitialSessionStatesDT : public FTableRowBase {...}
```

You can use this Data Table format to store all information about initial states. It is not directly used with the Diagen plugin, but you can use it for your own logic if needed. 

![Struct Init State Table](/docs/images/struct_init_session_state.png)

### Variables

| Name          | Type              | Editor        | Blueprint | Description           |
| ------------- | ----------------- | ------------- | --------- | --------------------- |
| NPC           | FString           | Edit Anywhere | Read-Only | **Deprecated**        |
| Type          | FString           | Edit Anywhere | Read-Only | **Deprecated**        |

<!------------------------------------------------------------------------------------------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

# Enumerations - UENUM()

The following enums can be used in blueprint for multiple purpose (switch, variable, ...)

## Diagen Subsystem Status

C++ Declaration: 
```cpp
UENUM(BlueprintType)
enum class EDiagenSubsystemStatus : uint8 {...}
```

All status available for the Diagen local executable lifecycle.

![Enum Subsystem Status](/docs/images/enum_diagen_subsystem_status.png)

### Values

| Name          | Description                                                       |
| ------------- | ----------------------------------------------------------------- |
| None          | The status is undetermined (should never happens)                 |
| Idle          | The subsystem is not working, the LLM model is not started        |
| Starting      | The local executable is starting and the LLM model loading        | 
| Running       | The local executable have started, the LLM model is not generating|
| Prompting     | The local executable have started, the LLM model is generating    |
| Error         | The local executable is stopped because an error occured (see log)|

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Session Attribute Type

C++ Declaration: 
```cpp
UENUM(BlueprintType)
enum class ESessionAttributeType : uint8 {...}
```

All session variables types (names).

![Enum Subsystem Status](/docs/images/enum_session_attribute_type.png)

### Values

| Name              | Description                                                       |
| ----------------- | ----------------------------------------------------------------- |
| Send Trigger      | No information available. Type is `TArray<FName>`                 |
| Enable State Tags | List of tags associated. Type is `Tarray<FString>`                |
| All State Tags    | **Deprecated**. Type is `TMap<FString, int>`                      | 
| Enable Topics     | List of topics associated. Type is `TArray<FName>`                |
| History           | LLM prompting and response history. Type is `TArray<FString>`     |
| CI                | **Deprecated**. Type is `NULL`                                    |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>