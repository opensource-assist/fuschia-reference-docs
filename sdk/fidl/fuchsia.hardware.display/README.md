[TOC]

# fuchsia.hardware.display


## **PROTOCOLS**

## Provider {#Provider}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#179)*

<p>Provider for display controllers.</p>
<p>The driver supports two simultaneous clients - a primary client and a virtcon
client.</p>

### OpenVirtconController {#OpenVirtconController}

<p>Open a virtcon client. <code>device</code> should be a handle to one endpoint of a
channel that (on success) will become an open connection to a new
instance of a display client device. A protocol request <code>controller</code>
provides an interface to the Controller for the new device. Closing the
connection to <code>device</code> will also close the <code>controller</code> interface. If
the display device already has a virtcon controller then this method
will return <code>ZX_ERR_ALREADY_BOUND</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Controller'>Controller</a>&gt;</code>
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
        </tr></table>

### OpenController {#OpenController}

<p>Open a primary client. <code>device</code> should be a handle to one endpoint of a
channel that (on success) will become an open connection to a new
instance of a display client device. A protocol request <code>controller</code>
provides an interface to the Controller for the new device. Closing the
connection to <code>device</code> will also close the <code>controller</code> interface. If
the display device already has a primary controller then this method
will return <code>ZX_ERR_ALREADY_BOUND</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Controller'>Controller</a>&gt;</code>
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
        </tr></table>

## Controller {#Controller}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#217)*

<p>Interface for accessing the display hardware.</p>
<p>A display configuration can be separated into two parts: the layer layout and
the layer contents. The layout includes all parts of a configuration other
than the image handles. The active configuration is composed of the most
recently applied layout and an active image from each layer - see
SetLayerImage for details on how the active image is defined. Note the
requirement that each layer has an active image. Whenever a new active
configuration is available, it is immediately given to the hardware. This
allows the layout and each layer's contents to advance independently when
possible.</p>
<p>Performing illegal actions on the interface will result in the interface
being closed.</p>

### DisplaysChanged {#DisplaysChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>added</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Info'>Info</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>removed</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
        </tr></table>

### ImportVmoImage {#ImportVmoImage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_config</code></td>
            <td>
                <code><a class='link' href='#ImageConfig'>ImageConfig</a></code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### ImportImage {#ImportImage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_config</code></td>
            <td>
                <code><a class='link' href='#ImageConfig'>ImageConfig</a></code>
            </td>
        </tr><tr>
            <td><code>collection_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### ReleaseImage {#ReleaseImage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### ImportEvent {#ImportEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### ReleaseEvent {#ReleaseEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CreateLayer {#CreateLayer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### DestroyLayer {#DestroyLayer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### SetDisplayMode {#SetDisplayMode}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>display_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#Mode'>Mode</a></code>
            </td>
        </tr></table>



### SetDisplayColorConversion {#SetDisplayColorConversion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>display_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>preoffsets</code></td>
            <td>
                <code>float32[3]</code>
            </td>
        </tr><tr>
            <td><code>coefficients</code></td>
            <td>
                <code>float32[9]</code>
            </td>
        </tr><tr>
            <td><code>postoffsets</code></td>
            <td>
                <code>float32[3]</code>
            </td>
        </tr></table>



### SetDisplayLayers {#SetDisplayLayers}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>display_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>layer_ids</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
        </tr></table>



### SetLayerPrimaryConfig {#SetLayerPrimaryConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>image_config</code></td>
            <td>
                <code><a class='link' href='#ImageConfig'>ImageConfig</a></code>
            </td>
        </tr></table>



### SetLayerPrimaryPosition {#SetLayerPrimaryPosition}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='#Transform'>Transform</a></code>
            </td>
        </tr><tr>
            <td><code>src_frame</code></td>
            <td>
                <code><a class='link' href='#Frame'>Frame</a></code>
            </td>
        </tr><tr>
            <td><code>dest_frame</code></td>
            <td>
                <code><a class='link' href='#Frame'>Frame</a></code>
            </td>
        </tr></table>



