# Streaming

**[← API Reference](/docs/API_reference/README.md)**

## On this page

The following nodes can be used to listen to the Diagen LLM generated parts via streaming.

* [Bind Event to Diagen Stream](#bind-event-to-diagen-stream)<br/>
* [Unbind Event to Diagen Stream](#unbind-event-to-diagen-stream)<br/>
* [Unbind All Events to Diagen Stream](#unbind-all-events-to-diagen-stream)<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Bind Event to Diagen Stream

C++ Function: 
```cpp
static void UDiagenLlmBPLibrary::BindStream()
```

Bind a [stream delegate](#TODO) (event) to the diagen LLM stream.

![Node bind stream](/docs/images/node_bind_event_to_diagen_stream.png)

### Parameters

| Name  | Type                                        | Default value | Description |
| ----- | ------------------------------------------- | ------------- | ----------- |
| Event | const [FOnDiagenStreamResponsePart](#TODO)& | -             | Delegate event called each time a stream part has been generated (from all prompts) |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Unbind Event to Diagen Stream

C++ Function: 
```cpp
static void UDiagenLlmBPLibrary::UnbindStream()
```

Unbind an existing [stream delegate](#TODO) (event) from the diagen LLM stream.

![Node unbind stream](/docs/images/node_unbind_event_to_diagen_stream.png)

### Parameters

| Name  | Type                                        | Default value | Description |
| ----- | ------------------------------------------- | ------------- | ----------- |
| Event | const [FOnDiagenStreamResponsePart](#TODO)& | -             | Delegate event called each time a stream part has been generated (from all prompts) |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Unbind All Events to Diagen Stream

C++ Function: 
```cpp
static void UDiagenLlmBPLibrary::ClearStream()
```

Unbind all existing [stream delegates](#TODO) (event) from the diagen LLM stream.

![Node unbind all stream](/docs/images/node_unbind_all_events_to_diagen_stream.png)

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>
