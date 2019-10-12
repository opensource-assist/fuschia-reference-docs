Project: /_project.yaml
Book: /_book.yaml

# fuchsia.camera


## **PROTOCOLS**

## Control {:#Control}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#83)*

 These are the original interfaces, which are being used for compatibility.
 The names are preserved from the ones in camera.h for porting ease.

### GetFormats {:#GetFormats}

 Get the available format types for this device
 NOTE: The formats are paginated to `MAX_FORMATS_PER_RESPONSE`, multiple
 GetFormats need to be issued until total_format_count are received

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

### CreateStream {:#CreateStream}

 Sent by the client to indicate desired stream characteristics.
 If setting the format is successful, the stream request will be honored.
 The stream token is used to provide additional control over the interface from the
 Camera Manager.  The driver provides the guarantee that:
     1) If the stream token receives the `PEER_CLOSED` event, the driver will close
        the stream.
     2) If the Stream interface is closed, the driver will close the eventpair.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_collection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionInfo'>BufferCollectionInfo</a></code>
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



### GetDeviceInfo {:#GetDeviceInfo}


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

## Stream {:#Stream}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#104)*


### Start {:#Start}

 Starts the streaming of frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {:#Stop}

 Stops the streaming of frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ReleaseFrame {:#ReleaseFrame}

 Unlocks the specified frame, allowing the driver to reuse the memory.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnFrameAvailable {:#OnFrameAvailable}

 Sent by the driver to the client when a frame is available for processing,
 or an error occurred.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code><a class='link' href='#FrameAvailableEvent'>FrameAvailableEvent</a></code>
            </td>
        </tr></table>

## Manager {:#Manager}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#46)*

 The Camera Manager grants access to individual or sets of cameras
 1) You request the list of cameras, which gives you camera descriptions
 2) You request the list of formats available for the camera to which you
    wish to connect.
 3) You request a Stream interface using CreateStream.

### GetDevices {:#GetDevices}

 Returns a list of all the video devices that are currently plugged in
 and enumerated.  The camera_id field of the DeviceInfo is used to specify
 a device in GetFormats, GetStream and GetStreamAndBufferCollection.

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

### GetFormats {:#GetFormats}

 Get all the available formats for a camera.
 `camera_id` is obtained from a DeviceInfo returned by GetDevices.

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

### CreateStream {:#CreateStream}

 Create a Stream with the specified access rights.  This may not succeed.
 If it does succeed, the Stream will have the rights indicated.
 `buffer_info` contains a set of buffers to be used with the Stream.
 This is being deprecated - please use CreateStreamV2.

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
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionInfo'>BufferCollectionInfo</a></code>
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



### CreateStreamV2 {:#CreateStreamV2}

 Create a Stream with the specified access rights.  This may not succeed.
 If it does succeed, the Stream will have the rights indicated.
 `buffer_info` contains a set of buffers to be used with the Stream.

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
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionInfo'>BufferCollectionInfo</a></code>
            </td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.camera.common/index.html'>fuchsia.camera.common</a>/<a class='link' href='../fuchsia.camera.common/index.html#Stream'>Stream</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>client_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>



## Control {:#Control}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#83)*

 These are the original interfaces, which are being used for compatibility.
 The names are preserved from the ones in camera.h for porting ease.

### GetFormats {:#GetFormats}

 Get the available format types for this device
 NOTE: The formats are paginated to `MAX_FORMATS_PER_RESPONSE`, multiple
 GetFormats need to be issued until total_format_count are received

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

### CreateStream {:#CreateStream}

 Sent by the client to indicate desired stream characteristics.
 If setting the format is successful, the stream request will be honored.
 The stream token is used to provide additional control over the interface from the
 Camera Manager.  The driver provides the guarantee that:
     1) If the stream token receives the `PEER_CLOSED` event, the driver will close
        the stream.
     2) If the Stream interface is closed, the driver will close the eventpair.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_collection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionInfo'>BufferCollectionInfo</a></code>
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



### GetDeviceInfo {:#GetDeviceInfo}


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

## Stream {:#Stream}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#104)*


