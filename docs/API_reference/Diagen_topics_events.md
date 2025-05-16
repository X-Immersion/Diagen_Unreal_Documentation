# Local Executable

**[← API Reference](/docs/API_reference/README.md)**

## On this page

The following nodes can be used to manage Diagen topics and events *(not Unreal events!)*.

* [Enable NPC Topic(s)](#enable-npc-topics)<br/>
* [Get NPC Enable Topic(s)](#get-npc-enable-topics)<br/>
* [Update Enabled Topics](#update-enabled-topics)<br/>
* [Trigger Diagen Event](#trigger-diagen-event)<br/>
* [List Available Events](#list-available-events)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Enable NPC Topic(s)

C++ Function: 
```cpp
static void UDiagenTopicBPLibrary::EnableNPCTopics()
```

Define enable topics for the given NPC on the current session.

![Node Enable NPC Topics](/docs/images/node_enable_npc_topics.png)

### Parameters

| Name           | Type                       | Default value  | Description |
| -------------- | -------------------------- | -------------- | ----------- |
| NPC Name       | const FString&             | *empty string* | The NPC name to enable the topic(s) |
| Session States | const TArray<[FSessionState](#TODO)>& | -   | The current session states  |
| Topic Table    | const UDataTable* | `nullptr`      | The [Topic table](#TODO) contains all topics | 

### Return values

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get NPC Enable Topic(s)

C++ Function: 
```cpp
static void UDiagenTopicBPLibrary::GetNPCEnabledTopics()
```

Get enabled topics for the given NPC on the current session.

![Node get NPC enable topics](/docs/images/node_get_npc_enable_topics.png)

### Parameters

| Name           | Type                       | Default value  | Description |
| -------------- | -------------------------- | -------------- | ----------- |
| NPC Name       | const FString&             | *empty string* | The NPC name to get enabled topic(s) |
| Session States | const TArray<[FSessionState](#TODO)>& | -   | The current session states  |

### Return values

| Name          | Type            | Description                |
| ------------- | --------------- | -------------------------- |
| Enable Topics | TArray\<FName>& | The list of enabled topics |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Update Enabled Topics

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::UpdateEnabledTopics()
```

Enable or diable the topics for the given NPC on the current session.

![Node Update Enabled Topics](/docs/images/node_update_enabled_topics.png)

### Parameters

| Name           | Type                     | Default value  | Description |
| -------------- | ------------------------ | -------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString&           | *empty string* | The NPC name to enable/disble topics |
| Topics         | const TArray\<FString>&   | -              | The list of topics to enable/disable |
| Enable         | const bool               | `false`        | Enable or disable the topics |
| Only First     | const bool               | `false`        | If disable topics, only remove the first topic in topics from state enable topics |

### Return values

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Trigger Diagen Event

C++ Function: 
```cpp
static void UDiagenTriggerBPLibrary::TriggerDiagenEvent()
```

Try to trigger a Diagen event, and return the event data if successful.

![Node Trigger Diagen Event](/docs/images/node_trigger_diagen_event.png)

### Parameters

| Name           | Type            | Default value  | Description |
| -------------- | --------------- | -------------- | ----------- |
| Event Name     | const FString&  | *empty string* | The event name (must match the row name in the [Event table](#TODO)) |
| NPC Name       | const FString&  | *empty string* | The NPC name to trigger the event |
| Diagen Events  | UDataTable*     | `nullptr`      | The [Event table](#TODO) with the Diagen events | 
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |

### Return values

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |
| Verbatime              | FString&                        | The static vebatim |
| Instruction            | FString&                        | The instruction that can then be used with the node [Instruction to Verbatime](./LLM_prompting.md#instruction-to-verbatime) | 
| Return Event           | FString&                        | The event 'return trigger' column value |
| Error                  | FString&                        | The error occurred while triggering the Diagen event (if any) | 

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## List Available Events

C++ Function: 
```cpp
static TArray\<FString> UDiagenTriggerBPLibrary::ListAvailableEvents()
```

List all available events for the given NPC based on the current session.

![Node List available Events](/docs/images/node_list_available_events.png)

### Parameters

| Name           | Type            | Default value  | Description |
| -------------- | --------------- | -------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString&  | *empty string* | The NPC name to find the events |
| Diagen Events  | UDataTable*     | `nullptr`      | The [Event table](#TODO) with the Diagen events | 


### Return values

| Name         | Type             | Description                |
| ------------ | ---------------- | -------------------------- |
| Return Value | TArray\<FString> | The list of all events that can be triggerred to the NPC  |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>