### SetLayerPrimaryAlpha {#SetLayerPrimaryAlpha}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#AlphaMode'>AlphaMode</a></code>
            </td>
        </tr><tr>
            <td><code>val</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetLayerCursorConfig {#SetLayerCursorConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>image_config</code></td>
            <td>
                <code><a class='link' href='#ImageConfig'>ImageConfig</a></code>
            </td>
        </tr></table>



### SetLayerCursorPosition {#SetLayerCursorPosition}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### SetLayerColorConfig {#SetLayerColorConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>color_bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### SetLayerImage {#SetLayerImage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>wait_event_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>signal_event_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CheckConfig {#CheckConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>discard</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code><a class='link' href='#ConfigResult'>ConfigResult</a></code>
            </td>
        </tr><tr>
            <td><code>ops</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ClientCompositionOp'>ClientCompositionOp</a>&gt;</code>
            </td>
        </tr></table>

### ApplyConfig {#ApplyConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### EnableVsync {#EnableVsync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enable</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### Vsync {#Vsync}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>display_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>images</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
        </tr></table>

### SetVirtconMode {#SetVirtconMode}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mode</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>



### ClientOwnershipChange {#ClientOwnershipChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>has_ownership</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### ComputeLinearImageStride {#ComputeLinearImageStride}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stride</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### AllocateVmo {#AllocateVmo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### ImportBufferCollection {#ImportBufferCollection}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>collection_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>collection_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#BufferCollectionToken'>BufferCollectionToken</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### ReleaseBufferCollection {#ReleaseBufferCollection}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>collection_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### SetBufferCollectionConstraints {#SetBufferCollectionConstraints}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>collection_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#ImageConfig'>ImageConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetSingleBufferFramebuffer {#GetSingleBufferFramebuffer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr><tr>
            <td><code>stride</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### ImportImageForCapture {#ImportImageForCapture}

<p>Imports a buffer collection backed VMO into the display controller. The VMO
will be used by display controller to capture the image being displayed.
Returns ZX_OK along with an image_id.
image_id must be used by the client to start capture and/or release
resources allocated for capture.
Returns ZX_ERR_NOT_SUPPORTED if controller does not support capture</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_config</code></td>
            <td>
                <code><a class='link' href='#ImageConfig'>ImageConfig</a></code>
            </td>
        </tr><tr>
            <td><code>collection_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_ImportImageForCapture_Result'>Controller_ImportImageForCapture_Result</a></code>
            </td>
        </tr></table>

### StartCapture {#StartCapture}

<p>Starts capture. Client must provide a valid signal_event_id and
image_id. signal_event_id must have been imported into the driver
using ImportEvent FIDL API. Image_id is the id from ImportImageForCapture.
The client will get notified once capture is complete via signal_event_id.
Returns ZX_ERR_NOT_SUPPORTED if controller does not support capture</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>signal_event_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>image_id</code></td>
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
                <code><a class='link' href='#Controller_StartCapture_Result'>Controller_StartCapture_Result</a></code>
            </td>
        </tr></table>

### ReleaseCapture {#ReleaseCapture}

<p>Releases resources allocated for capture.
Returns ZX_ERR_NOT_SUPPORTED if controller does not support capture</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_id</code></td>
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
                <code><a class='link' href='#Controller_ReleaseCapture_Result'>Controller_ReleaseCapture_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Controller_ImportImageForCapture_Response {#Controller_ImportImageForCapture_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_StartCapture_Response {#Controller_StartCapture_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_ReleaseCapture_Response {#Controller_ReleaseCapture_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Mode {#Mode}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#20)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>horizontal_resolution</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vertical_resolution</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>refresh_rate_e2</code></td>
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
        </tr>
</table>

### CursorInfo {#CursorInfo}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Info {#Info}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>modes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Mode'>Mode</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cursor_configs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CursorInfo'>CursorInfo</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer_name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>monitor_name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>monitor_serial</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImagePlane {#ImagePlane}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#71)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>byte_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bytes_per_row</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImageConfig {#ImageConfig}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#78)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td><a class='link' href='#typeSimple'>typeSimple</a></td>
        </tr><tr>
            <td><code>planes</code></td>
            <td>
                <code>[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Frame {#Frame}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#117)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x_pos</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y_pos</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ClientCompositionOp {#ClientCompositionOp}
*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#168)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>display_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>opcode</code></td>
            <td>
                <code><a class='link' href='#ClientCompositionOpcode'>ClientCompositionOpcode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### VirtconMode {#VirtconMode}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#13)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INACTIVE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>FALLBACK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>FORCED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Transform {#Transform}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#97)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>IDENTITY</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFLECT_X</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFLECT_Y</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROT_90</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROT_180</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROT_270</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROT_90_REFLECT_X</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROT_90_REFLECT_Y</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### AlphaMode {#AlphaMode}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#108)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DISABLE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PREMULTIPLIED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>HW_MULTIPLY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ClientCompositionOpcode {#ClientCompositionOpcode}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#126)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CLIENT_USE_PRIMARY</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLIENT_MERGE_BASE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLIENT_MERGE_SRC</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLIENT_FRAME_SCALE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLIENT_SRC_FRAME</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLIENT_TRANSFORM</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLIENT_COLOR_CONVERSION</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLIENT_ALPHA</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### ConfigResult {#ConfigResult}
Type: <code>uint32</code>

*Defined in [fuchsia.hardware.display/display-controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#154)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_CONFIG</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED_CONFIG</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>TOO_MANY_DISPLAYS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED_DISPLAY_MODES</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Controller_ImportImageForCapture_Result {#Controller_ImportImageForCapture_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_ImportImageForCapture_Response'>Controller_ImportImageForCapture_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_StartCapture_Result {#Controller_StartCapture_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_StartCapture_Response'>Controller_StartCapture_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_ReleaseCapture_Result {#Controller_ReleaseCapture_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_ReleaseCapture_Response'>Controller_ReleaseCapture_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#11">invalidId</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#34">modeInterlaced</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#45">identifierMaxLen</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-display/display-controller.fidl#94">typeSimple</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

