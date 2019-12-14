[TOC]

# fuchsia.hardware.cpu.insntrace


## **PROTOCOLS**

## Controller {#Controller}
*Defined in [fuchsia.hardware.cpu.insntrace/insntrace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#83)*


### Initialize {#Initialize}

<p>Initialize the trace.
This does not include allocating space for the trace buffers, that is
done later by |AllocateBuffer()|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>allocation</code></td>
            <td>
                <code><a class='link' href='#Allocation'>Allocation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_Initialize_Result'>Controller_Initialize_Result</a></code>
            </td>
        </tr></table>

### Terminate {#Terminate}

<p>Free all trace buffers and any other resources allocated for the trace.
This is also done when the connection is closed (as well as stopping
the trace).
May be called multiple times.
This can only fail when tracing in THREAD mode where tracing is
terminated differently, in which case the error is <code>ZX_ERR_BAD_STATE</code>.</p>

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
                <code><a class='link' href='#Controller_Terminate_Result'>Controller_Terminate_Result</a></code>
            </td>
        </tr></table>

### GetAllocation {#GetAllocation}

<p>Return the trace allocation configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>allocation</code></td>
            <td>
                <code><a class='link' href='#Allocation'>Allocation</a>?</code>
            </td>
        </tr></table>

### AllocateBuffer {#AllocateBuffer}

<p>Allocate a trace buffer.
When tracing cpus, buffers are auto-assigned to cpus: the resulting
trace buffer descriptor is the number of the cpu using the buffer.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#BufferConfig'>BufferConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_AllocateBuffer_Result'>Controller_AllocateBuffer_Result</a></code>
            </td>
        </tr></table>

### AssignThreadBuffer {#AssignThreadBuffer}

<p>Assign a buffer to a thread.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#BufferDescriptor'>BufferDescriptor</a></code>
            </td>
        </tr><tr>
            <td><code>thread</code></td>
            <td>
                <code>handle&lt;thread&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_AssignThreadBuffer_Result'>Controller_AssignThreadBuffer_Result</a></code>
            </td>
        </tr></table>

### ReleaseThreadBuffer {#ReleaseThreadBuffer}

<p>Release a previously assigned buffer from a thread.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#BufferDescriptor'>BufferDescriptor</a></code>
            </td>
        </tr><tr>
            <td><code>thread</code></td>
            <td>
                <code>handle&lt;thread&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_ReleaseThreadBuffer_Result'>Controller_ReleaseThreadBuffer_Result</a></code>
            </td>
        </tr></table>

### GetBufferConfig {#GetBufferConfig}

<p>Fetch a buffer's configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#BufferDescriptor'>BufferDescriptor</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#BufferConfig'>BufferConfig</a>?</code>
            </td>
        </tr></table>

### GetBufferState {#GetBufferState}

<p>Fetch runtime information about a buffer.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#BufferDescriptor'>BufferDescriptor</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#BufferState'>BufferState</a>?</code>
            </td>
        </tr></table>

### GetChunkHandle {#GetChunkHandle}

<p>Fetch the handle of a chunk of a trace buffer.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#BufferDescriptor'>BufferDescriptor</a></code>
            </td>
        </tr><tr>
            <td><code>chunk_num</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### FreeBuffer {#FreeBuffer}

<p>Free a previously allocated trace buffer.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#BufferDescriptor'>BufferDescriptor</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start tracing.
Must be called after |Initialize()| + |AllocateBuffer()|,
with tracing off.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Stop {#Stop}

<p>Stop tracing.
May be called any time after |Allocate()| has been called and before
|Free()|. If called at other times the call is ignored.
May be called multiple times.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Controller_Initialize_Response {#Controller_Initialize_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_Terminate_Response {#Controller_Terminate_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_AllocateBuffer_Response {#Controller_AllocateBuffer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#BufferDescriptor'>BufferDescriptor</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_AssignThreadBuffer_Response {#Controller_AssignThreadBuffer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_ReleaseThreadBuffer_Response {#Controller_ReleaseThreadBuffer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Allocation {#Allocation}
*Defined in [fuchsia.hardware.cpu.insntrace/insntrace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#27)*



<p>The allocation configuration of a trace.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#Mode'>Mode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>num_traces</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddressRange {#AddressRange}
*Defined in [fuchsia.hardware.cpu.insntrace/insntrace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#40)*



<p>An address range, as [start,end].</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>start</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>end</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BufferConfig {#BufferConfig}
*Defined in [fuchsia.hardware.cpu.insntrace/insntrace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#46)*



<p>A buffer's configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>num_chunks</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>A &quot;buffer&quot; is made up of |num_chunks| chunks with each chunk having
size |1&lt;&lt;chunk_order| pages.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>chunk_order</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>log2 of the number of pages</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_circular</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true then use circular buffering.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ctl</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The value of the control register.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>address_space_match</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>If non-zero then the address space of the instruction must match in
order for the instruction to be traced. On x86 architectures the
address space is specified by CR3.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>address_range_0</code></td>
            <td>
                <code><a class='link' href='#AddressRange'>AddressRange</a></code>
            </td>
            <td><p>If non-zero, tracing is restricted to these address ranges.
TODO(dje): There's only two, and vectors don't currently work here,
so spell these out individually</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>address_range_1</code></td>
            <td>
                <code><a class='link' href='#AddressRange'>AddressRange</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BufferState {#BufferState}
*Defined in [fuchsia.hardware.cpu.insntrace/insntrace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#73)*



<p>A buffer's runtime state.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>capture_end</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>This is the offset in the buffer where tracing stopped (treating all
buffers as one large one). If using a circular buffer then all of the
buffer may contain data, there's no current way to know if tracing
wrapped without scanning records.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Mode {#Mode}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.cpu.insntrace/insntrace.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#19)*

<p>Tracing modes</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CPU</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>THREAD</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Controller_Initialize_Result {#Controller_Initialize_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Initialize_Response'>Controller_Initialize_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_Terminate_Result {#Controller_Terminate_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Terminate_Response'>Controller_Terminate_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_AllocateBuffer_Result {#Controller_AllocateBuffer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_AllocateBuffer_Response'>Controller_AllocateBuffer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_AssignThreadBuffer_Result {#Controller_AssignThreadBuffer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_AssignThreadBuffer_Response'>Controller_AssignThreadBuffer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Controller_ReleaseThreadBuffer_Result {#Controller_ReleaseThreadBuffer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_ReleaseThreadBuffer_Response'>Controller_ReleaseThreadBuffer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="API_VERSION">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#9">API_VERSION</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAX_NUM_TRACES">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#13">MAX_NUM_TRACES</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint16</code></td>
            <td><p>The maximum number of traces that can be collected at once.
A &quot;trace&quot; is the instruction stream for one entity, cpu or thread.</p>
</td>
        </tr>
    <tr id="MAX_NUM_ADDR_RANGES">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#16">MAX_NUM_ADDR_RANGES</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint16</code></td>
            <td><p>The maximum number of supported address ranges.</p>
</td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="BufferDescriptor">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-cpu-insntrace/insntrace.fidl#81">BufferDescriptor</a></td>
            <td>
                <code>uint32</code></td>
            <td></td>
        </tr></table>

