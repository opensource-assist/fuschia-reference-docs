Project: /_project.yaml
Book: /_book.yaml

# fuchsia.camera2


## **PROTOCOLS**

## Manager {:#Manager}
*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#11)*


### OnDeviceAvailable {:#OnDeviceAvailable}

 Notifies the client when a camera becomes available.  A number of these events will
 be sent when a client first connects to this protocol.
 |device_id| is used to identify the camera.  The device_id should not change throughout
 the lifetime of the camera.
 |last_known_camera| is set to true when the Camera Manager has notified the client
 of all the devices it currently knows about.
 |description| describes the properties of the camera.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code><a class='link' href='#DeviceInfo'>DeviceInfo</a></code>
            </td>
        </tr><tr>
            <td><code>last_known_camera</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### OnDeviceUnavailable {:#OnDeviceUnavailable}

 Notifies the client when a camera becomes unavailable.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### OnDeviceMuteChanged {:#OnDeviceMuteChanged}

 Notifies the client when a camera becomes muted or unmuted.
 |device_id| refers to the device_id from the description of a previous OnDeviceAvailable
 call.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>currently_muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### AcknowledgeDeviceEvent {:#AcknowledgeDeviceEvent}

 AcknowledgeDeviceEvent must be called after any of the above events before more
 events will be sent.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ConnectToStream {:#ConnectToStream}

 Connect to a camera stream:
 |device_id| Refers to a specific device_id that has been advertised by OnDeviceAvailable.
 |constraints| contains a set of constraints on the requested stream.  The Camera
 Manager will attempt to find a stream that meets the constraints.  If multiple
 streams match, one of the matching streams will be connected.
 |token| refers to a Sysmem buffer allocation that will be used to pass images using
 the Stream protocol.  The Camera Manager will apply a BufferCollectionContraints
 related to the image format(s), so the client does not need to apply any
 ImageFormatConstraints.
 Sync is assumed to have been called on |token| before it is passed to
 ConnectToStream.
 Since |constraints| may not dictate a specific format, the initial format of images
 on the stream is indicated on the response.
 The connection is considered to be successful once a response has been given, unless
 |stream| is closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>constraints</code></td>
            <td>
                <code><a class='link' href='#StreamConstraints'>StreamConstraints</a></code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionToken'>BufferCollectionToken</a></code>
            </td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Stream'>Stream</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#ImageFormat_2'>ImageFormat_2</a></code>
            </td>
        </tr></table>

## MuteControl {:#MuteControl}
*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#54)*


### Mute {:#Mute}

 Mutes a camera.  This is independent from stopping or closing a stream.  A muted
 camera will not produce any more images until
 unmute is called.  You can still connect to streams from a muted camera, but they
 will not produce frames until the camera is unmuted.
 |device_id| refers to the device_id from a previous OnDeviceAvailable call.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>int32</code>
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

### Unmute {:#Unmute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>int32</code>
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

## Stream {:#Stream}
*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#72)*


### Start {:#Start}

 Control Operations
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
 or an error occurred.  The frame is considered read-locked by the client
 after this message.  The client must call ReleaseFrame to release the
 read-lock for a non-error frame, or the consumer will eventually run out of buffers.
 If a frame has an error, the client must call AcknowledgeFrameError before
 another OnFrameAvailable will be called with an error frame.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code><a class='link' href='#FrameAvailableInfo'>FrameAvailableInfo</a></code>
            </td>
        </tr></table>

### AcknowledgeFrameError {:#AcknowledgeFrameError}

 Provides flow control for receiving frame errors. See OnFrameAvailable comment.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetRegionOfInterest {:#SetRegionOfInterest}

 Data operations
 This is used by clients to provide inputs for region of interest
 selection.
 Inputs are the x & y coordinates for the new bounding box.
 For streams which do not support smart framing, this would
 return an error.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x_min</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>y_min</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>x_max</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>y_max</code></td>
            <td>
                <code>float32</code>
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

### SetImageFormat {:#SetImageFormat}

 Change the image format of the stream. This is called when clients want
 to dynamically change the resolution of the stream while the streaming is
 is going on.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_format_index</code></td>
            <td>
                <code>uint32</code>
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

### GetImageFormats {:#GetImageFormats}

 Get the image formats that this stream supports.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>image_formats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#ImageFormat_2'>ImageFormat_2</a>&gt;[256]</code>
            </td>
        </tr></table>



## **STRUCTS**

### FrameAvailableInfo {:#FrameAvailableInfo}
*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#34)*



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
                <code><a class='link' href='#FrameMetadata'>FrameMetadata</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FrameRate {:#FrameRate}
*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#44)*





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



## **ENUMS**

### DeviceType {:#DeviceType}
Type: <code>uint32</code>

*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#72)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BUILTIN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>VIRTUAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### FrameStatus {:#FrameStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#14)*

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



## **TABLES**

### StreamConstraints {:#StreamConstraints}


*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#66)*

 These constraints are given to the Camera Manager when requesting a stream.  The
 Camera Manager will use these constraints to match an appropriate stream.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#StreamProperties'>StreamProperties</a></code>
            </td>
            <td> A table that describes the properties of the stream. Any properties specified will
 be considered requirements for matching streams.
</td>
        </tr></table>

### DeviceInfo {:#DeviceInfo}


*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#78)*

 Identifying information about the device.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>vendor_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> Information from physical device enumeration:
</td>
        </tr><tr>
            <td>2</td>
            <td><code>vendor_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>product_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>product_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>serial_number</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#DeviceType'>DeviceType</a></code>
            </td>
            <td> Information about the type of device:
</td>
        </tr></table>

### FrameMetadata {:#FrameMetadata}


*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#25)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>image_format_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> |image_format_index| references the index into the vector of available
 formats supported by the stream.
</td>
        </tr></table>

### StreamProperties {:#StreamProperties}


*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#67)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream_type</code></td>
            <td>
                <code><a class='link' href='#CameraStreamType'>CameraStreamType</a></code>
            </td>
            <td> These could be one or more of the above mentioned Stream Types
</td>
        </tr></table>







## **BITS**

### CameraStreamType {:#CameraStreamType}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>MACHINE_LEARNING</td>
            <td>1</td>
            <td> ML request FR(Full Resolution) stream as well as
 a DS(Down Scaled Resolution) stream for Security Use Case
 which are of fixed resolutions
</td>
        </tr><tr>
            <td>MONITORING</td>
            <td>2</td>
            <td> This is Security Video Stream which could support multiple
 resolutions at runtime.
</td>
        </tr><tr>
            <td>FULL_RESOLUTION</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>DOWNSCALED_RESOLUTION</td>
            <td>8</td>
            <td> ML request a DS stream for Video Conferencing which is fixed resolution
</td>
        </tr><tr>
            <td>VIDEO_CONFERENCE</td>
            <td>16</td>
            <td> This is Video Conferencing Stream which could support
 multiple resolutions at runtime.
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#11">MAX_IMAGE_FORMATS</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maximum number of image formats per stream.
</td>
        </tr>
    
</table>

