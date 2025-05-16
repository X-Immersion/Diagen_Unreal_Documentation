# Local Executable

**[← API Reference](/docs/API_reference/README.md)**

## On this page

The following nodes can be used to handle the local LLM model lifecycle.

* [Start Diagen Local Executable (START DIAGEN LOCAL)](#start-diagen-local-executable)<br/>
* [Stop Diagen Local Executable (STOP DIAGEN LOCAL)](#stop-diagen-local-executable)<br/>
* [Get Diagen Local Executable Status](#get-diagen-local-executable-status---pure) - *Pure*<br/>
* [Can Use Local Executable](#can-use-local-executable---pure) - *Pure*<br/>
* [Is Local Executable Installed](#is-local-executable-installed---pure) - *Pure*<br/>

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Start Diagen Local Executable

*Short name: **START DIAGEN LOCAL***

C++ Function: 
```cpp
static void UDiagenLlmBPLibrary::StartDiagenLocalExecutable()
```

Start the Diagen local executable and load the LLM model in memory. When the model is loaded, the event [On Diagen Initialized](#TODO) will be executed and you can start [prompting the model](/docs/API_reference/LLM_prompting.md).

![Node Start Diagen Local Exec](/docs/images/node_start_diagen_local.png)

### Parameters

| Name                  | Type                       | Default value | Description |
| --------------------- | -------------------------- | ------------- | ----------- |
| Config                | const [FDiagenSubsystemConfig](#TODO)& | - | The Diagen executable configuration |
| On Diagen Initialized | [FOnDiagenInitialized](#TODO)          | - | Delegate event called when the executable is ready to use (or if an error occured) |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Stop Diagen Local Executable

*Short name: **STOP DIAGEN LOCAL***

C++ Function: 
```cpp
static void UDiagenLlmBPLibrary::StopDiagenLocalExecutable()
```

Unload the LLM model and stop the Diagen local executable.

![Node Stop Diagen Local Exec](/docs/images/node_stop_diagen_local.png)

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Get Diagen Local Executable Status - *Pure*

C++ Function: 
```cpp
static EDiagenSubsystemStatus UDiagenLlmBPLibrary::GetSubsystemStatus()
```

Get the current status of Diagen Local Executable.

![Node get Local Exec Status](/docs/images/node_get_diagen_local_executable_status.png)

### Return values

| Name          | Type                            | Description        |
| ------------- | ------------------------------  | ------------------ |
| Return Value  | [EDiagenSubsystemStatus](#TODO) | The current status |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Can Use Local Executable - *Pure*

C++ Function: 
```cpp
static bool UDiagenUtilitiesLibrary::CanUseLocalExecutable()
```

Indicate if the Api-Key have been validated for local execution.

![Node can Use Local Exec](/docs/images/node_can_use_local_executable.png)

### Return values

| Name          | Type | Description        |
| ------------- | ---- | ------------------ |
| Return Value  | bool | `true` if local executable can be used, `false` otherwise |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>

## Is Local Executable Installed - *Pure*

C++ Function: 
```cpp
static bool UDiagenUtilitiesLibrary::CanUseLocalExecutable()
```

Check if the Diagen local executable is installed on this machine.

![Node is Local Exec Installed](/docs/images/node_is_local_executable_installed.png)

### Return values

| Name          | Type     | Description        |
| ------------- | -------  | ------------------ |
| OutPath       | FString& | The Diagen local executable path |
| Return Value  | bool     | `true` if local executable can be used, `false` otherwise |

<!------------------------------------------------------------------------------------------------------------------------------->
<br/>
