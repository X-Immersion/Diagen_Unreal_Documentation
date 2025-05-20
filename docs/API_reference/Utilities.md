# Utilities

**[← API Reference](/docs/API_reference/README.md)**

## On this page

The following nodes are not directly used by the Diagen plugin, but can be very useful in some situations.

* [Get NPC State](#get-npc-state)<br/>
* [Get File Content](#get-file-content)<br/>
* [Parse Into Array Lines](#parse-into-array-lines)<br/>
* [Replace Regex Matches](#replace-regex-matches)<br/>
* [Sort NPC Description Priority Array](#sort-npc-description-priority-array)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get NPC State

C++ Function: 
```cpp
static void UDiagenStateBPLibrary::GetNPCState()
```

Alternative node to find the state information for a given NPC on the current state. The other method is to simply iterate over the session states array and check for the state NPC name.

![Node Get NPC State](/docs/images/node_get_npc_state.png)

### Parameters

| Name           | Type           | Default value            | Description                          |
| -------------- | -------------- | ------------------------ | ------------------------------------ |
| Session States | const TArray<[FSessionState](./Classes_structs_enums.md#session-state)>& | - | The current session states           |
| NPC Name       | const FString& | *empty string*           | The name of the NPC to get the data  |

### Return values

| Name  | Type                    | Description                |
| ----- | ----------------------- | -------------------------- |
| State | [FSessionState](./Classes_structs_enums.md#session-state)& | The NPC state data         |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get File Content

C++ Function: 
```cpp
static bool UDiagenUtilitiesLibrary::GetFileContent()
```

Use the Unreal C++ function `FFileHelper::LoadFileToString()` to read the whole file content as string (the function is not available for Blueprints by default).

![Node Get File Content](/docs/images/node_get_file_content.png)

### Parameters

| Name      | Type  | Default value | Description                          |
| --------- | ----- | ------------- | ------------------------------------ |
| File Path | FText | *empty text*  | The full file path, including file extension |

### Return values

| Name          | Type     | Description                |
| ------------- | -------- | -------------------------- |
| Output String | FString& | The file content, as string |
| Return Value  | bool     | True if the file could be read, false otherwise |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Parse Into Array Lines

C++ Function: 
```cpp
static bool UDiagenUtilitiesLibrary::ParseIntoArrayLines()
```

Use the Unreal C++ string method `FString::ParseIntoArrayLines()` to split the input sentence with both `\n`, `\r` and `\n\r` characters. The Blueprint node `ParseIntoArray` does not handle all types of new line ASCII/UTF8 chars as delimiter.

![Node Parse Into Array Lines](/docs/images/node_parse_into_array_lines.png)

### Parameters

| Name       | Type           | Default value | Description                          |
| ---------- | -------------- | ------------- | ------------------------------------ |
| Str        | const FString& | *empty text*  | The string that will be parsed into an array |
| Cull Empty | bool           | `true`        | Does not include empty string parts in the result array |

### Return values

| Name            | Type             | Description                |
| --------------- | ---------------- | -------------------------- |
| Out Array Lines | TArray<FString>& | The splitted string parts  |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Replace Regex Matches

C++ Function: 
```cpp
static int UDiagenUtilitiesLibrary::ReplaceRegexMatches()
```

Similar to the Blueprint string node `Replace`, but use a Regex to search substrings.

![Node Replace Regex Matches](/docs/images/node_replace_regex_matches.png)

### Parameters

| Name           | Type           | Default value  | Description                          |
| -------------- | -------------- | -------------- | ------------------------------------ |
| Input          | FString        | *empty string* | The input string where the regex will be applied |
| Regex          | FString        | *empty string* | The regex used to search substring(s) |
| Replace String | FString        | *empty string* | The substring used to replace all matching parts |

### Return values

| Name             | Type             | Description                |
| ---------------- | ---------------- | -------------------------- |
| Processed String | TArray<FString>& | The result string, where all matches have been replaced |
| Return Value     | int              | The amout of substring that matches the regex. This can be useful if you want to count your regex matches |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Sort NPC Description Priority Array

C++ Function: 
```cpp
static void UDiagenUtilitiesLibrary::SortNPCDescriptionPriorityArray()
```

Sort an array of string based on the string priority (weight). This can be really useful if you use your own logic to create the NPC system prompt, rather than using the node [Create Prompt](./LLM_prompting.md#create-prompt) *(i.e.: Construct the NPC system prompt from the CI table in the good order)*.

![Node Sort NPC Description](/docs/images/node_sort_npc_description_priority_array.png)

### Parameters

| Name  | Type                                             | Default value  | Description                          |
| ----- | ------------------------------------------------ | -------------- | ------------------------------------ |
| Array | TArray<[FNpcDescriptionPriority](./Classes_structs_enums.md#npc-description-priority)>&        | -              | The array to sort |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>