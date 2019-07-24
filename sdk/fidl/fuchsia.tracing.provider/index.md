Project: /_project.yaml
Book: /_book.yaml

# fuchsia.tracing.provider


## **PROTOCOLS**

## Provider {:#Provider}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#23)*

 The provider interface which applications must implement and register
 with the `TraceRegistry` to participate in tracing.

 See //zircon/system/ulib/trace-provider/ for a C++ implementation of
 this interface which can easily be configured by an application.

### Initialize {:#Initialize}

 Initialize tracing and prepare for writing trace records for events in
 the specified `categories` into `buffer` using `fifo` for signaling.
 Tracing hasn't started yet, a `Start()` call is still required.


 At most one trace can be active at a time. Subsequent `Initialize()`
 requests received prior to a `Terminate()` call must be ignored.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#ProviderConfig'>ProviderConfig</a></code>
            </td>
        </tr></table>



### Start {:#Start}

 Begin tracing.

 If tracing has already started the provider must ignore the request.

 There is no result. The provider must send a TRACE_PROVIDER_STARTED
 packet on `fifo` to indicate success/failure of starting.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#StartOptions'>StartOptions</a></code>
            </td>
        </tr></table>



### Stop {:#Stop}

 Stop tracing.

 If tracing has already stopped the provider must ignore the request.

 Once the provider has finished writing any final events to the trace
 buffer, it must send a TRACE_PROVIDER_STOPPED packet on `fifo`.
 Note that multiple `Start,Stop` requests can be received between
 `Initialize,Terminate`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Terminate {:#Terminate}

 Terminate tracing.

 Tracing is stopped first if not already stopped.
 After tracing has fully terminated the provider must close both
 `buffer` and `fifo` to indicate to the trace manager that tracing is
 finished.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Registry {:#Registry}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#65)*

 The service which trace providers use to register themselves with
 the tracing system.
 Note that one property of this interface is that once registration is made
 the provider can drop this connection.

### RegisterProvider {:#RegisterProvider}

 Registers the trace provider.
 Note: Registration is asynchronous, it's only at some point after this
 returns that the provider is actually registered.
 To unregister, simply close the Provider pipe.
 `pid` is the process id of the provider, `name` is the name of the
 provider. Both of these are used in logging and diagnostic messages.

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
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>



### RegisterProviderSynchronously {:#RegisterProviderSynchronously}

 Registers the trace provider synchronously. The call doesn't return
 until the provider is registered.
 On return `s` is ZX_OK if registration was successful.
 `started` is true if tracing has already started, which is a hint to
 the provider to wait for the Start() message before continuing if it
 wishes to not drop trace records before Start() is received.
 To unregister, simply close the Provider pipe.
 `pid` is the process id of the provider, `name` is the name of the
 provider. Both of these are used in logging and diagnostic messages.

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
                <code>uint64</code>
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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>started</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## **STRUCTS**

### ProviderConfig {:#ProviderConfig}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#113)*



 Trace provider configuration.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffering_mode</code></td>
            <td>
                <code><a class='link' href='#BufferingMode'>BufferingMode</a></code>
            </td>
            <td> `buffering_mode` specifies what happens when the buffer fills.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The buffer to write trace records into.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fifo</code></td>
            <td>
                <code>handle&lt;fifo&gt;</code>
            </td>
            <td> When the trace provider observes `ZX_FIFO_PEER_CLOSED` on `fifo`, it
 must assume the trace manager has terminated abnormally (since `Stop`
 was not received as usual) and stop tracing automatically, discarding
 any in-flight trace data.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>categories</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
            <td> What trace categories to collect data for.
</td>
            <td>No default</td>
        </tr>
</table>

### StartOptions {:#StartOptions}
*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#164)*



 Additional options to control tracing at start.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer_disposition</code></td>
            <td>
                <code><a class='link' href='#BufferDisposition'>BufferDisposition</a></code>
            </td>
            <td> Whether and how to clear the buffer when starting data collection.
 This allows, for example, multiple Start/Stop trace runs to be
 collected in the same buffer.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_categories</code></td>
            <td>
                <code>vector&lt;string&gt;[100]</code>
            </td>
            <td> The trace categories to add to the initial set provided in
 `ProviderConfig`.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### BufferingMode {:#BufferingMode}
Type: <code>uint8</code>

*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#87)*

 The trace buffering mode.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ONESHOT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CIRCULAR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>STREAMING</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### BufferDisposition {:#BufferDisposition}
Type: <code>uint8</code>

*Defined in [fuchsia.tracing.provider/provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#138)*

 Choices for clearing/retaining trace buffer contents at Start.
 A brief summary of buffer contents:
 The trace buffer is divided into two main pieces: durable and non-durable.
 The durable portion contains things like the string and thread data for
 their respective references (trace_encoded_string_ref_t and
 trace_encoded_thread_ref_t). The non-durable portion contains the rest of
 the trace data like events); this is the portion that, for example, is
 discarded in circular buffering mode when the (non-durable) buffer fills.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CLEAR_ENTIRE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLEAR_NONDURABLE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>RETAIN</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#10">MAX_PROVIDER_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#13">MAX_NUM_CATEGORIES</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-tracing-provider/provider.fidl#16">MAX_CATEGORY_NAME_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

