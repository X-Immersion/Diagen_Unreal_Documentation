# Delegates (Events)

**[← API Reference](/docs/API_reference/README.md)**

## On this page

Here you can find a list of all Delegates (or Events) defined in the Diagen plugin.

* [On Diagen Initialized](#on-diagen-initialized)<br/>
* [On Diagen Stream Response Part](#on-diagen-stream-response-part)<br/>
* [On Diagen Response](#on-diagen-response)<br/>
* [On Diagen Topic Response](#on-diagen-topic-response)<br/>
* [On Diagen Topic Validation Response](#on-diagen-topic-validation-response)<br/>
* <i style="color: red">**Deprecated**</i> - [On Topic Initialized](#deprecated---on-topic-initialized)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## On Diagen Initialized

C++ Declaration: 
```cpp
DECLARE_DYNAMIC_DELEGATE_OneParam(FOnDiagenInitialized, bool, Success);
```

Use the nodes *Add Custom Event...* or *Create Event* to bind this event to the node [Start Diagen Local Executable (START DIAGEN LOCAL)](./Local.md#start-diagen-local-executable).

![Event how to add](/docs/images/event_connect.png)<br/>
![Event On Diagen Init](/docs/images/event_on_diagen_initialized.png)

### Event variables

| Name    | Type                    | Description                |
| ------- | ----------------------- | -------------------------- |
| Success | bool                    | `true` if the Diagen local executable is started and the LLM model is loaded, `false` otherwise |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## On Diagen Stream Response Part

C++ Declaration: 
```cpp
DECLARE_DYNAMIC_DELEGATE_TwoParams(FOnDiagenStreamResponsePart, FString, ResponsePart, const FGuid&, Guid);
```

Use the nodes *Add Custom Event...* or *Create Event* to bind this event to the nodes [Bind Event to Diagen Stream](./Stream.md#bind-event-to-diagen-stream) and [Unbind Event to Diagen Stream](./Stream.md#unbind-event-to-diagen-stream).

![Event how to add](/docs/images/event_connect.png)<br/>
![Event On Diagen Stream Response part](/docs/images/event_on_diagen_stream_response_part.png)

### Event variables

| Name          | Type                    | Description                |
| ------------- | ----------------------- | -------------------------- |
| Response Part | FString                 | The LLM stream generated part (for all requests)|
| Guid          | const FGuid&            | The Guid associated with this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## On Diagen Response

C++ Declaration: 
```cpp
DECLARE_DYNAMIC_DELEGATE_ThreeParams(FOnDiagenResponse, bool, Success, FString, ResponseOrError, const FGuid&, Guid);
```

Use the nodes *Add Custom Event...* or *Create Event* to bind this event to the nodes [Diagen Prompt AI Model (raw)](./LLM_prompting.md#diagen-prompt-ai-model-raw), [Diagen Prompt AI Model (conversation)](./LLM_prompting.md#diagen-prompt-ai-model-conversation) and [Instruction to Verbatime](./LLM_prompting.md#instruction-to-verbatime).

![Event how to add](/docs/images/event_connect.png)<br/>
![Event On Diagen Response](/docs/images/event_on_diagen_response.png)

### Event variables

| Name              | Type                  | Description                |
| ----------------- | --------------------- | -------------------------- |
| Success           | bool                  | `true` if the generation was successful, `false` if an error occured |
| Response or Error | FString               | The LLM generated response if *Success* is true, otherwise the error message |
| Guid              | const FGuid&          | The Guid associated with this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## On Diagen Topic Response

C++ Declaration: 
```cpp
DECLARE_DYNAMIC_DELEGATE_FourParams(FOnTopicResponse, bool, Success, FString, ResponseOrError, const TArray<FTopicTriggerPair>&, TopicPairs, const FGuid&, Guid);
```

Use the nodes *Add Custom Event...* or *Create Event* to bind this event to the node [Diagen LLM Topic Detection](./LLM_prompting.md#diagen-llm-topic-detection).

![Event how to add](/docs/images/event_connect.png)<br/>
![Event On Diagen Topic Response](/docs/images/event_on_diagen_topic_response.png)

### Event variables

| Name              | Type                  | Description                |
| ----------------- | --------------------- | -------------------------- |
| Success           | bool                  | `true` if the generation was successful, `false` if an error occured |
| Response or Error | FString               | The LLM detected topic index, or the LLM raw response |
| Topic Pairs       | const TArray<[FTopicTriggerPair](#TODO)>& | The list of **ALL** topic(s) for the NPC |
| Guid              | const FGuid&          | The Guid associated with this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## On Diagen Topic Validation Response

C++ Declaration: 
```cpp
DECLARE_DYNAMIC_DELEGATE_FiveParams(FOnTopicValidationResponse, bool, Success, FString, ResponseOrError, FString, Topic, FString, Triggers, const FGuid&, Guid);
```

Use the nodes *Add Custom Event...* or *Create Event* to bind this event to the node [Diagen LLM Topic Validation](./LLM_prompting.md#diagen-llm-topic-validation).

![Event how to add](/docs/images/event_connect.png)<br/>
![Event On Diagen Topic Validation Response](/docs/images/event_on_diagen_topic_validation_response.png)

### Event variables

| Name              | Type                  | Description                |
| ----------------- | --------------------- | -------------------------- |
| Success           | bool                  | `true` if the generation was successful, `false` if an error occured |
| Response or Error | FString               | The LLM topic validation strength, or the LLM raw response |
| Topic             | FString               | The detected topic (ONLY if the LLM response strength is `>= 3`) |
| Trigger           | FString               | The topic trigger (ONLY if the LLM response strength is `>= 3`) |
| Guid              | const FGuid&          | The Guid associated with this prompt |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## <i style="color: red">**Deprecated**</i> - On Topic Initialized

C++ Declaration: 
```cpp
DECLARE_DYNAMIC_DELEGATE_OneParam(FOnTopicInitialized, bool, Success);
```

> [!IMPORTANT]  
> This event is not used anymore!