# API Reference

**[← Table of contents](/README.md#table-of-contents)**

<br/><br/>

## [LLM Prompting](./LLM_prompting.md)
    [Create Prompt](./LLM_prompting.md#create-prompt)<br/>
    [Diagen Prompt AI model (Conversation)](./LLM_prompting.md#diagen-prompt-ai-model-conversation)<br/>
    [Diagen Prompt AI model (Raw)](./LLM_prompting.md#diagen-prompt-ai-model-raw)<br/>
    [Diagen Prompt AI model (Topic detection)](./LLM_prompting.md#diagen-prompt-ai-model-topic-detection)<br/>
    [Diagen Prompt AI model (Topic validation)](./LLM_prompting.md#diagen-prompt-ai-model-topic-validation)<br/>
    [Diagen LLM Topic Detection](./LLM_prompting.md#diagen-llm-topic-detection)<br/>
    [Diagen LLM Topic Validation](./LLM_prompting.md#diagen-llm-topic-validation)<br/>
    [Instruction to Verbatime](./LLM_prompting.md#instruction-to-verbatime)<br/>

## [Local executable](./Local.md)
    [Start Diagen Local Executable (START DIAGEN LOCAL)](./Local.md#start-diagen-local-executable)<br/>
    [Stop Diagen Local Executable (STOP DIAGEN LOCAL)](./Local.md#stop-diagen-local-executable)<br/>
    [Get Diagen Local Executable Status](./Local.md#get-diagen-local-executable-status---pure) - *Pure*<br/>
    [Can Use Local Executable](./Local.md#can-use-local-executable---pure) - *Pure*<br/>
    [Is Local Executable Installed](./Local.md#is-local-executable-installed---pure) - *Pure*<br/>

## [Stream](./Stream.md)
    [Bind Event to Diagen Stream](./Stream.md#bind-event-to-diagen-stream)<br/>
    [Unbind Event to Diagen Stream](./Stream.md#unbind-event-to-diagen-stream)<br/>
    [Unbind All Events to Diagen Stream](./Stream.md#unbind-all-events-to-diagen-stream)<br/>

## [Diagen Session](./Diagen_session.md)
    [Add NPC](./Diagen_session.md#add-npc) - *previously InitSession()*<br/>
    [Remove NPC](./Diagen_session.md#remove-npc)<br/>
    [Reset NPC](./Diagen_session.md#reset-npc)<br/>
    [Get Session NPC Names](./Diagen_session.md#get-session-npc-names)<br/>
    [Save Session States](./Diagen_session.md#save-session-states)<br/>
    [Load Session States](./Diagen_session.md#load-session-states)<br/>
    <i style="color: red">**Deprecated**</i> - [Reset Session](./Diagen_session.md#reset-session---deprecated)<br/>
    [Update Session Array](./Diagen_session.md#update-session-array)<br/>
    [Update Session Int](./Diagen_session.md#update-session-int)<br/>
    [Update Session String](./Diagen_session.md#update-session-string)<br/>
    [Get Session Array](./Diagen_session.md#get-session-array)<br/>
    [Get Session Int](./Diagen_session.md#get-session-int)<br/>
    [Get Session String](./Diagen_session.md#get-session-string)<br/>
    [Reset History](./Diagen_session.md#reset-history)<br/>
    [Update History](./Diagen_session.md#update-history)<br/>

## [Diagen Topics and Events](./Diagen_topics_events.md)
    [Enable NPC Topic(s)](./Diagen_topics_events.md#enable-npc-topics)<br/>
    [Get NPC Enable Topic(s)](./Diagen_topics_events.md#get-npc-enable-topics)<br/>
    [Update Enabled Topics](./Diagen_topics_events.md#update-enabled-topics)<br/>
    [Trigger Diagen Event](./Diagen_topics_events.md#trigger-diagen-event)<br/>
    [List Available Events](./Diagen_topics_events.md#list-available-events)<br/>

## [Diagen State Tags](./Diagen_state_tags.md)
    [Append NPC State Tags](./Diagen_state_tags.md#append-npc-state-tags)<br/>
    [Remove NPC State Tags](./Diagen_state_tags.md#remove-npc-state-tags)<br/>
    [Clear NPC State Tags](./Diagen_state_tags.md#clear-npc-state-tags)<br/>
    [Contains NPC State Tags](./Diagen_state_tags.md#contains-npc-state-tags)<br/>
    [Get NPC State Tags](./Diagen_state_tags.md#get-npc-state-tags)<br/>
    [Set NPC State Tags](./Diagen_state_tags.md#set-npc-state-tags)<br/>
    <i style="color: red">**Deprecated**</i> - [Bind All State Tags to NPC](./Diagen_state_tags.md#deprecated---bind-all-state-tags-to-npc)<br/>
    <i style="color: red">**Deprecated**</i> - [Get NPC All State Tags](./Diagen_state_tags.md#deprecated---get-npc-all-state-tags)<br/>

## [Utilities](./Utilities.md)
    [Get NPC State](./Utilities.md#get-npc-state)<br/>
    [Get File Content](./Utilities.md#get-file-content)<br/>
    [Parse Into Array Lines](./Utilities.md#parse-into-array-lines)<br/>
    [Replace Regex Matches](./Utilities.md#replace-regex-matches)<br/>
    [Sort NPC Description Priority Array](./Utilities.md#sort-npc-description-priority-array)<br/>

## [Delegates (Events)](./Delegates.md)
    [On Diagen Initialized](./Delegates.md#on-diagen-initialized)<br/>
    [On Diagen Stream Response Part](./Delegates.md#on-diagen-stream-response-part)<br/>
    [On Diagen Response](./Delegates.md#on-diagen-response)<br/>
    [On Diagen Topic Response](./Delegates.md#on-diagen-topic-response)<br/>
    [On Diagen Topic Validation Response](./Delegates.md#on-diagen-topic-validation-response)<br/>
    <i style="color: red">**Deprecated**</i> - [On Topic Initialized](./Delegates.md#deprecated---on-topic-initialized)<br/>

## [Classes](./Classes_structs_enums.md#classes---uclass)
    [Diagen Plugin Settings](./Classes_structs_enums.md#diagen-plugin-settings)<br/>

## [Structs](./Classes_structs_enums.md#structures---ustruct)
    [Diagen Subsystem Config](./Classes_structs_enums.md#diagen-subsystem-config)<br/>
    [Diagen Prompt Config](./Classes_structs_enums.md#diagen-prompt-config)<br/>
    [Prompt Message](./Classes_structs_enums.md#prompt-message)<br/>
    [NPC Description Priority](./Classes_structs_enums.md#npc-description-priority)<br/>
    [Session State](./Classes_structs_enums.md#session-state)<br/>
    [Topic Trigger Pair](./Classes_structs_enums.md#topic-trigger-pair)<br/>

## [Data Table Structs](./Classes_structs_enums.md#structures-for-data-table---ustruct)
    [Character Information Table (CI Table)](./Classes_structs_enums.md#character-information-table-ci-table)<br/>
    [Diagen Event Table](./Classes_structs_enums.md#diagen-event-table)<br/>
    [Topic Table](./Classes_structs_enums.md#topic-table)<br/>
    [State Tags Weight Table](./Classes_structs_enums.md#state-tags-weights-table)<br/>
    <i style="color: red">**Deprecated**</i> - [Trigger Option Table](./Classes_structs_enums.md#trigger-option-table---deprecated)<br/>
    <i style="color: red">**Deprecated**</i> - [Prefix Option Table](./Classes_structs_enums.md#prefix-option-table----deprecated)<br/>
    <i style="color: red">**Deprecated**</i> - [Suffix Option Table](./Classes_structs_enums.md#suffix-option-table----deprecated)<br/>
    <i style="color: red">**Deprecated**</i> - [Initial Session States Table](./Classes_structs_enums.md#initial-session-states-table----deprecated)<br/>

## [Enums](./Classes_structs_enums.md#enumerations---uenum)
    [Diagen Subsystem Status](./Classes_structs_enums.md#diagen-subsystem-status)<br/>
    [Session Attribute Style](./Classes_structs_enums.md#session-attribute-type)<br/>