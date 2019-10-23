[TOC]

# fuchsia.hardware.block


## **PROTOCOLS**

## Block {#Block}
*Defined in [fuchsia.hardware.block/block.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#80)*


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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#BlockInfo'>BlockInfo</a>?</code>
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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='#BlockStats'>BlockStats</a>?</code>
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
                <code>int32</code>
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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>vmoid</code></td>
            <td>
                <code><a class='link' href='#VmoID'>VmoID</a>?</code>
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
                <code>int32</code>
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
                <code>int32</code>
            </td>
        </tr></table>

## Ftl {#Ftl}
*Defined in [fuchsia.hardware.block/ftl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/ftl.fidl#10)*


### Format {#Format}


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
                <code>int32</code>
            </td>
        </tr></table>



## **STRUCTS**

### BlockInfo {#BlockInfo}
*Defined in [fuchsia.hardware.block/block.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#26)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>block_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>block_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_transfer_size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>reserved</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BlockStats {#BlockStats}
*Defined in [fuchsia.hardware.block/block.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#46)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>read</code></td>
            <td>
                <code><a class='link' href='../fuchsia.storage.metrics/'>fuchsia.storage.metrics</a>/<a class='link' href='../fuchsia.storage.metrics/#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>write</code></td>
            <td>
                <code><a class='link' href='../fuchsia.storage.metrics/'>fuchsia.storage.metrics</a>/<a class='link' href='../fuchsia.storage.metrics/#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>trim</code></td>
            <td>
                <code><a class='link' href='../fuchsia.storage.metrics/'>fuchsia.storage.metrics</a>/<a class='link' href='../fuchsia.storage.metrics/#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flush</code></td>
            <td>
                <code><a class='link' href='../fuchsia.storage.metrics/'>fuchsia.storage.metrics</a>/<a class='link' href='../fuchsia.storage.metrics/#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>barrier_before</code></td>
            <td>
                <code><a class='link' href='../fuchsia.storage.metrics/'>fuchsia.storage.metrics</a>/<a class='link' href='../fuchsia.storage.metrics/#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>barrier_after</code></td>
            <td>
                <code><a class='link' href='../fuchsia.storage.metrics/'>fuchsia.storage.metrics</a>/<a class='link' href='../fuchsia.storage.metrics/#CallStat'>CallStat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VmoID {#VmoID}
*Defined in [fuchsia.hardware.block/block.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#69)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#10">FLAG_READONLY</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#13">FLAG_REMOVABLE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#16">FLAG_BOOTPART</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#19">FLAG_TRIM_SUPPORT</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#23">MAX_TRANSFER_UNBOUNDED</a></td>
            <td>
                    <code>4294967295</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-block/block.fidl#75">VMOID_INVALID</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>

