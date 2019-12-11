[TOC]

# fuchsia.diagnostics


## **PROTOCOLS**

## Archive {#Archive}
*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#64)*

<p>Outer protocol for interacting with the different diagnostics data sources.</p>

### ReadInspect {#ReadInspect}

<p>Creates a Reader for interacting with Inspect data.
The resulting interface can be used to analyze Inspect hierarchy data
scoped to the components specified by the static configurations of the Accessor
pipeline that the client connects to, and the provided selectors vector argument.</p>
<ul>
<li>request <code>inspect_reader</code> is a [fuchsia.diagnostics/Reader] that processes
Reader requests, sitting on top of inspect data.</li>
<li>request <code>selectors</code> is a vector of [fuchsia.diagnostics/SelectorArgument] which
provide additional filters to scope data with. If the vector is empty,
all available results are returned.
.</li>
</ul>
<ul>
<li>error a [fuchsia.diagnostics/AccessorError]
value indicating that the provided selectors failed to verify.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>inspect_reader</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Reader'>Reader</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>selectors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SelectorArgument'>SelectorArgument</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Archive_ReadInspect_Result'>Archive_ReadInspect_Result</a></code>
            </td>
        </tr></table>

### ReadLogs {#ReadLogs}

<p>Creates a Reader for interacting with structured Log data.
The resulting interface can be used to analyze structured Log data
scoped to the components specified by the static configurations of the Accessor
pipeline that the client connects to, and the provided selectors vector argument.</p>
<ul>
<li>request <code>log_reader</code> is a [fuchsia.diagnostics/Reader] that processes
Reader requests, sitting on top of Log data.</li>
<li>request <code>selectors</code> is a vector of [fuchsia.diagnostics/SelectorArgument] which
provide additional filters to scope data with. If the vector is empty,
all available results are returned.</li>
</ul>
<ul>
<li>error a [fuchsia.diagnostics/AccessorError]
value indicating that the provided selectors failed to verify.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log_reader</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Reader'>Reader</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>selectors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SelectorArgument'>SelectorArgument</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Archive_ReadLogs_Result'>Archive_ReadLogs_Result</a></code>
            </td>
        </tr></table>

### ReadLifecycleEvents {#ReadLifecycleEvents}

<p>Creates a Reader for interacting with lifecycle event data.
The resulting interface can be used to analyze lifecycle event data
scoped to the components specified by the static configurations of the Accessor
pipeline that the client connects to, and the provided selectors vector argument.</p>
<ul>
<li>request <code>lifecycle_reader</code> is a [fuchsia.diagnostics/Reader] that processes Reader
requests, sitting on top of lifecycle event data.</li>
<li>request <code>selectors</code> is a vector of [fuchsia.diagnostics/SelectorArgument] which
provide additional filters to scope data with. If the vector is empty,
all available results are returned.</li>
</ul>
<ul>
<li>error a [fuchsia.diagnostics/AccessorError]
value indicating that the provided selectors failed to verify.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lifecycle_reader</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Reader'>Reader</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>selectors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SelectorArgument'>SelectorArgument</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Archive_ReadLifecycleEvents_Result'>Archive_ReadLifecycleEvents_Result</a></code>
            </td>
        </tr></table>

## Reader {#Reader}
*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#117)*

<p>A protocol to access data from a particular data source.</p>

### GetSnapshot {#GetSnapshot}

<p>Filters the data hierarchies of components based on the statically provided allowlists
and the selectors provided by the accessor request, formats these filtered data
hierarchies according to the specified [fuchsia.diagnostics/FormatSettings]
argument, then serves the resulting data hierarchies over a BatchIterator.</p>
<ul>
<li>request <code>format_settings</code> the [fuchsia.diagnostics/FormatSettings] that
specifies the format of data returned by the BatchIterator.</li>
<li>request <code>result_iterator</code> is a [fuchsia.diagnostics.BatchIterator] that
processes client requests to fetch [fuchsia.diagnostics/FormattedContent]
structs from the current snapshot.</li>
</ul>
<ul>
<li>error a [fuchsia.diagnostics/ReaderError]
value indicating that there was an issue configuring the BatchIterator
connection.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#Format'>Format</a></code>
            </td>
        </tr><tr>
            <td><code>result_iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BatchIterator'>BatchIterator</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Reader_GetSnapshot_Result'>Reader_GetSnapshot_Result</a></code>
            </td>
        </tr></table>

### ReadStream {#ReadStream}