### Start {:#Start}

 Starts the streaming of frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {:#Stop}

 Stops the streaming of frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ReleaseFrame {:#ReleaseFrame}

 Unlocks the specified frame, allowing the driver to reuse the memory.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnFrameAvailable {:#OnFrameAvailable}

 Sent by the driver to the client when a frame is available for processing,
 or an error occurred.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code><a class='link' href='#FrameAvailableEvent'>FrameAvailableEvent</a></code>
            </td>
        </tr></table>

## Manager {:#Manager}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#46)*

 The Camera Manager grants access to individual or sets of cameras
 1) You request the list of cameras, which gives you camera descriptions
 2) You request the list of formats available for the camera to which you
    wish to connect.
 3) You request a Stream interface using CreateStream.

### GetDevices {:#GetDevices}

 Returns a list of all the video devices that are currently plugged in
 and enumerated.  The camera_id field of the DeviceInfo is used to specify
 a device in GetFormats, GetStream and GetStreamAndBufferCollection.

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

### GetFormats {:#GetFormats}

 Get all the available formats for a camera.
 `camera_id` is obtained from a DeviceInfo returned by GetDevices.

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

### CreateStream {:#CreateStream}

 Create a Stream with the specified access rights.  This may not succeed.
 If it does succeed, the Stream will have the rights indicated.
 `buffer_info` contains a set of buffers to be used with the Stream.
 This is being deprecated - please use CreateStreamV2.

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
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionInfo'>BufferCollectionInfo</a></code>
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



### CreateStreamV2 {:#CreateStreamV2}

 Create a Stream with the specified access rights.  This may not succeed.
 If it does succeed, the Stream will have the rights indicated.
 `buffer_info` contains a set of buffers to be used with the Stream.

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
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionInfo'>BufferCollectionInfo</a></code>
            </td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.camera.common/index.html'>fuchsia.camera.common</a>/<a class='link' href='../fuchsia.camera.common/index.html#Stream'>Stream</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>client_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### DeviceInfo {:#DeviceInfo}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#27)*



 Identifying information about the device.


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
            <td><code>serial_number</code></td>
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
            <td> The maximum number of stream interfaces that the device can support
 simultaneously.
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

### Metadata {:#Metadata}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#53)*





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

### FrameAvailableEvent {:#FrameAvailableEvent}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#59)*



 Sent by the driver to the client when a frame is available for processing,
 or an error occurred.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frame_status</code></td>
            <td>
                <code><a class='link' href='#FrameStatus'>FrameStatus</a></code>
            </td>
            <td> Non zero if an error occurred.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The index of the buffer in the buffer collection.
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

### FrameRate {:#FrameRate}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#69)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frames_per_sec_numerator</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The frame rate is frames_per_sec_numerator / frames_per_sec_denominator.
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

### VideoFormat {:#VideoFormat}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#75)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#ImageFormat'>ImageFormat</a></code>
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

### VideoStream {:#VideoStream}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#14)*



 A stream that the camera manager can provide.  Video streams reference a
 a camera, but may have additional hardware and bandwidth restrictions
 from and ISP or other processing units.
 This is being deprecated - please use VideoStreamV2 (below).


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The camera_id corresponds to the camera_id that is given in the DeviceInfo
 received from GetDevices.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#VideoFormat'>VideoFormat</a></code>
            </td>
            <td> The requested video format.  Note that this is field is necessary to
 set The frame rate, even when calling CreateStream.
 When calling CreateStream, format.format should match buffer_info.format.
</td>
            <td>No default</td>
        </tr>
</table>

### VideoStreamV2 {:#VideoStreamV2}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#30)*



 Preferred version of stream.
 A version of stream that relies on definition of VideoFormat coming out of
 fuchsia.hardware.camera. Streams reference a camera, but may have additional
 hardware and bandwidth restrictions from an ISP or other processing units.
 New code should depend on this as the other version will be deprecated when
 dependencies are removed.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The camera_id corresponds to the camera_id that is given in DeviceInfo
 received from GetDevices.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html'>fuchsia.camera.common</a>/<a class='link' href='../fuchsia.camera.common/index.html#VideoFormat'>VideoFormat</a></code>
            </td>
            <td> The requested video format. Note that this field is necessary to set the
 frame rate, even when calling CreateStream. When calling CreateStream
 format.format should match buffer_info.format.
