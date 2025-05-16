# Session States

**[← API Reference](/docs/API_reference/README.md)**

## On this page

The following nodes can be used to manage the Diagen session states, containing all NPCs and their [attributes](#TODO) (tags, triggers, topcis, history, ...).

* [Add NPC](#add-npc) - *previously InitSession()*<br/>
* [Remove NPC](#remove-npc)<br/>
* [Reset NPC](#reset-npc)<br/>
* [Get Session NPC Names](#get-session-npc-names)<br/>
* [Save Session States](#save-session-states)<br/>
* [Load Session States](#load-session-states)<br/>
* <i style="color: red">**Deprecated**</i> - [Reset Session](#reset-session---deprecated)<br/>
* [Update Session Array](#update-session-array)<br/>
* [Update Session Int](#update-session-int)<br/>
* [Update Session String](#update-session-string)<br/>
* [Get Session Array](#get-session-array)<br/>
* [Get Session Int](#get-session-int)<br/>
* [Get Session String](#get-session-string)<br/>
* [Reset History](#reset-history)<br/>
* [Update History](#update-history)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Add NPC

*Previous name: **Init Session***

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::AddNPC()
```

Add a new NPC to the session. If the NPC does already exist, reset the NPC data.

![Node Add NPC](/docs/images/node_add_npc.png)

### Parameters

| Name           | Type           | Default value      | Description |
| -------------  | -------------- | ------------------ | ----------- |
| Session States | TArray<[FSessionState](#TODO)>& | - | The current session states |
| NPC Name       | const FString& | *empty string*     | The name of the NPC to be added |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Remove NPC

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::RemoveNPC()
```

Remove an NPC from the session. If the NPC is not in the session, does nothing.

![Node Remove NPC](/docs/images/node_remove_npc.png)

### Parameters

| Name           | Type           | Default value      | Description |
| -------------  | -------------- | ------------------ | ----------- |
| Session States | TArray<[FSessionState](#TODO)>& | - | The current session states |
| NPC Name       | const FString& | *empty string*     | The name of the NPC to be removed |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Reset NPC

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::ResetNPC()
```

Reset an NPC from the session. If the NPC is not in the session, does nothing.

![Node Reset NPC](/docs/images/node_reset_npc.png)

### Parameters

| Name           | Type           | Default value      | Description |
| -------------  | -------------- | ------------------ | ----------- |
| Session States | TArray<[FSessionState](#TODO)>& | - | The current session states |
| NPC Name       | const FString& | *empty string*     | The name of the NPC to be reset |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get Session NPC Names

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::GetSessionNpcs()
```

Get the list of all NPCs defined in the current session.

![Node Get NPC names](/docs/images/node_get_session_npc_names.png)

### Parameters

| Name           | Type           | Default value      | Description |
| -------------  | -------------- | ------------------ | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states |

### Return Value

| Name          | Type             | Description |
| ------------- | ---------------- | ----------- |
| Out NPC Names | TArray\<FString>& | The list of all NPC in the session |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Save Session States

C++ Function: 
```cpp
static bool UDiagenSessionBPLibrary::SaveSessionStates()
```

Save the current session in 'Saved' dir.

![Node Save Session](/docs/images/node_save_session_states.png)

### Parameters

| Name           | Type           | Default value      | Description |
| -------------  | -------------- | ------------------ | ----------- |
| Save File Name | const FString& | *empty string*     | The save filename (extension is optional, default to .json) |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states |

### Return Value

| Name         | Type | Description |
| ------------ | ---- | ----------- |
| Return Value | bool | `true` if the session states has been saved, `false` otherwise |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Load Session States

C++ Function: 
```cpp
static bool UDiagenSessionBPLibrary::LoadSessionStates()
```

Load the current session from 'Saved' dir.

![Node Load Session](/docs/images/node_load_session_states.png)

### Parameters

| Name           | Type           | Default value      | Description |
| -------------  | -------------- | ------------------ | ----------- |
| Save File Name | const FString& | *empty string*     | The save filename (extension is optional, default to .json) |

### Return Value

| Name           | Type             | Description |
| -------------- | ---------------- | ----------- |
| Session States | TArray<[FSessionState](#TODO)>& | - | The loaded session states from the save file |
| Return Value | bool | `true` if the session states has been loaded, `false` otherwise |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Reset Session - <i style="color: red">**Deprecated**</i>

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::ResetSession()
```

> [!IMPORTANT]
> The function is deprecated. Use [Reset NPC](#reset-npc) instead.

Reset the current session for the NPC with the given [Session state table](#TODO).

![Node reset Session](/docs/images/node_reset_session.png)

### Parameters

| Name           | Type           | Default value      | Description |
| -------------  | -------------- | ------------------ | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states |
| Initial States | UDataTable* | `nullptr`    | [???](#TODO) Cannot be empty but not used in C++ code. Just put anything |
| NPC Name       | const FString& | *empty string*     | The name of the NPC to be reset |

### Return Value

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Initial States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Update Session Array

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::UpdateSessionArray()
```

Update the current session `TArray<FString>` [attribute](#TODO) for the given NPC. 

The following attributes can be used as an array of string:

* `send_trigger`
* `enable_topics`
* `executed_triggers`
* `history`

![Node Update Session Array](/docs/images/node_update_session_array.png)

### Parameters

| Name           | Type           | Default value       | Description |
| -------------  | -------------- | ------------------- | ----------- |
| Session States | TArray<[FSessionState](#TODO)>& | -  | The current session states  |
| NPC Name       | const FString& | *empty string*      | The NPC name to change the attribute |
| Attribute      | const [ESessionAttributeType](#TODO)& | The attribute to update (see valid array attributes above) |
| Value          | const TArray\<FString>& | *empty array* | The value to update the attribute with |
| Append         | const bool     | `false`             | If set to `true`, append the given array to the already existing one instead of replacing it . |

### Return Value

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |


<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Update Session Int

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::UpdateSessionInt()
```

Update the current session `int` [attribute](#TODO) for the given NPC. 

The following attributes can be used as an integer:

* *No session attribute are of type `int32` yet!*

![Node Update Session int](/docs/images/node_update_session_int.png)

### Parameters

| Name           | Type           | Default value       | Description |
| -------------  | -------------- | ------------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString& | *empty string*      | The NPC name to change the attribute |
| Attribute      | const [ESessionAttributeType](#TODO)& | The attribute to update (see valid array attributes above) |
| Value          | int32 | *empty array* | The value to update the attribute with |

### Return Value

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Update Session String

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::UpdateSessionString()
```

Update the current session `FString` [attribute](#TODO) for the given NPC. 

The following attributes can be used as a string:

* *No session attribute are of type `FString` yet!*

![Node Update Session String](/docs/images/node_update_session_string.png)

### Parameters

| Name           | Type           | Default value       | Description |
| -------------  | -------------- | ------------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString& | *empty string*      | The NPC name to change the attribute |
| Attribute      | const [ESessionAttributeType](#TODO)& | The attribute to update (see valid array attributes above) |
| Value          | const FString& | *empty string*      | The value to update the attribute with |

### Return Value

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get Session Array

C++ Function: 
```cpp
static TArray\<FString> UDiagenSessionBPLibrary::GetSessionArray()
```

Get the current session `TArray<FString>` [attribute](#TODO) for the given NPC. 

The following attributes can be used as an array of string:

* `send_trigger`
* `enable_topics`
* `executed_triggers`
* `history`

![Node Set Session Array](/docs/images/node_get_session_arrray.png)

### Parameters

| Name           | Type           | Default value        | Description |
| -------------  | -------------- | -------------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString& | *empty string*       | The NPC name to get the attribute from |
| Attribute      | const [ESessionAttributeType](#TODO)& | The attribute to get (see valid array attributes above) |

### Return Value

| Name          | Type              | Description           |
| ------------- | ----------------- | --------------------- |
| Return Value  | TArray\<FString>   | The attribute value   |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get Session Int

C++ Function: 
```cpp
static int32 UDiagenSessionBPLibrary::GetSessionInt()
```

Get the current session `int32` [attribute](#TODO) for the given NPC. 

The following attributes can be used as an integer:

* *No session attribute are of type `int32` yet!*

![Node Set Session Int](/docs/images/node_get_session_int.png)

### Parameters

| Name           | Type           | Default value        | Description |
| -------------  | -------------- | -------------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString& | *empty string*       | The NPC name to get the attribute from |
| Attribute      | const [ESessionAttributeType](#TODO)& | The attribute to get (see valid array attributes above) |

### Return Value

| Name          | Type              | Description           |
| ------------- | ----------------- | --------------------- |
| Return Value  | int32             | The attribute value   |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get Session String

C++ Function: 
```cpp
static FString UDiagenSessionBPLibrary::GetSessionString()
```

Get the current session `FString` [attribute](#TODO) for the given NPC. 

The following attributes can be used as a string:

* *No session attribute are of type `FString` yet!*

![Node Set Session String](/docs/images/node_get_session_string.png)

### Parameters

| Name           | Type           | Default value        | Description |
| -------------  | -------------- | -------------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString& | *empty string*       | The NPC name to get the attribute from |
| Attribute      | const [ESessionAttributeType](#TODO)& | The attribute to get (see valid array attributes above) |

### Return Value

| Name          | Type              | Description           |
| ------------- | ----------------- | --------------------- |
| Return Value  | FString           | The attribute value   |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Reset History

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::ResetHistory()
```

Clear the LLM conversation history for the given NPC. Does nothing if the NPC is not in the current session.

![Node Reset History](/docs/images/node_reset_history.png)

### Parameters

| Name           | Type           | Default value        | Description |
| -------------- | -------------- | -------------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString& | *empty string*       | The NPC name to reset the history |

### Return Value

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Update History

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::UpdateHistory()
```

Add the LLM conversation entry (user question + LLM response) to the history for the given NPC. If there are too many entries, remove the oldest one.

![Node Update History](/docs/images/node_update_history.png)

### Parameters

| Name           | Type           | Default value        | Description |
| -------------- | -------------- | -------------------- | ----------- |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states  |
| NPC Name       | const FString& | *empty string*       | The NPC name to update the history |
| Question       | const FString& | *empty string*       | The message prompted to the LLM model |
| Answer         | const FString& | *empty string*       | The response generated from the LLM model |
| Keep N Entries | const inr32    | `8`                  | The maximum amount of entries to keep in history. If there are more, the oldest entry will be removed | 

### Return Value

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |