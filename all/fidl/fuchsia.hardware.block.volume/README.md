[TOC]

# fuchsia.hardware.block.volume


## **PROTOCOLS**

## VolumeManager {#VolumeManager}
*Defined in [fuchsia.hardware.block.volume/volume.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block-volume/volume.fidl#50)*


### AllocatePartition {#AllocatePartition}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>slice_count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block.partition/'>fuchsia.hardware.block.partition</a>/<a class='link' href='../fuchsia.hardware.block.partition/#GUID'>GUID</a></code>
            </td>
        </tr><tr>
            <td><code>instance</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block.partition/'>fuchsia.hardware.block.partition</a>/<a class='link' href='../fuchsia.hardware.block.partition/#GUID'>GUID</a></code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]</code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### Query {#Query}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#VolumeInfo'>VolumeInfo</a>?</code>
            </td>
        </tr></table>

### GetInfo {#GetInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#VolumeManagerInfo'>VolumeManagerInfo</a>?</code>
            </td>
        </tr></table>

### Activate {#Activate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>old_guid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block.partition/'>fuchsia.hardware.block.partition</a>/<a class='link' href='../fuchsia.hardware.block.partition/#GUID'>GUID</a></code>
            </td>
        </tr><tr>
            <td><code>new_guid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block.partition/'>fuchsia.hardware.block.partition</a>/<a class='link' href='../fuchsia.hardware.block.partition/#GUID'>GUID</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

## Volume {#Volume}
*Defined in [fuchsia.hardware.block.volume/volume.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block-volume/volume.fidl#103)*


### GetInfo {#GetInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block/'>fuchsia.hardware.block</a>/<a class='link' href='../fuchsia.hardware.block/#BlockInfo'>BlockInfo</a>?</code>
            </td>
        </tr></table>

### GetStats {#GetStats}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>clear</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block/'>fuchsia.hardware.block</a>/<a class='link' href='../fuchsia.hardware.block/#BlockStats'>BlockStats</a>?</code>
            </td>
        </tr></table>

### GetFifo {#GetFifo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>fifo</code></td>
            <td>
                <code>handle&lt;fifo&gt;?</code>
            </td>
        </tr></table>

### AttachVmo {#AttachVmo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>vmoid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block/'>fuchsia.hardware.block</a>/<a class='link' href='../fuchsia.hardware.block/#VmoID'>VmoID</a>?</code>
            </td>
        </tr></table>

### CloseFifo {#CloseFifo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### RebindDevice {#RebindDevice}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### GetTypeGuid {#GetTypeGuid}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>guid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block.partition/'>fuchsia.hardware.block.partition</a>/<a class='link' href='../fuchsia.hardware.block.partition/#GUID'>GUID</a>?</code>
            </td>
        </tr></table>

### GetInstanceGuid {#GetInstanceGuid}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>guid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.block.partition/'>fuchsia.hardware.block.partition</a>/<a class='link' href='../fuchsia.hardware.block.partition/#GUID'>GUID</a>?</code>
            </td>
        </tr></table>

### GetName {#GetName}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[128]?</code>
            </td>
        </tr></table>

### Query {#Query}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#VolumeInfo'>VolumeInfo</a>?</code>
            </td>
        </tr></table>

### QuerySlices {#QuerySlices}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_slices</code></td>
            <td>
                <code>vector&lt;uint64&gt;[16]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>response</code></td>
            <td>
                <code>[16]</code>
            </td>
        </tr><tr>
            <td><code>response_count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### Extend {#Extend}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_slice</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>slice_count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### Shrink {#Shrink}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_slice</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>slice_count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### Destroy {#Destroy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### VolumeInfo {#VolumeInfo}
*Defined in [fuchsia.hardware.block.volume/volume.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block-volume/volume.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>slice_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vslice_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pslice_total_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pslice_allocated_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VolumeManagerInfo {#VolumeManagerInfo}
*Defined in [fuchsia.hardware.block.volume/volume.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block-volume/volume.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>slice_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>current_slice_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>maximum_slice_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VsliceRange {#VsliceRange}
*Defined in [fuchsia.hardware.block.volume/volume.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block-volume/volume.fidl#93)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>allocated</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="AllocatePartitionFlagInactive">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block-volume/volume.fidl#46">AllocatePartitionFlagInactive</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="MAX_SLICE_REQUESTS">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block-volume/volume.fidl#87">MAX_SLICE_REQUESTS</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