<p>Creates a Stream for polling a Reader data sources for new data.
The resulting interface can be used retrieve the next batch of data matching
which is within the ComponentSelector and TreeSelector scopes defined by the Archive
and Reader protocols through which this stream was created, in addition to the
static configurations that define the allowlist of data the reader has access to.</p>
<ul>
<li>request <code>format_settings</code> the [fuchsia.diagnostics/FormatSettings] that
specifies the format of data returned by the Batch during
FormatBatch calls.</li>
<li>request <code>stream_mode</code> is a [fuchsia.diagnostics/StreamMode] that specifies how the
streaming server provides streamed results.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_mode</code></td>
            <td>
                <code><a class='link' href='#StreamMode'>StreamMode</a></code>
            </td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#Format'>Format</a></code>
            </td>
        </tr><tr>
            <td><code>formatted_stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Stream'>Stream</a>&gt;</code>
            </td>
        </tr></table>



## Stream {#Stream}
*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#166)*

<p>Protocol offering an API for batch-retrieving all newly updated diagnostics data sincee
the last call.</p>

### GetBatch {#GetBatch}

<p>Retrieves the batch of data which has appeared since the last GetNext call and matches
the configured ComponentSelector and TreeSelector scopes, in addition to the
static configurations that define the allowlist of data the reader has access to.</p>
<p>The batch of data which has appeared since the last FormatNext call is formatted
according to the FormatSettings provided to the ReadStream call
which created the connection and then is served over a BatchIterator.</p>
<p>If no new data has appeared since the last FormatBatch call, the BatchIterator
that starts serving over <code>batch_iterator</code> will just serve an empty vector, and then
close.</p>
<ul>
<li>request <code>batch_iterator</code> is a [fuchsia.diagnostics.BatchIterator] that
processes client requests to fetch [fuchsia.diagnostics/FormattedContent]
structs encoding newly available data from the data hierarchies the Reader that spawned
this stream is sitting upon.</li>
</ul>
<ul>
<li>error a [fuchsia.diagnostics/ReaderError]
value indicating that there was an issue configuring the Batch
connection for the stream data.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>batch_iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BatchIterator'>BatchIterator</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stream_GetBatch_Result'>Stream_GetBatch_Result</a></code>
            </td>
        </tr></table>

## BatchIterator {#BatchIterator}
*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#193)*

<p>Conceptually, a directory iterator, where each element in the iterator is a single
complete file that can be concatenated with other results.</p>

### GetNext {#GetNext}

<p>Returns a vector of [fuchsia.diagnostics/FormattedContent] structs
with a format dictated by the format_settings argument provided to the Reader protocol
which spawned this BatchIterator.</p>
<p>An empty vector implies that the data hierarchy has been fully iterated, and subsequent
GetNext calls will return no data.</p>
<ul>
<li>returns a vector of FormattedContent structs. Clients connected to a
Batch are expected to call GetNext() until an empty vector
is returned, denoting that the entire data hierarchy has been read.</li>
</ul>
<ul>
<li>error a [fuchsia.diagnostics/ReaderError]
value indicating that there was an issue reading the underlying data hierarchies
or formatting those hierarchies to populate the <code>batch</code>. Note, these
issues do not include a single component's data hierarchy failing to be read.
The iterator is tolerant of individual component data sources failing to be read,
whether that failure is a timeout or a malformed binary file.
In the event that a GetNext call fails, that subset of the data hierarchy results is
dropped, but future calls to GetNext will provide new subsets of
FormattedDataHierarchies.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#BatchIterator_GetNext_Result'>BatchIterator_GetNext_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Archive_ReadInspect_Response {#Archive_ReadInspect_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Archive_ReadLogs_Response {#Archive_ReadLogs_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Archive_ReadLifecycleEvents_Response {#Archive_ReadLifecycleEvents_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Reader_GetSnapshot_Response {#Reader_GetSnapshot_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stream_GetBatch_Response {#Stream_GetBatch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### BatchIterator_GetNext_Response {#BatchIterator_GetNext_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>batch</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FormattedContent'>FormattedContent</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Selector {#Selector}
*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#86)*



<p>Structured selector containing all required information for pattern-matching onto
string-named properties owned by nodes in a data hierarchy, where data hierarchies belong
to specific components.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>component_selector</code></td>
            <td>
                <code><a class='link' href='#ComponentSelector'>ComponentSelector</a></code>
            </td>
            <td><p>The selector defining a pattern of component monikers to match
