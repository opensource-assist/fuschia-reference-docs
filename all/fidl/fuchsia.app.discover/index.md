Project: /_project.yaml
Book: /_book.yaml

# fuchsia.app.discover


## **PROTOCOLS**

## DiscoverRegistry {:#DiscoverRegistry}
*Defined in [fuchsia.app.discover/discover_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#16)*

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



## ModuleOutputWriter {:#ModuleOutputWriter}
*Defined in [fuchsia.app.discover/module_output.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/module_output.fidl#8)*


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
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>entity_reference</code></td>
            <td>
                <code>string?</code>
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
*Defined in [fuchsia.app.discover/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#3)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### OutputError {:#OutputError}
Type: <code>int32</code>

*Defined in [fuchsia.app.discover/module_output.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/module_output.fidl#16)*

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


*Defined in [fuchsia.app.discover/discover_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.app.discover/discover_registry.fidl#21)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>story_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The ID of the story to which the module belongs.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>module_path</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The named path leading up to this module instance. This path is a unique
 identifier of the module in the story.
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
*Defined in [fuchsia.app.discover/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#6)*


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
    
</table>

