Project: /_project.yaml
Book: /_book.yaml

# fuchsia.gpu.magma


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.gpu.magma/magma.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.gpu.magma/magma.fidl#10)*


### Query {:#Query}

 Get a parameter.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### QueryReturnsBuffer {:#QueryReturnsBuffer}

 Get a parameter and store it in a new vmo.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>query_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>

### Connect {:#Connect}

 Get the magma ipc channels.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>primary_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>notification_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>

### DumpState {:#DumpState}

 Dumps driver and hardware state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dump_type</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### TestRestart {:#TestRestart}

 For testing only.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Primary {:#Primary}
*Defined in [fuchsia.gpu.magma/magma.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.gpu.magma/magma.fidl#41)*


### ImportBuffer {:#ImportBuffer}

 Imports a buffer for use in the system driver.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>



### ReleaseBuffer {:#ReleaseBuffer}

 Destroys the buffer with `buffer_id` within this connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### ImportObject {:#ImportObject}

 Imports an object for use in the system driver.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>object</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>object_type</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### ReleaseObject {:#ReleaseObject}

 Destroys the object with `object_id` within this connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>object_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>object_type</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### CreateContext {:#CreateContext}

 Creates context `context_id`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### DestroyContext {:#DestroyContext}

 Destroys context `context_id`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### ExecuteCommandBuffer {:#ExecuteCommandBuffer}

 Submits a command buffer for execution on the GPU.
 Note that the buffer referred to by `command_buffer` must contain a valid
 magma_system_command_buffer and all associated data structures
 Transfers ownership of `command_buffer`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>command_buffer</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr><tr>
            <td><code>context_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### ExecuteCommandBufferWithResources {:#ExecuteCommandBufferWithResources}

 Submits a command buffer for execution on the GPU, with associated resources.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>command_buffer</code></td>
            <td>
                <code><a class='link' href='#CommandBuffer'>CommandBuffer</a></code>
            </td>
        </tr><tr>
            <td><code>resources</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Resource'>Resource</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>wait_semaphores</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
        </tr><tr>
            <td><code>signal_semaphores</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
        </tr></table>



### ExecuteImmediateCommands {:#ExecuteImmediateCommands}

 Submits a series of commands for execution on the GPU without using a command buffer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>context_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>command_data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[2048]</code>
            </td>
        </tr><tr>
            <td><code>semaphores</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
        </tr></table>



### GetError {:#GetError}

 Retrieve the current magma error status.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>magma_status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### MapBufferGpu {:#MapBufferGpu}

 Maps `page_count` pages of `buffer` from `page_offset` onto the GPU in the connection's
 address space at `gpu_va`.  `flags` is a set of flags from `MAGMA_GPU_MAP_FLAGS` that
 specify how the GPU can access the buffer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>gpu_va</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>page_offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>page_count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### UnmapBufferGpu {:#UnmapBufferGpu}

 Releases the mapping at `gpu_va` from the GPU.
 Buffers will also be implicitly unmapped when released.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>gpu_va</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CommitBuffer {:#CommitBuffer}

 Ensures that `page_count` pages starting at `page_offset` from the beginning of the
 buffer are backed by physical memory.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>page_offset</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>page_count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>





## **STRUCTS**

### Resource {:#Resource}
*Defined in [fuchsia.gpu.magma/magma.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.gpu.magma/magma.fidl#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>length</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CommandBuffer {:#CommandBuffer}
*Defined in [fuchsia.gpu.magma/magma.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.gpu.magma/magma.fidl#36)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>batch_buffer_resource_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>batch_start_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.gpu.magma/magma.fidl#28">kReceiveBufferSize</a></td>
            <td>
                    <code>2048</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