</td>
            <td>No default</td>
        </tr>
</table>

### DeviceInfo {:#DeviceInfo}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#27)*



 Identifying information about the device.


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
            <td><code>serial_number</code></td>
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
            <td> The maximum number of stream interfaces that the device can support
 simultaneously.
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

### Metadata {:#Metadata}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#53)*





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

### FrameAvailableEvent {:#FrameAvailableEvent}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#59)*



 Sent by the driver to the client when a frame is available for processing,
 or an error occurred.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frame_status</code></td>
            <td>
                <code><a class='link' href='#FrameStatus'>FrameStatus</a></code>
            </td>
            <td> Non zero if an error occurred.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The index of the buffer in the buffer collection.
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

### FrameRate {:#FrameRate}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#69)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frames_per_sec_numerator</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The frame rate is frames_per_sec_numerator / frames_per_sec_denominator.
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

### VideoFormat {:#VideoFormat}
*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#75)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#ImageFormat'>ImageFormat</a></code>
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

### VideoStream {:#VideoStream}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#14)*



 A stream that the camera manager can provide.  Video streams reference a
 a camera, but may have additional hardware and bandwidth restrictions
 from and ISP or other processing units.
 This is being deprecated - please use VideoStreamV2 (below).


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The camera_id corresponds to the camera_id that is given in the DeviceInfo
 received from GetDevices.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#VideoFormat'>VideoFormat</a></code>
            </td>
            <td> The requested video format.  Note that this is field is necessary to
 set The frame rate, even when calling CreateStream.
 When calling CreateStream, format.format should match buffer_info.format.
</td>
            <td>No default</td>
        </tr>
</table>

### VideoStreamV2 {:#VideoStreamV2}
*Defined in [fuchsia.camera/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/manager.fidl#30)*



 Preferred version of stream.
 A version of stream that relies on definition of VideoFormat coming out of
 fuchsia.hardware.camera. Streams reference a camera, but may have additional
 hardware and bandwidth restrictions from an ISP or other processing units.
 New code should depend on this as the other version will be deprecated when
 dependencies are removed.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The camera_id corresponds to the camera_id that is given in DeviceInfo
 received from GetDevices.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html'>fuchsia.camera.common</a>/<a class='link' href='../fuchsia.camera.common/index.html#VideoFormat'>VideoFormat</a></code>
            </td>
            <td> The requested video format. Note that this field is necessary to set the
 frame rate, even when calling CreateStream. When calling CreateStream
 format.format should match buffer_info.format.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### FrameStatus {:#FrameStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#42)*

 Status to be set when a frame is signalled available.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR_FRAME</code></td>
            <td><code>1</code></td>
            <td> An error occurred during the production of a frame.
 No data will be available in the data buffer corresponding to this
 notification.
</td>
        </tr><tr>
            <td><code>ERROR_BUFFER_FULL</code></td>
            <td><code>2</code></td>
            <td> No space was available in the data buffer, resulting in a dropped frame.
</td>
        </tr></table>

### FrameStatus {:#FrameStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera/camera.fidl#42)*

 Status to be set when a frame is signalled available.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR_FRAME</code></td>
            <td><code>1</code></td>
            <td> An error occurred during the production of a frame.
 No data will be available in the data buffer corresponding to this
 notification.
</td>
        </tr><tr>
            <td><code>ERROR_BUFFER_FULL</code></td>
            <td><code>2</code></td>
            <td> No space was available in the data buffer, resulting in a dropped frame.
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
            <td> A coarse set of capabilities.  This struct is used in the camera description
 to help filter out cameras which will not have the needed capabilities.
 This set of declarations would be the bitfield: CameraOutputCapabilities.
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
    <tr>
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
            <td> A coarse set of capabilities.  This struct is used in the camera description
 to help filter out cameras which will not have the needed capabilities.
 This set of declarations would be the bitfield: CameraOutputCapabilities.
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

