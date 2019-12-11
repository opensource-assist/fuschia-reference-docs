[TOC]

# fuchsia.diagnostics.stream


## **PROTOCOLS**

## Source {#Source}
*Defined in [fuchsia.diagnostics.stream/source.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.stream/source.fidl#29)*

<p>A component with records for the Diagnostics system to retrieve.</p>
<p>To record diagnostics, a component allocates a VMO and begins writing records into the buffer,
incrementing a header value after each write to inform readers how much of the buffer has been
filled.</p>
<p>If any retrievers are connected, the <code>Source</code> sends them <code>OnBufferInit</code> events for each
diagnostic buffer created.</p>
<p>When the buffer fills, the <code>Source</code> sends <code>OnBufferDone</code> to the retrievers, and will wait for
all notified retrievers to reply with <code>RetireBuffer</code> when they have finished reading from the
buffer.</p>
<p>When all readers of the buffer have finished, the <code>Source</code> may recycle the buffer by zeroing it
and sending <code>OnBufferInit</code> again to connected retrievers.</p>
<p>Once a <code>Source</code> has sent <code>OnBufferDone</code> to a retriever, it is up to the <code>Source</code> to handle new
records that are generated while the retriever drains the buffer. Double buffering is
recommended to prevent excessive blocking, but this protocol does not mandate a specific
approach to handling records generated while buffers are full.</p>

### OnBufferInit {#OnBufferInit}

<p>Notifies the connected retriever of a new stream buffer. Should be emitted as soon as each
buffer is (re)initialized.</p>
<p><code>latest</code> should be read-only.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>latest</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>

### OnBufferDone {#OnBufferDone}

<p>Asks the connected retriever to finish working with <code>buffer</code>, usually because the <code>Source</code>
does not intend to write further records.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#koid'>koid</a></code>
            </td>
        </tr></table>

### RetireBuffer {#RetireBuffer}

<p>Notifies the <code>Source</code> that the retriever is done reading from the buffer. If the <code>Source</code>
wishes it should zero the buffer's contents and recycle it for future records. Buffers must
be re-sent via <code>OnBufferInit</code> after they're zeroed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#koid'>koid</a></code>
            </td>
        </tr></table>



### RegisterInterest {#RegisterInterest}

<p>Notifies the component of interest in a subset of diagnostic records.</p>
<p>Before the component receives this request it should filter according to a default interest
specifier.</p>
<p>After receiving this message components begin writing records according to the new
specifier. <code>Source</code> components must be prepared to handle multiple client connections,
and may filter records according to the union of all interest specifiers. Clients may
receive records outside the scope of their interest.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>desired</code></td>
            <td>
                <code><a class='link' href='#Interest'>Interest</a></code>
            </td>
        </tr></table>







## **ENUMS**

### Severity {#Severity}
Type: <code>uint32</code>

*Defined in [fuchsia.diagnostics.stream/source.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.stream/source.fidl#67)*

<p>The severity of a given record.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FATAL</code></td>
            <td><code>5</code></td>
            <td><p>Components should only record fatal records prior to terminating operation. Fatal
records are informative only, and front-end libraries which trigger an exit in response
to them should clearly document this behavior to their users.</p>
</td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>4</code></td>
            <td><p>Components should include error records as well as more severe records.</p>
</td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>3</code></td>
            <td><p>Components should include warning records as well as more severe records.</p>
</td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>2</code></td>
            <td><p>Components should include informative records as well as more severe records. (default)</p>
</td>
        </tr><tr>
            <td><code>DEBUG</code></td>
            <td><code>1</code></td>
            <td><p>Components should include developer-facing debug records as well as more severe records.</p>
</td>
        </tr><tr>
            <td><code>ANY</code></td>
            <td><code>0</code></td>
            <td><p>Components should include all records.</p>
</td>
        </tr></table>



## **TABLES**

### Interest {#Interest}


*Defined in [fuchsia.diagnostics.stream/source.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.stream/source.fidl#61)*

<p>The system's current interest in records.</p>
<p>Without having received an interest specifier or receiving one with empty fields, components
should assume a default interest specifier, as documented for each field in this table.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>min_severity</code></td>
            <td>
                <code><a class='link' href='#Severity'>Severity</a></code>
            </td>
            <td><p>Minimum desired severity. The default is <code>INFO</code>.</p>
</td>
        </tr></table>











