Project: /_project.yaml
Book: /_book.yaml

# fuchsia.app.discover


## **PROTOCOLS**

## DiscoverRegistry {:#DiscoverRegistry}
*Defined in [fuchsia.app.discover/discover_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#24)*

 Interface between sessionmgr and discovermgr to route service connections
 requests that require module scoping.

### RegisterModuleOutputWriter {:#RegisterModuleOutputWriter}

 Retrieves a module output writer for the module identified by `module`.

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
                <code>request&lt;<a class='link' href='#ModuleOutputWriter'>ModuleOutputWriter</a>&gt;</code>
            </td>
        </tr></table>



### RegisterStoryModule {:#RegisterStoryModule}

 Retrieves a story module controller for the module identified by `module`.

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



## ModuleOutputWriter {:#ModuleOutputWriter}
*Defined in [fuchsia.app.discover/module_output.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/module_output.fidl#15)*

 DEPRECATED in favor of StoryModule.

### Write {:#Write}

 Writes the `entity_reference` to the module's `output_parameter_name`
 output. If no entity is provided, the output will be unset.
 Return happens upon completion of a successful write.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_name</code></td>
            <td>
                <code>string[128]</code>
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
                <code><a class='link' href='#ModuleOutputWriter_Write_Result'>ModuleOutputWriter_Write_Result</a></code>
            </td>
        </tr></table>

## SessionDiscoverContext {:#SessionDiscoverContext}
*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#27)*

 Provided to session shells to communicate with discover.

### GetStoryContext {:#GetStoryContext}

 The session shell can act as the story shell. Gets a a story control
 service.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>story_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StoryDiscoverContext'>StoryDiscoverContext</a>&gt;</code>
            </td>
        </tr></table>



## StoryDiscoverContext {:#StoryDiscoverContext}
*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#35)*


### SetProperty {:#SetProperty}

 Sets the value for the given story property |key|.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
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

### GetProperty {:#GetProperty}

 Gets the value for the given story property |key|.

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

### GetSurfaceData {:#GetSurfaceData}

 Gets the surface data for the given |surface_id|.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>surface_id</code></td>
            <td>
                <code>string[1024]</code>
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

## StoryModule {:#StoryModule}
*Defined in [fuchsia.app.discover/story_module.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#13)*


### WriteOutput {:#WriteOutput}

 Writes the `entity_reference` to the module's `output_parameter_name`
 output. If no entity is provided, the output will be unset.
 Return happens upon completion of a successful write.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_name</code></td>
            <td>
                <code>string[128]</code>
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

### IssueIntent {:#IssueIntent}

 Starts a mod by issuing an intent to it or re-issues an intent to the mod
 with the given name.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>intent</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#Intent'>Intent</a></code>
            </td>
        </tr><tr>
            <td><code>mod_name</code></td>
            <td>
                <code>string[512]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Suggestions {:#Suggestions}
*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#12)*


### GetSuggestions {:#GetSuggestions}

 Sends a query to get suggestions and an iterator with which the client
 can fetch suggestions coming as response.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#SuggestionsIterator'>SuggestionsIterator</a>&gt;</code>
            </td>
        </tr></table>



### NotifyInteraction {:#NotifyInteraction}

 Requests the execution of a suggestion's intent.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>suggestion_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>interaction</code></td>
            <td>
                <code><a class='link' href='#InteractionType'>InteractionType</a></code>
            </td>
        </tr></table>



## SuggestionsIterator {:#SuggestionsIterator}
*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#27)*


### Next {:#Next}

 Fetches the next set of suggestions being iterated on. When there's no
 more suggestions an empty vector will be sent and the connection will be
 closed from the server.

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

### ModuleOutputWriter_Write_Response {:#ModuleOutputWriter_Write_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryDiscoverContext_SetProperty_Response {:#StoryDiscoverContext_SetProperty_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### StoryDiscoverContext_GetProperty_Response {:#StoryDiscoverContext_GetProperty_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StoryModule_WriteOutput_Response {:#StoryModule_WriteOutput_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### StoryDiscoverContextError {:#StoryDiscoverContextError}
Type: <code>int32</code>

*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#14)*

 Error code for StoryDiscoverContext services.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STORAGE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>STRING_CONVERSION</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### OutputError {:#OutputError}
Type: <code>int32</code>

*Defined in [fuchsia.app.discover/story_module.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#25)*

 Errors that can occur when writing to an output.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN_NAME</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_ENTITY_REFERENCE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ENTITY_TYPE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### InteractionType {:#InteractionType}
Type: <code>uint32</code>

*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#22)*

 Supported types of interaction with a suggestion.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SELECTED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ModuleIdentifier {:#ModuleIdentifier}


*Defined in [fuchsia.app.discover/discover_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#32)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>story_id</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The ID of the story to which the module belongs.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;[512]</code>
            </td>
            <td> The named path leading up to this module instance. This path is a unique
 identifier of the module in the story.
</td>
        </tr></table>

### SurfaceData {:#SurfaceData}


*Defined in [fuchsia.app.discover/story_discover_context.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#47)*

 Information about a surface in the story.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>action</code></td>
            <td>
                <code>string[512]</code>
            </td>
            <td> The name of the action that triggered the creation of that surface.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>parameter_types</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The types of the parameters for each parameter of the action.
</td>
        </tr></table>

### Suggestion {:#Suggestion}


*Defined in [fuchsia.app.discover/suggestions_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/suggestions_service.fidl#34)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The id of the suggestion. This id is used when notifying an interaction.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>display_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.modular/index.html'>fuchsia.modular</a>/<a class='link' href='../fuchsia.modular/index.html#DisplayInfo'>DisplayInfo</a></code>
            </td>
            <td> Display information about the suggestion.
</td>
        </tr></table>



## **UNIONS**

### ModuleOutputWriter_Write_Result {:#ModuleOutputWriter_Write_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ModuleOutputWriter_Write_Response'>ModuleOutputWriter_Write_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#OutputError'>OutputError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryDiscoverContext_SetProperty_Result {:#StoryDiscoverContext_SetProperty_Result}
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
                <code><a class='link' href='#StoryDiscoverContextError'>StoryDiscoverContextError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryDiscoverContext_GetProperty_Result {:#StoryDiscoverContext_GetProperty_Result}
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
                <code><a class='link' href='#StoryDiscoverContextError'>StoryDiscoverContextError</a></code>
            </td>
            <td></td>
        </tr></table>

### StoryModule_WriteOutput_Result {:#StoryModule_WriteOutput_Result}
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







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#8">STORY_ID_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum length of a story id.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#14">MODULE_PATH_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum length of a module path.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#15">MODULE_PATH_PART_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/module_output.fidl#7">OUTPUT_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/module_output.fidl#8">ENTITY_REFERENCE_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#55">ACTION_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#56">PARAMETER_TYPE_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_discover_context.fidl#57">SURFACE_ID_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/story_module.fidl#9">MODULE_NAME_MAX_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

