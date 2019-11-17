[TOC]

# fuchsia.virtualization.hardware


## **PROTOCOLS**

## VirtioDevice {#VirtioDevice}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#55)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## VirtioBalloon {#VirtioBalloon}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#70)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the balloon device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetMemStats {#GetMemStats}

<p>Get memory statistics from the balloon device.</p>

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
            <td><code>mem_stats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.virtualization/'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/#MemStat'>MemStat</a>&gt;?</code>
            </td>
        </tr></table>

## VirtioBlock {#VirtioBlock}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#82)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the block device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string[20]</code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='../fuchsia.virtualization/'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/#BlockMode'>BlockMode</a></code>
            </td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.virtualization/'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/#BlockFormat'>BlockFormat</a></code>
            </td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/#File'>File</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

## VirtioConsole {#VirtioConsole}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#93)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the console device. This uses <code>socket</code> to handle input and output.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## ViewListener {#ViewListener}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#102)*

<p>Provides a way for VirtioInput to listen to view events.</p>

### OnSizeChanged {#OnSizeChanged}

<p>Called when a View's size is changed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#vec3'>vec3</a></code>
            </td>
        </tr></table>



### OnInputEvent {#OnInputEvent}

<p>Called when a View receives input events.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#InputEvent'>InputEvent</a></code>
            </td>
        </tr></table>



## VirtioGpu {#VirtioGpu}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#111)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the GPU device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr><tr>
            <td><code>view_listener</code></td>
            <td>
                <code><a class='link' href='#ViewListener'>ViewListener</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnConfigChanged {#OnConfigChanged}

<p>Called when a device's configuration is changed.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## VirtioInput {#VirtioInput}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#122)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the input device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## VirtioMagma {#VirtioMagma}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#130)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the magma device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr><tr>
            <td><code>vmar</code></td>
            <td>
                <code>handle&lt;vmar&gt;</code>
            </td>
        </tr><tr>
            <td><code>wayland_importer</code></td>
            <td>
                <code><a class='link' href='#VirtioWaylandImporter'>VirtioWaylandImporter</a>?</code>
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
        </tr></table>

## VirtioNet {#VirtioNet}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#140)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the net device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr><tr>
            <td><code>mac_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/#MacAddress'>MacAddress</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## VirtioRng {#VirtioRng}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#148)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the RNG device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## VirtioWaylandImporter {#VirtioWaylandImporter}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#158)*


### Import {#Import}


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
            <td><code>vfd_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

## VirtioWayland {#VirtioWayland}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#164)*


### ConfigureQueue {#ConfigureQueue}

<p>Configure a <code>queue</code> for the device. This specifies the <code>size</code> and the
guest physical addresses of the queue: <code>desc</code>, <code>avail</code>, and <code>used</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>desc</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>avail</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>used</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### NotifyQueue {#NotifyQueue}

<p>Notify a <code>queue</code> for the device. Primarily used for black-box testing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {#Ready}

<p>Ready a device. This provides the set of <code>negotiated_features</code> that the
driver and device have agreed upon.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>negotiated_features</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Start {#Start}

<p>Start the wayland device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_info</code></td>
            <td>
                <code><a class='link' href='#StartInfo'>StartInfo</a></code>
            </td>
        </tr><tr>
            <td><code>vmar</code></td>
            <td>
                <code>handle&lt;vmar&gt;</code>
            </td>
        </tr><tr>
            <td><code>dispatcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.virtualization/'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/#WaylandDispatcher'>WaylandDispatcher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetImporter {#GetImporter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>importer</code></td>
            <td>
                <code>request&lt;<a class='link' href='#VirtioWaylandImporter'>VirtioWaylandImporter</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### Trap {#Trap}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#25)*



<p>Contains the details of a device trap.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The address of the device trap. This must be page-aligned.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The size of the device trap. This must be a multiple of the page size.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### StartInfo {#StartInfo}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#34)*



<p>Contains the basic information required to start execution of a device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>trap</code></td>
            <td>
                <code><a class='link' href='#Trap'>Trap</a></code>
            </td>
            <td><p>The trap associated with a device. It is up to the device to set this
trap during device setup.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>guest</code></td>
            <td>
                <code>handle&lt;guest&gt;?</code>
            </td>
            <td><p>The guest associated with a device. This handle should be used to setup
device traps, and then be released before device operation begins.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td><p>The event associated with a device interrupt. This is how the device will
notify the guest of events it should process.</p>
<p>The meaning of the different signals that can be raised on the event are
documented by the EVENT_* constants above.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td><p>The VMO used to represent guest physical memory.</p>
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#18">EVENT_SET_QUEUE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Set a flag to inspect queues on the next interrupt.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#20">EVENT_SET_CONFIG</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Set a flag to inspect configs on the next interrupt.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#22">EVENT_SET_INTERRUPT</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>If a flag is set, send an interrupt to the device.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#155">kVirtioWaylandInvalidVfdId</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

