[TOC]

# fuchsia.tracing.provider


## **PROTOCOLS**

## Provider {#Provider}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#23)*

<p>The provider interface which applications must implement and register
with the <code>TraceRegistry</code> to participate in tracing.</p>
<p>See //zircon/system/ulib/trace-provider/ for a C++ implementation of
this interface which can easily be configured by an application.</p>

### Initialize {#Initialize}

<p>Initialize tracing and prepare for writing trace records for events in
the specified <code>categories</code> into <code>buffer</code> using <code>fifo</code> for signaling.
Tracing hasn't started yet, a <code>Start()</code> call is still required.</p>
<p>At most one trace can be active at a time. Subsequent <code>Initialize()</code>
requests received prior to a <code>Terminate()</code> call must be ignored.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#ProviderConfig'>ProviderConfig</a></code>
            </td>
        </tr></table>



### Start {#Start}

<p>Begin tracing.</p>
<p>If tracing has already started the provider must ignore the request.</p>
<p>There is no result. The provider must send a <code>TRACE_PROVIDER_STARTED</code>
packet on <code>fifo</code> to indicate success/failure of starting.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#StartOptions'>StartOptions</a></code>
            </td>
        </tr></table>



### Stop {#Stop}

<p>Stop tracing.</p>
<p>If tracing has already stopped the provider must ignore the request.</p>
<p>Once the provider has finished writing any final events to the trace
buffer, it must send a <code>TRACE_PROVIDER_STOPPED</code> packet on <code>fifo</code>.
Note that multiple <code>Start,Stop</code> requests can be received between
<code>Initialize,Terminate</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Terminate {#Terminate}

<p>Terminate tracing.</p>
<p>Tracing is stopped first if not already stopped.
After tracing has fully terminated the provider must close both
<code>buffer</code> and <code>fifo</code> to indicate to the trace manager that tracing is
finished.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Registry {#Registry}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#65)*

<p>The service which trace providers use to register themselves with
the tracing system.
Note that one property of this interface is that once registration is made
the provider can drop this connection.</p>

### RegisterProvider {#RegisterProvider}

<p>Registers the trace provider.
Note: Registration is asynchronous, it's only at some point after this
returns that the provider is actually registered.
To unregister, simply close the Provider pipe.
<code>pid</code> is the process id of the provider, <code>name</code> is the name of the
provider. Both of these are used in logging and diagnostic messages.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='#Provider'>Provider</a></code>
            </td>
        </tr><tr>
            <td><code>pid</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#koid'>koid</a></code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>



### RegisterProviderSynchronously {#RegisterProviderSynchronously}

<p>Registers the trace provider synchronously. The call doesn't return
until the provider is registered.
On return <code>s</code> is <code>ZX_OK</code> if registration was successful.
<code>started</code> is true if tracing has already started, which is a hint to
the provider to wait for the Start() message before continuing if it
wishes to not drop trace records before Start() is received.
To unregister, simply close the Provider pipe.
<code>pid</code> is the process id of the provider, <code>name</code> is the name of the
provider. Both of these are used in logging and diagnostic messages.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>provider</code></td>
            <td>
                <code><a class='link' href='#Provider'>Provider</a></code>
            </td>
        </tr><tr>
            <td><code>pid</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#koid'>koid</a></code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>started</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## **STRUCTS**

### ProviderConfig {#ProviderConfig}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#113)*



<p>Trace provider configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffering_mode</code></td>
            <td>
                <code><a class='link' href='#BufferingMode'>BufferingMode</a></code>
            </td>
            <td><p><code>buffering_mode</code> specifies what happens when the buffer fills.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td><p>The buffer to write trace records into.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fifo</code></td>
            <td>
                <code>handle&lt;fifo&gt;</code>
            </td>
            <td><p>When the trace provider observes <code>ZX_FIFO_PEER_CLOSED</code> on <code>fifo</code>, it
must assume the trace manager has terminated abnormally (since <code>Stop</code>
was not received as usual) and stop tracing automatically, discarding
any in-flight trace data.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>categories</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
            <td><p>What trace categories to collect data for.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### StartOptions {#StartOptions}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#164)*



<p>Additional options to control tracing at start.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer_disposition</code></td>
            <td>
                <code><a class='link' href='#BufferDisposition'>BufferDisposition</a></code>
            </td>
            <td><p>Whether and how to clear the buffer when starting data collection.
This allows, for example, multiple Start/Stop trace runs to be
collected in the same buffer.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_categories</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
            <td><p>The trace categories to add to the initial set provided in
<code>ProviderConfig</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### BufferingMode {#BufferingMode}
Type: <code>uint8</code>

*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#87)*

<p>The trace buffering mode.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ONESHOT</code></td>
            <td><code>1</code></td>
            <td><p>In oneshot mode there is only one buffer that is not reused. When the
buffer fills the provider just keeps dropping records, keeping a count,
and then when tracing stops the header is updated to record final
state.</p>
</td>
        </tr><tr>
            <td><code>CIRCULAR</code></td>
            <td><code>2</code></td>
            <td><p>In circular mode, the buffer is continually written to until tracing
stops. When the buffer fills older records are discarded as needed.</p>
</td>
        </tr><tr>
            <td><code>STREAMING</code></td>
            <td><code>3</code></td>
            <td><p>In streaming mode, the buffer is effectively split into two pieces.
When one half of the buffer fills the provider notifies the trace
manager via the provided fifo, and then starts filling the other half
of the buffer. When the buffer is saved, the manager responds via the
provided fifo. If trace manager hasn't saved the buffer in time, and
the other buffer fills, then the provider is required to drop records
until space becomes available.</p>
</td>
        </tr></table>

### BufferDisposition {#BufferDisposition}
Type: <code>uint8</code>

*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#138)*

<p>Choices for clearing/retaining trace buffer contents at Start.
A brief summary of buffer contents:
The trace buffer is divided into two main pieces: durable and non-durable.
The durable portion contains things like the string and thread data for
their respective references (trace_encoded_string_ref_t and
trace_encoded_thread_ref_t). The non-durable portion contains the rest of
the trace data like events); this is the portion that, for example, is
discarded in circular buffering mode when the (non-durable) buffer fills.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CLEAR_ENTIRE</code></td>
            <td><code>1</code></td>
            <td><p>Clear the entire buffer, including durable buffer contents.
N.B. If this is done mid-session, then string and thread references
from prior to this point will become invalid - the underlying data
will be gone. To prevent this save buffer contents before clearing.</p>
<p>This is typically used when buffer contents were saved after the
preceding Stop.</p>
</td>
        </tr><tr>
            <td><code>CLEAR_NONDURABLE</code></td>
            <td><code>2</code></td>
            <td><p>Clear the non-durable portion of the buffer, retaining the durable
portion.</p>
<p>This is typically used when buffer contents were not saved after the
preceding Stop and the current contents are to be discarded.</p>
</td>
        </tr><tr>
            <td><code>RETAIN</code></td>
            <td><code>3</code></td>
            <td><p>Retain buffer contents. New trace data is added where the previous
trace run left off.</p>
<p>This is typically used when buffer contents were not saved after the
preceding Stop and the current contents are to be retained.</p>
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_PROVIDER_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#10">MAX_PROVIDER_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of a provider's name.</p>
</td>
        </tr>
    <tr id="MAX_NUM_CATEGORIES">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#13">MAX_NUM_CATEGORIES</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of categories supported.</p>
</td>
        </tr>
    <tr id="MAX_CATEGORY_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#16">MAX_CATEGORY_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum length of a category name.</p>
</td>
        </tr>
    
</table>



