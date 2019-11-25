[TOC]

# fuchsia.camera


## **PROTOCOLS**

## Control {#Control}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#82)*

<p>These are the original interfaces, which are being used for compatibility.
The names are preserved from the ones in camera.h for porting ease.</p>

### GetFormats {#GetFormats}

<p>Get the available format types for this device
NOTE: The formats are paginated to <code>MAX_FORMATS_PER_RESPONSE</code>, multiple
GetFormats need to be issued until total_format_count are received</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>formats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#VideoFormat'>VideoFormat</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>total_format_count</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### CreateStream {#CreateStream}

<p>Sent by the client to indicate desired stream characteristics.
If setting the format is successful, the stream request will be honored.
The stream token is used to provide additional control over the interface from the
Camera Manager.  The driver provides the guarantee that:
1) If the stream token receives the <code>PEER_CLOSED</code> event, the driver will close
the stream.
2) If the Stream interface is closed, the driver will close the eventpair.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_collection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#BufferCollectionInfo'>BufferCollectionInfo</a></code>
            </td>
        </tr><tr>
            <td><code>rate</code></td>
            <td>
                <code><a class='link' href='#FrameRate'>FrameRate</a></code>
            </td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Stream'>Stream</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>stream_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>



### GetDeviceInfo {#GetDeviceInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_info</code></td>
            <td>
                <code><a class='link' href='#DeviceInfo'>DeviceInfo</a></code>
            </td>
        </tr></table>

## Stream {#Stream}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#103)*


### Start {#Start}

<p>Starts the streaming of frames.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Stops the streaming of frames.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ReleaseFrame {#ReleaseFrame}

<p>Unlocks the specified frame, allowing the driver to reuse the memory.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnFrameAvailable {#OnFrameAvailable}

<p>Sent by the driver to the client when a frame is available for processing,
or an error occurred.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code><a class='link' href='#FrameAvailableEvent'>FrameAvailableEvent</a></code>
            </td>
        </tr></table>

## Manager {#Manager}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#45)*

<p>The Camera Manager grants access to individual or sets of cameras</p>
<ol>
<li>You request the list of cameras, which gives you camera descriptions</li>
<li>You request the list of formats available for the camera to which you
wish to connect.</li>
<li>You request a Stream interface using CreateStream.</li>
</ol>

### GetDevices {#GetDevices}

<p>Returns a list of all the video devices that are currently plugged in
and enumerated.  The camera_id field of the DeviceInfo is used to specify
a device in GetFormats, GetStream and GetStreamAndBufferCollection.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DeviceInfo'>DeviceInfo</a>&gt;</code>
            </td>
        </tr></table>

### GetFormats {#GetFormats}

<p>Get all the available formats for a camera.
<code>camera_id</code> is obtained from a DeviceInfo returned by GetDevices.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>camera_id</code></td>
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
            <td><code>formats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#VideoFormat'>VideoFormat</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>total_format_count</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### CreateStream {#CreateStream}

<p>Create a Stream with the specified access rights.  This may not succeed.
If it does succeed, the Stream will have the rights indicated.
<code>buffer_info</code> contains a set of buffers to be used with the Stream.
This is being deprecated - please use CreateStreamV2.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#VideoStream'>VideoStream</a></code>
            </td>
        </tr><tr>
            <td><code>buffer_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#BufferCollectionInfo'>BufferCollectionInfo</a></code>
            </td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Stream'>Stream</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>client_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>



### CreateStreamV2 {#CreateStreamV2}

<p>Create a Stream with the specified access rights.  This may not succeed.
If it does succeed, the Stream will have the rights indicated.
<code>buffer_info</code> contains a set of buffers to be used with the Stream.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#VideoStreamV2'>VideoStreamV2</a></code>
            </td>
        </tr><tr>
            <td><code>buffer_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#BufferCollectionInfo'>BufferCollectionInfo</a></code>
            </td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Stream'>Stream</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>client_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### DeviceInfo {#DeviceInfo}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#27)*



<p>Identifying information about the device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vendor_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vendor_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>product_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>product_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_stream_count</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The maximum number of stream interfaces that the device can support
simultaneously.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>output_capabilities</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Metadata {#Metadata}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#52)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FrameAvailableEvent {#FrameAvailableEvent}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#58)*



<p>Sent by the driver to the client when a frame is available for processing,
or an error occurred.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frame_status</code></td>
            <td>
                <code><a class='link' href='#FrameStatus'>FrameStatus</a></code>
            </td>
            <td><p>Non zero if an error occurred.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The index of the buffer in the buffer collection.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code><a class='link' href='#Metadata'>Metadata</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FrameRate {#FrameRate}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#68)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frames_per_sec_numerator</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The frame rate is frames_per_sec_numerator / frames_per_sec_denominator.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>frames_per_sec_denominator</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VideoFormat {#VideoFormat}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#74)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#ImageFormat'>ImageFormat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rate</code></td>
            <td>
                <code><a class='link' href='#FrameRate'>FrameRate</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VideoStream {#VideoStream}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#13)*



<p>A stream that the camera manager can provide.  Video streams reference a
a camera, but may have additional hardware and bandwidth restrictions
from and ISP or other processing units.
This is being deprecated - please use VideoStreamV2 (below).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The camera_id corresponds to the camera_id that is given in the DeviceInfo
received from GetDevices.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#VideoFormat'>VideoFormat</a></code>
            </td>
            <td><p>The requested video format.  Note that this is field is necessary to
set The frame rate, even when calling CreateStream.
When calling CreateStream, format.format should match buffer_info.format.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### VideoStreamV2 {#VideoStreamV2}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#29)*



<p>Preferred version of stream.
A version of stream that relies on definition of VideoFormat coming out of
fuchsia.hardware.camera. Streams reference a camera, but may have additional
hardware and bandwidth restrictions from an ISP or other processing units.
New code should depend on this as the other version will be deprecated when
dependencies are removed.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The camera_id corresponds to the camera_id that is given in DeviceInfo
received from GetDevices.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#VideoFormat'>VideoFormat</a></code>
            </td>
            <td><p>The requested video format. Note that this field is necessary to set the
frame rate, even when calling CreateStream. When calling CreateStream
format.format should match buffer_info.format.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### FrameStatus {#FrameStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#41)*

<p>Status to be set when a frame is signalled available.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR_FRAME</code></td>
            <td><code>1</code></td>
            <td><p>An error occurred during the production of a frame.
No data will be available in the data buffer corresponding to this
notification.</p>
</td>
        </tr><tr>
            <td><code>ERROR_BUFFER_FULL</code></td>
            <td><code>2</code></td>
            <td><p>No space was available in the data buffer, resulting in a dropped frame.</p>
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#13">MAX_FORMATS_PER_RESPONSE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#18">CAMERA_OUTPUT_UNKNOWN</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>A coarse set of capabilities.  This struct is used in the camera description
to help filter out cameras which will not have the needed capabilities.
This set of declarations would be the bitfield: CameraOutputCapabilities.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#19">CAMERA_OUTPUT_STILL_IMAGE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#20">CAMERA_OUTPUT_BURST</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#21">CAMERA_OUTPUT_STREAM</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#22">CAMERA_OUTPUT_HDR</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#23">CAMERA_OUTPUT_DEPTH</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#24">CAMERA_OUTPUT_STEREO</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