against.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>tree_selector</code></td>
            <td>
                <code><a class='link' href='#TreeSelector'>TreeSelector</a></code>
            </td>
            <td><p>The selector defining data hierarchy properties to match against
within the data hierarchies owned by components matched by
<code>component_selector</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Format {#Format}
Type: <code>uint32</code>

*Defined in [fuchsia.diagnostics/format.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/format.fidl#9)*

<p>Enum used to specify the output format for
Reader results.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>JSON</code></td>
            <td><code>1</code></td>
            <td><p>Dump read results per the Diagnostics Json
Schema specifications.</p>
</td>
        </tr><tr>
            <td><code>TEXT</code></td>
            <td><code>2</code></td>
            <td><p>Dump read results per the Iquery text specifications.</p>
</td>
        </tr></table>

### AccessorError {#AccessorError}
Type: <code>uint32</code>

*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#14)*

<p>Enum describing the potential fail-states of the Accessor service.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID_SELECTOR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### ReaderError {#ReaderError}
Type: <code>uint32</code>

*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#23)*

<p>Enum describing the potential fail-states of the Accessor service due to issues
reading the data.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IO</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### StreamMode {#StreamMode}
Type: <code>uint8</code>

*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#150)*

<p>Enum specifying the modes by which a user can connect to and stream diagnostics metrics.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>REPLAY_ONLY</code></td>
            <td><code>1</code></td>
            <td><p>The first call to FormatBatch will serve the historical polling records of metrics
configured to store state in buffers, then the server will close.</p>
</td>
        </tr><tr>
            <td><code>REPLAY_THEN_ONGOING</code></td>
            <td><code>2</code></td>
            <td><p>The first call to FormatBatch will serve the historical polling records of metrics
configured to store state in buffers, then will close. Subsequent calls to FormatBatch
will return newly polled records that were taken since the last FormatBatch call.</p>
</td>
        </tr><tr>
            <td><code>ONGOING_ONLY</code></td>
            <td><code>3</code></td>
            <td><p>The first call to FormatBatch will return newly polled records that were taken
since the client connection was established. Subsequent calls to FormatBatch
will return newly polled records that were taken since the last FormatBatch call.</p>
</td>
        </tr></table>



## **TABLES**

### ComponentSelector {#ComponentSelector}


*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#46)*

<p>ComponentSelector encodes path to a component that is being selected for.
The <code>component_moniker</code> specifies a pattern of component relative monikers which
identify components being selected for.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>moniker_segments</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StringSelector'>StringSelector</a>&gt;[25]</code>
            </td>
            <td><p>Vector encoding the a pattern for monikers of components being selected for.
These monikers are child-monikers relative to a &quot;root&quot; hierarchy that the archivist
is aware of.</p>
<p>There must be at least one StringSelector provided, which
specifies the component names that are matched by
the current selector.
TODO(4601): Investigate options for introduction of recursive wildcards.</p>
</td>
        </tr></table>

### TreeSelector {#TreeSelector}


*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#67)*

<p>TreeSelector represents a selection request on a nested structure where each
nested node has properties that can be retrieved. The node_path specifies which
nodes we search through, and the target_properties specify which properties to
look for on the matched nodes.</p>
<p>Given that a Tree Selector has two sections, <object node selector>:<property selector>,
in the absence of an optional property_selector, we return the subtree of all nodes specified
by the object node selector.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_path</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StringSelector'>StringSelector</a>&gt;[100]</code>
            </td>
            <td><p>A vector of StringSelectors which serve as a pattern matcher
for paths through a hierarchy of named nodes.</p>
<p>This field is required.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>target_properties</code></td>
            <td>
                <code><a class='link' href='#StringSelector'>StringSelector</a></code>
            </td>
            <td><p>A StringSelector which serves as a pattern matcher for
string-named properties on a node in a data hierarchy.</p>
<p>This field is optional. Without a property selector, the TreeSelector
will select the entire subtree of all nodes selected by the node_path.</p>
</td>
        </tr></table>



## **UNIONS**

### Archive_ReadInspect_Result {#Archive_ReadInspect_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Archive_ReadInspect_Response'>Archive_ReadInspect_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#AccessorError'>AccessorError</a></code>
            </td>
            <td></td>
        </tr></table>

### Archive_ReadLogs_Result {#Archive_ReadLogs_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Archive_ReadLogs_Response'>Archive_ReadLogs_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#AccessorError'>AccessorError</a></code>
            </td>
            <td></td>
        </tr></table>

### Archive_ReadLifecycleEvents_Result {#Archive_ReadLifecycleEvents_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Archive_ReadLifecycleEvents_Response'>Archive_ReadLifecycleEvents_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#AccessorError'>AccessorError</a></code>
            </td>
            <td></td>
        </tr></table>

### Reader_GetSnapshot_Result {#Reader_GetSnapshot_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Reader_GetSnapshot_Response'>Reader_GetSnapshot_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ReaderError'>ReaderError</a></code>
            </td>
            <td></td>
        </tr></table>

### Stream_GetBatch_Result {#Stream_GetBatch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stream_GetBatch_Response'>Stream_GetBatch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ReaderError'>ReaderError</a></code>
            </td>
            <td></td>
        </tr></table>

### BatchIterator_GetNext_Result {#BatchIterator_GetNext_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#BatchIterator_GetNext_Response'>BatchIterator_GetNext_Response</a></code>
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

### SelectorArgument {#SelectorArgument}
*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#31)*

<p>Argument used for Archive selectors, can be either the pre-parsed
fidl struct or string representation.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>structured_selector</code></td>
            <td>
                <code><a class='link' href='#Selector'>Selector</a></code>
            </td>
            <td><p>A Selector defining a pattern-matcher which selects for components within a hierarchy
and properties in a data hierarchy namespaced by component.</p>
</td>
        </tr><tr>
            <td><code>raw_selector</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td><p>The Archive protocol parses the raw_selector
into a structured [fuchsia.diagnostics/Selector]
The Selector defines a pattern-matcher which selects for components within a hierarchy
and properties in a data hierarchy namespaced by component.
NOTE: All StringSelectors parsed from the raw_selector will be interperetted in
string_pattern mode, giving significance to special characters.
TODO(4601): Link to in-tree documentation for raw selector strings.</p>
</td>
        </tr></table>

### FormattedContent {#FormattedContent}
*Defined in [fuchsia.diagnostics/reader.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#48)*

<p>A fidl union containing a complete hierarchy of structured diagnostics
data, such that the content can be parsed into a file by itself.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>formatted_json_hierarchy</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>A complete formatted data hierarchy encoded as json.
Data hierarchies are the hierarchical representation
of the structured diagnostics data on the system.
The VMO will contain up to 1mb of diagnostics data,
with dropped subtrees if the hierarchy is too large.</p>
</td>
        </tr><tr>
            <td><code>formatted_text_hierarchy</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td><p>A complete formatted data hierarchy encoded as text.
The VMO will contain up to 1mb of diagnostics data,
with dropped subtrees if the hierarchy is too large.</p>
</td>
        </tr></table>

### StringSelector {#StringSelector}
*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#20)*

<p>StringSelector is an xunion defining different ways to describe a pattern to match
strings against.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>string_pattern</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>This is a provided string that defines a pattern to
match against. The parser treats asterisks (*), colons (:) and backslashes
() as special characters.</p>
<p>If you wish to match against literal asterisks (*), they must be escaped.
If you wish to match against literal backslashes (), they must be escaped.
If you wish to match against literal colons (:), they must be escaped.</p>
<p>eg: abc will match any string with the exact name &quot;abc&quot;.
eg: a* will match any string with the exact name &quot;a*&quot;.
eg: a\* will match any that starts with exactly &quot;a&quot;.
eg: a* will match any string that starts with &quot;a&quot;.
eg: a<em>b will match any string that starts with a and ends with b.
eg: a</em>b*c will match any string that starts with a and ends with c, with <code>b</code>
in the middle.</p>
</td>
        </tr><tr>
            <td><code>exact_match</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>This is a provided string that defines an exact string to match against. No
characters are treated as special, or carry special syntax.</p>
</td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAXIMUM_RAW_SELECTOR_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/reader.fidl#11">MAXIMUM_RAW_SELECTOR_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint16</code></td>
            <td><p>The size bound of 1024 is a reasonably low size restriction that meets most
canonical selectors we've ecountered.</p>
</td>
        </tr>
    <tr id="MAXIMUM_STRING_SELECTOR_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#8">MAXIMUM_STRING_SELECTOR_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAXIMUM_MONIKER_SEGMENTS">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#12">MAXIMUM_MONIKER_SEGMENTS</a></td>
            <td>
                    <code>25</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAXIMUM_DATA_HIERARCHY_DEPTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#16">MAXIMUM_DATA_HIERARCHY_DEPTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>



