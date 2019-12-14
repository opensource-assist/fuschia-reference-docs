[TOC]

# fuchsia.app.discover


## **PROTOCOLS**

## DiscoverRegistry {#DiscoverRegistry}
*Defined in [fuchsia.app.discover/discover_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#24)*

<p>Interface between sessionmgr and discovermgr to route service connections
requests that require module scoping.</p>

### RegisterStoryModule {#RegisterStoryModule}

<p>Retrieves a story module controller for the module identified by <code>module</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>module</code></td>
            <td>
                <code><a class='link' href='#ModuleIdentifier'>ModuleIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoryModule'>StoryModule</a>&gt;</code>
            </td>
        </tr></table>



## SessionDiscoverContext {#SessionDiscoverContext}
*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#27)*

<p>Provided to session shells to communicate with discover.</p>

### GetStoryContext {#GetStoryContext}

<p>The session shell can act as the story shell. Gets a a story control
service.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code><a class='link' href='#StoryId'>StoryId</a></code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoryDiscoverContext'>StoryDiscoverContext</a>&gt;</code>
            </td>
        </tr></table>



## StoryDiscoverContext {#StoryDiscoverContext}
*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#35)*


### SetProperty {#SetProperty}

<p>Sets the value for the given story property |key|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverContext_SetProperty_Result'>StoryDiscoverContext_SetProperty_Result</a></code>
            </td>
        </tr></table>

### GetProperty {#GetProperty}

<p>Gets the value for the given story property |key|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverContext_GetProperty_Result'>StoryDiscoverContext_GetProperty_Result</a></code>
            </td>
        </tr></table>

### GetSurfaceData {#GetSurfaceData}

<p>Gets the surface data for the given |surface_id|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code><a class='link' href='#SurfaceId'>SurfaceId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_data</code></td>
            <td>
                <code><a class='link' href='#SurfaceData'>SurfaceData</a></code>
            </td>
        </tr></table>

## StoryModule {#StoryModule}
*Defined in [fuchsia.app.discover/story_module.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#20)*


### WriteOutput {#WriteOutput}

<p>Writes the <code>entity_reference</code> to the module's <code>output_parameter_name</code>
output. If no entity is provided, the output will be unset.
Return happens upon completion of a successful write.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_name</code></td>
            <td>
                <code><a class='link' href='#OutputName'>OutputName</a></code>
            </td>
        </tr><tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryModule_WriteOutput_Result'>StoryModule_WriteOutput_Result</a></code>
            </td>
        </tr></table>

### IssueIntent {#IssueIntent}

<p>Starts a mod by issuing an intent to it or re-issues an intent to the mod
with the given name.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code><a class='link' href='#ModuleName'>ModuleName</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### WriteInstanceState {#WriteInstanceState}

<p>Writes the <code>instance_state</code> item with the given key to storage.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#StateKey'>StateKey</a></code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryModule_WriteInstanceState_Result'>StoryModule_WriteInstanceState_Result</a></code>
            </td>
        </tr></table>

### ReadInstanceState {#ReadInstanceState}

<p>Reads the <code>instance_state</code> item with the given key from storage.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#StateKey'>StateKey</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#StoryModule_ReadInstanceState_Result'>StoryModule_ReadInstanceState_Result</a></code>
            </td>
        </tr></table>

## Suggestions {#Suggestions}
*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#12)*


### GetSuggestions {#GetSuggestions}

<p>Sends a query to get suggestions and an iterator with which the client
can fetch suggestions coming as response.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code><a class='link' href='#Query'>Query</a></code>
            </td>
        </tr><tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#SuggestionsIterator'>SuggestionsIterator</a>&gt;</code>
            </td>
        </tr></table>



### NotifyInteraction {#NotifyInteraction}

<p>Requests the execution of a suggestion's intent.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>suggestion_id</code></td>
            <td>
                <code><a class='link' href='#SuggestionId'>SuggestionId</a></code>
            </td>
        </tr><tr>
            <td><code>interaction</code></td>
            <td>
                <code><a class='link' href='#InteractionType'>InteractionType</a></code>
            </td>
        </tr></table>



## SuggestionsIterator {#SuggestionsIterator}
*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#27)*


### Next {#Next}

<p>Fetches the next set of suggestions being iterated on. When there's no
more suggestions an empty vector will be sent and the connection will be
closed from the server.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>suggestions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Suggestion'>Suggestion</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### StoryDiscoverContext_SetProperty_Response {#StoryDiscoverContext_SetProperty_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryDiscoverContext_GetProperty_Response {#StoryDiscoverContext_GetProperty_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryModule_WriteOutput_Response {#StoryModule_WriteOutput_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryModule_WriteInstanceState_Response {#StoryModule_WriteInstanceState_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryModule_ReadInstanceState_Response {#StoryModule_ReadInstanceState_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### StoryDiscoverError {#StoryDiscoverError}
Type: <code>int32</code>

*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#14)*

<p>Error code for story related services.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STORAGE</code></td>
            <td><code>1</code></td>
            <td><p>If the story storage fails to respond to the SetProperty request.</p>
</td>
        </tr><tr>
            <td><code>VMO_STRING_CONVERSION</code></td>
            <td><code>2</code></td>
            <td><p>If the given value fails to be converted to a story property.</p>
</td>
        </tr><tr>
            <td><code>INVALID_KEY</code></td>
            <td><code>3</code></td>
            <td><p>If the key for a story property is invalid.</p>
</td>
        </tr></table>

### OutputError {#OutputError}
Type: <code>int32</code>

*Defined in [fuchsia.app.discover/story_module.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#38)*

<p>Errors that can occur when writing to an output.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN_NAME</code></td>
            <td><code>1</code></td>
            <td><p>If the output doesn't match a parameter defined in the module manifest
for the action currently being handled by the module.</p>
</td>
        </tr><tr>
            <td><code>UNKNOWN_ENTITY_REFERENCE</code></td>
            <td><code>2</code></td>
            <td><p>If the entity reference couldn't be resolved.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ENTITY_TYPE</code></td>
            <td><code>3</code></td>
            <td><p>If the entity type written doesn't match the type defined in the module
manifest for the action currently being handled by the module.</p>
</td>
        </tr></table>

### InteractionType {#InteractionType}
Type: <code>uint32</code>

*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#22)*

<p>Supported types of interaction with a suggestion.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SELECTED</code></td>
            <td><code>0</code></td>
            <td><p>Set when the suggestion was accepted by the user.</p>
</td>
        </tr></table>



## **TABLES**

### ModuleIdentifier {#ModuleIdentifier}


*Defined in [fuchsia.app.discover/discover_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#29)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>story_id</code></td>
            <td>
                <code><a class='link' href='#StoryId'>StoryId</a></code>
            </td>
            <td><p>The ID of the story to which the module belongs.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>module_path</code></td>
            <td>
                <code><a class='link' href='#ModulePath'>ModulePath</a></code>
            </td>
            <td><p>The named path leading up to this module instance. This path is a unique
identifier of the module in the story.</p>
</td>
        </tr></table>

### SurfaceData {#SurfaceData}


*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#47)*

<p>Information about a surface in the story.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#ActionName'>ActionName</a></code>
            </td>
            <td><p>The name of the action that triggered the creation of that surface.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>parameter_types</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The types of the parameters for each parameter of the action.</p>
</td>
        </tr></table>

### Suggestion {#Suggestion}


*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#34)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#SuggestionId'>SuggestionId</a></code>
            </td>
            <td><p>The id of the suggestion. This id is used when notifying an interaction.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>display_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/#DisplayInfo'>DisplayInfo</a></code>
            </td>
            <td><p>Display information about the suggestion.</p>
</td>
        </tr></table>



## **UNIONS**

### StoryDiscoverContext_SetProperty_Result {#StoryDiscoverContext_SetProperty_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverContext_SetProperty_Response'>StoryDiscoverContext_SetProperty_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverError'>StoryDiscoverError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryDiscoverContext_GetProperty_Result {#StoryDiscoverContext_GetProperty_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverContext_GetProperty_Response'>StoryDiscoverContext_GetProperty_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverError'>StoryDiscoverError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryModule_WriteOutput_Result {#StoryModule_WriteOutput_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryModule_WriteOutput_Response'>StoryModule_WriteOutput_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#OutputError'>OutputError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryModule_WriteInstanceState_Result {#StoryModule_WriteInstanceState_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryModule_WriteInstanceState_Response'>StoryModule_WriteInstanceState_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverError'>StoryDiscoverError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryModule_ReadInstanceState_Result {#StoryModule_ReadInstanceState_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#StoryModule_ReadInstanceState_Response'>StoryModule_ReadInstanceState_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#StoryDiscoverError'>StoryDiscoverError</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="STORY_ID_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#8">STORY_ID_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length of a story id.</p>
</td>
        </tr>
    <tr id="MODULE_PATH_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#14">MODULE_PATH_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length of a module path.</p>
</td>
        </tr>
    <tr id="MODULE_PATH_PART_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#15">MODULE_PATH_PART_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="ACTION_NAME_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#55">ACTION_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="PARAMETER_TYPE_NAME_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#56">PARAMETER_TYPE_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="SURFACE_ID_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#57">SURFACE_ID_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="ENTITY_REFERENCE_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#10">ENTITY_REFERENCE_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="MODULE_NAME_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#11">MODULE_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="STATE_KEY_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#12">STATE_KEY_MAX_LENGTH</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="OUTPUT_NAME_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#13">OUTPUT_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="StoryId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#11">StoryId</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#STORY_ID_MAX_LENGTH'>STORY_ID_MAX_LENGTH</a></code>]</td>
            <td><p>An ientifier for a story.</p>
</td>
        </tr><tr id="ModulePathPart">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#18">ModulePathPart</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MODULE_PATH_PART_MAX_LENGTH'>MODULE_PATH_PART_MAX_LENGTH</a></code>]</td>
            <td><p>And identifier for a module.</p>
</td>
        </tr><tr id="ModulePath">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#19">ModulePath</a></td>
            <td>
                <code>vector</code>[<code><a class='link' href='#MODULE_PATH_MAX_LENGTH'>MODULE_PATH_MAX_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr id="ActionName">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#9">ActionName</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#ACTION_NAME_MAX_LENGTH'>ACTION_NAME_MAX_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr id="ParameterTypeName">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#10">ParameterTypeName</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#PARAMETER_TYPE_NAME_MAX_LENGTH'>PARAMETER_TYPE_NAME_MAX_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr id="SurfaceId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#11">SurfaceId</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#SURFACE_ID_MAX_LENGTH'>SURFACE_ID_MAX_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr id="ModuleName">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#15">ModuleName</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#MODULE_NAME_MAX_LENGTH'>MODULE_NAME_MAX_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr id="OutputName">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#16">OutputName</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#OUTPUT_NAME_MAX_LENGTH'>OUTPUT_NAME_MAX_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr id="StateKey">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#17">StateKey</a></td>
            <td>
                <code>string</code>[<code><a class='link' href='#STATE_KEY_MAX_LENGTH'>STATE_KEY_MAX_LENGTH</a></code>]</td>
            <td></td>
        </tr><tr id="Query">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#8">Query</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr><tr id="SuggestionId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#9">SuggestionId</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr></table>

