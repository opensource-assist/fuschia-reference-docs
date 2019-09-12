Project: /_project.yaml
Book: /_book.yaml

# fuchsia.diagnostics.inspect


## **PROTOCOLS**

## Reader {:#Reader}
*Defined in [fuchsia.diagnostics.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/inspect.fidl#62)*


### AddSelector {:#AddSelector}

 Adds a [fuchsia.diagnostics.inspect/ReaderSelector] to the Inspect instance,
 which will be used when determining which Inspect data to parse and return.
 + request `selector` a [fuchsia.diagnostics.inspect/ReaderSelector]
   defining a specific component-hierarchy and inspect-tree pattern
   of interest to the client.
 * error a [fuchsia.diagnostics.inspect/ReaderError]
   value indicating how the call failed.
   - `UNIMPLEMENTED_FORMAT` means that a selector whose format is
     not yet supported was provided.

   - `INVALID_SELECTOR` means that a selector which had an invalid
     structure was passed in and failed verficiation.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>selector</code></td>
            <td>
                <code><a class='link' href='#ReaderSelector'>ReaderSelector</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Reader_AddSelector_Result'>Reader_AddSelector_Result</a></code>
            </td>
        </tr></table>

### ClearSelectors {:#ClearSelectors}

 Removes all previously added ReaderSelectors from the Inspect instance.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Format {:#Format}

 Parses the inspect data of the component hierarchy into a format
 specified by the [fuchsia.diagnostics.inspect/FormatSettings] struct,
 dump that formatted string to a VMO, and return a buffer to the VMO.

 The inspect data which is parsed is defined both by the static
 configuration of the service and the ReaderSelectors which are
 currently added to the instance. If no added ReaderSelectors
 have been added to the current instance, the default behavior
 is to parse all Inspect data that the instance has access to.

 + request `settings` the `fuchsia.diagnostics.inspect/FormatSettings` that
   specifies the format of the read Inspect data.
 - response `inspect_data_result` the `fuchsia.mem/Buffer` which contains
   the formatted inspect data.
 * error a [fuchsia.diagnostics.inspect/ReaderError]
   value indicating how the call failed.
   - `IO` means that parsing the Inspect VMO or writing the formatted data
      failed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#FormatSettings'>FormatSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Reader_Format_Result'>Reader_Format_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Reader_AddSelector_Response {:#Reader_AddSelector_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Reader_Format_Response {:#Reader_Format_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>inspect_data_result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### JsonSettings {:#JsonSettings}
*Defined in [fuchsia.diagnostics.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/inspect.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>indent</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TextSettings {:#TextSettings}
*Defined in [fuchsia.diagnostics.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/inspect.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>indent</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Selector {:#Selector}
*Defined in [fuchsia.diagnostics.inspect/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/selector.fidl#60)*



 Structured selector containing all required information for the
 Inspect service to provide specific views into inspect data.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>component_selector</code></td>
            <td>
                <code><a class='link' href='../fuchsia.diagnostics/index.html'>fuchsia.diagnostics</a>/<a class='link' href='../fuchsia.diagnostics/index.html#ComponentSelector'>ComponentSelector</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tree_selector</code></td>
            <td>
                <code><a class='link' href='#TreeSelector'>TreeSelector</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ReaderError {:#ReaderError}
Type: <code>uint32</code>

*Defined in [fuchsia.diagnostics.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/inspect.fidl#34)*

 Enums describing the potential fail states
 of the reader service.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNIMPLEMENTED_FORMAT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_SELECTOR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>IO</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### FormatSettings {:#FormatSettings}


*Defined in [fuchsia.diagnostics.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/inspect.fidl#28)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#DisplaySettings'>DisplaySettings</a></code>
            </td>
            <td></td>
        </tr></table>

### TreeSelector {:#TreeSelector}


*Defined in [fuchsia.diagnostics.inspect/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/selector.fidl#45)*

 TreeSelector represents a selection request on a nested structure where each
 nested node has properties that can be retrieved. The node_path specifies which
 nodes we search through, and the target_properties specify which properties to
 look for on the matched nodes.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_path</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.diagnostics/index.html'>fuchsia.diagnostics</a>/<a class='link' href='../fuchsia.diagnostics/index.html#PathSelectionNode'>PathSelectionNode</a>&gt;[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>target_properties</code></td>
            <td>
                <code><a class='link' href='#PropertySelector'>PropertySelector</a></code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### Reader_AddSelector_Result {:#Reader_AddSelector_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Reader_AddSelector_Response'>Reader_AddSelector_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ReaderError'>ReaderError</a></code>
            </td>
            <td></td>
        </tr></table>

### Reader_Format_Result {:#Reader_Format_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Reader_Format_Response'>Reader_Format_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ReaderError'>ReaderError</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### DisplaySettings {:#DisplaySettings}
*Defined in [fuchsia.diagnostics.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/inspect.fidl#22)*

 Criteria for how to format
 the selected Inspect data.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>json</code></td>
            <td>
                <code><a class='link' href='#JsonSettings'>JsonSettings</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code><a class='link' href='#TextSettings'>TextSettings</a></code>
            </td>
            <td></td>
        </tr></table>

### ReaderSelector {:#ReaderSelector}
*Defined in [fuchsia.diagnostics.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/inspect.fidl#44)*

 Selection criteria for data returned by the Reader service.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>structured_selector</code></td>
            <td>
                <code><a class='link' href='#Selector'>Selector</a></code>
            </td>
            <td> The reader applies the selection defined
 by structured_selector to all possible inspect data that it
 has access to, returning a potential subset, but not superset,
 of what would be returned by selection using only the system
 configuration.
</td>
        </tr><tr>
            <td><code>string_selector</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td> The reader parses the string-based selector
 string_selector into a structured selector and then will apply
 the selection defined by structured_selector to all possible inspect
 data that it has access to, returning a potential subset, but
 not a superset of what would be returned by selection using only the
 system configuration.
</td>
        </tr></table>

### PropertySelector {:#PropertySelector}
*Defined in [fuchsia.diagnostics.inspect/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/selector.fidl#36)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>string_pattern</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>wildcard</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>





