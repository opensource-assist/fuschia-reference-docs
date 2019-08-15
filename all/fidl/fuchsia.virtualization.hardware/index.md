Project: /_project.yaml
Book: /_book.yaml

# fuchsia.virtualization.hardware


## **PROTOCOLS**

## VirtioDevice {:#VirtioDevice}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#54)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

## VirtioBalloon {:#VirtioBalloon}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#69)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the balloon device.

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

### GetMemStats {:#GetMemStats}

 Get memory statistics from the balloon device.

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
                <code>vector&lt;<a class='link' href='../fuchsia.virtualization/index.html'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/index.html#MemStat'>MemStat</a>&gt;?</code>
            </td>
        </tr></table>

## VirtioBlock {:#VirtioBlock}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#81)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the block device.

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
                <code><a class='link' href='../fuchsia.virtualization/index.html'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/index.html#BlockMode'>BlockMode</a></code>
            </td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.virtualization/index.html'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/index.html#BlockFormat'>BlockFormat</a></code>
            </td>
        </tr><tr>
            <td><code>file</code></td>
            <td>
                <code><a class='link' href='../fuchsia.io/index.html'>fuchsia.io</a>/<a class='link' href='../fuchsia.io/index.html#File'>File</a></code>
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

## VirtioConsole {:#VirtioConsole}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#92)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the console device. This uses `socket` to handle input and output.

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

## ViewListener {:#ViewListener}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#101)*

 Provides a way for VirtioInput to listen to view events.

### OnSizeChanged {:#OnSizeChanged}

 Called when a View's size is changed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
        </tr></table>



### OnInputEvent {:#OnInputEvent}

 Called when a View receives input events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#InputEvent'>InputEvent</a></code>
            </td>
        </tr></table>



## VirtioGpu {:#VirtioGpu}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#110)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the GPU device.

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

### OnConfigChanged {:#OnConfigChanged}

 Called when a device's configuration is changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## VirtioInput {:#VirtioInput}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#121)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the input device.

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

## VirtioMagma {:#VirtioMagma}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#129)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the magma device.

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

## VirtioNet {:#VirtioNet}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#139)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the net device.

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

## VirtioRng {:#VirtioRng}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#147)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the RNG device.

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

## VirtioWaylandImporter {:#VirtioWaylandImporter}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#157)*


### Import {:#Import}


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

## VirtioWayland {:#VirtioWayland}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#163)*


### ConfigureQueue {:#ConfigureQueue}

 Configure a `queue` for the device. This specifies the `size` and the
 guest physical addresses of the queue: `desc`, `avail`, and `used`.

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

### NotifyQueue {:#NotifyQueue}

 Notify a `queue` for the device. Primarily used for black-box testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>queue</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Ready {:#Ready}

 Ready a device. This provides the set of `negotiated_features` that the
 driver and device have agreed upon.

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

### Start {:#Start}

 Start the wayland device.

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
                <code><a class='link' href='../fuchsia.virtualization/index.html'>fuchsia.virtualization</a>/<a class='link' href='../fuchsia.virtualization/index.html#WaylandDispatcher'>WaylandDispatcher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetImporter {:#GetImporter}


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

### Trap {:#Trap}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#24)*



 Contains the details of a device trap.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The address of the device trap. This must be page-aligned.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The size of the device trap. This must be a multiple of the page size.
</td>
            <td>No default</td>
        </tr>
</table>

### StartInfo {:#StartInfo}
*Defined in [fuchsia.virtualization.hardware/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#33)*



 Contains the basic information required to start execution of a device.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>trap</code></td>
            <td>
                <code><a class='link' href='#Trap'>Trap</a></code>
            </td>
            <td> The trap associated with a device. It is up to the device to set this
 trap during device setup.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>guest</code></td>
            <td>
                <code>handle&lt;guest&gt;?</code>
            </td>
            <td> The guest associated with a device. This handle should be used to setup
 device traps, and then be released before device operation begins.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td> The event associated with a device interrupt. This is how the device will
 notify the guest of events it should process.

 The meaning of the different signals that can be raised on the event are
 documented by the EVENT_* constants above.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td> The VMO used to represent guest physical memory.
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#17">EVENT_SET_QUEUE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#19">EVENT_SET_CONFIG</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#21">EVENT_SET_INTERRUPT</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualization.hardware/device.fidl#154">kVirtioWaylandInvalidVfdId</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

