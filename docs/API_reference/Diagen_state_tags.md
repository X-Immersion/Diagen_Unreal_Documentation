# Diagen State Tags

**[← API Reference](/docs/API_reference/README.md)**

## On this page

The following nodes can be used to manage the state tags in the current [session](#TODO) for the given NPC (the NPC must have been added to the session).

* [Append NPC State Tags](#append-npc-state-tags)<br/>
* [Remove NPC State Tags](#remove-npc-state-tags)<br/>
* [Clear NPC State Tags](#clear-npc-state-tags)<br/>
* [Contains NPC State Tags](#contains-npc-state-tags)<br/>
* [Get NPC State Tags](#get-npc-state-tags)<br/>
* [Set NPC State Tags](#set-npc-state-tags)<br/>
* <i style="color: red">**Deprecated**</i> - [Bind All State Tags to NPC](#deprecated---bind-all-state-tags-to-npc)<br/>
* <i style="color: red">**Deprecated**</i> - [Get NPC All State Tags](#deprecated---get-npc-all-state-tags)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Append NPC State Tags

C++ Function: 
```cpp
static void UDiagenStateTagsBPLibrary::AppendNPCStateTags()
```

Append the state tags with those already present for the given NPC on the current session. Uses [Set NPC State Tags](#set-npc-state-tags) if you want to replace the tags.

![Node Append NPC Tags](/docs/images/node_append_npc_state_tags.png)

### Parameters

| Name           | Type           | Default value            | Description |
| -------------- | -------------- | ------------------------ | ----------- |
| NPC Name       | const FString& | *empty string*           | The name of the NPC to append the tags |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states |
| State Tags     | const TArray\<FString>& | -               | The tags that will be append to the already existing NPC tags |

### Return values

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Remove NPC State Tags

C++ Function: 
```cpp
static void UDiagenStateTagsBPLibrary::RemoveNPCStateTags()
```

Remove the state tags from the given NPC on the current session. Does nothing if the NPC does not have the tag.

![Node Remove NPC Tags](/docs/images/node_remove_npc_state_tags.png)

### Parameters

| Name           | Type           | Default value            | Description |
| -------------- | -------------- | ------------------------ | ----------- |
| NPC Name       | const FString& | *empty string*           | The name of the NPC to remove the tags |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states |
| State Tags     | const TArray\<FString>& | -               | The tags that will be removed to the NPC tags |

### Return values

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Clear NPC State Tags

C++ Function: 
```cpp
static void UDiagenStateTagsBPLibrary::ClearNPCStateTags()
```

Remove all the state tags from the given NPC on the current session.

![Node Clear NPC Tags](/docs/images/node_clear_npc_state_tags.png)

### Parameters

| Name           | Type           | Default value            | Description |
| -------------- | -------------- | ------------------------ | ----------- |
| NPC Name       | const FString& | *empty string*           | The name of the NPC to remove **all** the tags |
| Session States | const TArray<[FSessionState](#TODO)>& | - | The current session states |

### Return values

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Updated Session States | TArray<[FSessionState](#TODO)>& | The updated session states |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Contains NPC State Tags

C++ Function: 
```cpp
static void UDiagenStateTagsBPLibrary::ContainsNPCStateTags()
```

Check if the given state tags are defined for the given NPC on the current session. All the tags that are not found will be returned with the array `Missing State Tags`.

![Node Contains NPC Tags](/docs/images/node_contains_npc_state_tags.png)

### Parameters

| Name                  | Type                    | Default value   | Description |
| --------------------- | ----------------------- | --------------- | ----------- |
| NPC Name              | const FString&          | *empty string*  | The name of the NPC to check the tags |
| Session States        | const TArray<[FSessionState](#TODO)>& | - | The current session states            |
| State Tags to Search  | const TArray\<FString>& | -               | The list of tags to search            |

### Return values

| Name                   | Type                            | Description                |
| ---------------------- | ------------------------------- | -------------------------- |
| Missing State Tags     | TArray<[FSessionState](#TODO)>& | The list of all tags that have not been found |
| Contains               | bool&                           | `true` if all search tags have been found, `false` otherwise |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get NPC State Tags

C++ Function: 
```cpp
static void UDiagenStateTagsBPLibrary::GetNPCEnabledStateTags()
```

Get the state tags for the given NPC on the current session.

![Node Get NPC Tags](/docs/images/node_get_npc_state_tags.png)

### Parameters

| Name                  | Type                    | Default value   | Description |
| --------------------- | ----------------------- | --------------- | ----------- |
| NPC Name              | const FString&          | *empty string*  | The name of the NPC to get the tags   |
| Session States        | const TArray<[FSessionState](#TODO)>& | - | The current session states            |

### Return values

| Name                   | Type              | Description                |
| ---------------------- | ----------------- | -------------------------- |
| Enabled State Tags     | TArray\<FString>& | The list of the NPC tags   |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Set NPC State Tags

C++ Function: 
```cpp
static void UDiagenStateTagsBPLibrary::SetNPCStateTags()
```

Set the state tags for the given NPC on the current session. Uses [Append NPC State Tags](#append-npc-state-tags) if you prefer to add the tags to those already existing.

![Node Set NPC Tags](/docs/images/node_get_npc_state_tags.png)

### Parameters

| Name                  | Type                    | Default value   | Description |
| --------------------- | ----------------------- | --------------- | ----------- |
| NPC Name              | const FString&          | *empty string*  | The name of the NPC to set the tags   |
| Session States        | const TArray<[FSessionState](#TODO)>& | - | The current session states            |
| New State Tags        | const TArray\<FString>& | -               | The list of tags set to the NPC       |

### Return values

| Name                   | Type              | Description                |
| ---------------------- | ----------------- | -------------------------- |
| Enabled State Tags     | TArray\<FString>& | The list of the NPC tags   |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## <i style="color: red">**Deprecated**</i> - Bind All State Tags to NPC

C++ Function: 
```cpp
static void UDiagenSessionBPLibrary::BindAllStateTagsToNpc()
```

> [!CAUTION]
> `AllStateTags` is deprecated and should **not** be used anymore!

Fill the `AllStateTags` array based on the tables for the given NPC on the current session.

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## <i style="color: red">**Deprecated**</i> - Get NPC All State Tags

C++ Function: 
```cpp
static void UDiagenStateTagsBPLibrary::GetNPCAllStateTags()
```

> [!CAUTION]
> `AllStateTags` is deprecated and should **not** be used anymore!

Get the `AllStateTags` array for the given NPC on the current session.


