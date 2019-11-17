[TOC]

# fuchsia.camera2


## **PROTOCOLS**

## Manager {#Manager}
*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#11)*


### OnDeviceAvailable {#OnDeviceAvailable}

<p>Notifies the client when a camera becomes available.  A number of these events will
be sent when a client first connects to this protocol.
|device_id| is used to identify the camera.  The device_id should not change throughout
the lifetime of the camera.
|last_known_camera| is set to true when the Camera Manager has notified the client
of all the devices it currently knows about.
|description| describes the properties of the camera.</p>



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

### OnDeviceUnavailable {#OnDeviceUnavailable}

<p>Notifies the client when a camera becomes unavailable.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### OnDeviceMuteChanged {#OnDeviceMuteChanged}

<p>Notifies the client when a camera becomes muted or unmuted.
|device_id| refers to the device_id from the description of a previous OnDeviceAvailable
call.</p>



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

### AcknowledgeDeviceEvent {#AcknowledgeDeviceEvent}

<p>AcknowledgeDeviceEvent must be called after any of the above events before more
events will be sent.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ConnectToStream {#ConnectToStream}

<p>Connect to a camera stream:
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
|stream| is closed.</p>

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
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#BufferCollectionToken'>BufferCollectionToken</a></code>
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
                <code><a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#ImageFormat_2'>ImageFormat_2</a></code>
            </td>
        </tr></table>

## MuteControl {#MuteControl}
*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#54)*


### Mute {#Mute}

<p>Mutes a camera.  This is independent from stopping or closing a stream.  A muted
camera will not produce any more images until
unmute is called.  You can still connect to streams from a muted camera, but they
will not produce frames until the camera is unmuted.
|device_id| refers to the device_id from a previous OnDeviceAvailable call.</p>

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

### Unmute {#Unmute}


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

## Stream {#Stream}
*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#72)*


### Start {#Start}

<p>Control Operations
Starts the streaming of frames.</p>

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
or an error occurred.  The frame is considered read-locked by the client
after this message.  The client must call ReleaseFrame to release the
read-lock for a non-error frame, or the consumer will eventually run out of buffers.
If a frame has an error, the client must call AcknowledgeFrameError before
another OnFrameAvailable will be called with an error frame.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frame</code></td>
            <td>
                <code><a class='link' href='#FrameAvailableInfo'>FrameAvailableInfo</a></code>
            </td>
        </tr></table>

### AcknowledgeFrameError {#AcknowledgeFrameError}

<p>Provides flow control for receiving frame errors. See OnFrameAvailable comment.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetRegionOfInterest {#SetRegionOfInterest}

<p>Data operations
This is used by clients to provide inputs for region of interest
selection.
Inputs are the x &amp; y coordinates for the new bounding box.
For streams which do not support smart framing, this would
return an error.</p>

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

### SetImageFormat {#SetImageFormat}

<p>Change the image format of the stream. This is called when clients want
to dynamically change the resolution of the stream while the streaming is
is going on.</p>

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

### GetImageFormats {#GetImageFormats}

<p>Get the image formats that this stream supports.</p>

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
                <code>vector&lt;<a class='link' href='../fuchsia.sysmem/'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/#ImageFormat_2'>ImageFormat_2</a>&gt;[256]</code>
            </td>
        </tr></table>



## **STRUCTS**

### FrameAvailableInfo {#FrameAvailableInfo}
*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#34)*



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
                <code><a class='link' href='#FrameMetadata'>FrameMetadata</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FrameRate {#FrameRate}
*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#44)*





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



## **ENUMS**

### DeviceType {#DeviceType}
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

### FrameStatus {#FrameStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#14)*

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



## **TABLES**

### StreamConstraints {#StreamConstraints}


*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#66)*

<p>These constraints are given to the Camera Manager when requesting a stream.  The
Camera Manager will use these constraints to match an appropriate stream.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#StreamProperties'>StreamProperties</a></code>
            </td>
            <td><p>A table that describes the properties of the stream. Any properties specified will
be considered requirements for matching streams.</p>
</td>
        </tr></table>

### DeviceInfo {#DeviceInfo}


*Defined in [fuchsia.camera2/manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/manager.fidl#78)*

<p>Identifying information about the device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>vendor_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Information from physical device enumeration:</p>
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
            <td><p>Information about the type of device:</p>
</td>
        </tr></table>

### FrameMetadata {#FrameMetadata}


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
            <td><p>|image_format_index| references the index into the vector of available
formats supported by the stream.</p>
</td>
        </tr></table>

### StreamProperties {#StreamProperties}


*Defined in [fuchsia.camera2/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2/stream.fidl#67)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream_type</code></td>
            <td>
                <code><a class='link' href='#CameraStreamType'>CameraStreamType</a></code>
            </td>
            <td><p>These could be one or more of the above mentioned Stream Types</p>
</td>
        </tr></table>







## **BITS**

### CameraStreamType {#CameraStreamType}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>MACHINE_LEARNING</td>
            <td>1</td>
            <td><p>ML request FR(Full Resolution) stream as well as
a DS(Down Scaled Resolution) stream for Security Use Case
which are of fixed resolutions</p>
</td>
        </tr><tr>
            <td>MONITORING</td>
            <td>2</td>
            <td><p>This is Security Video Stream which could support multiple
resolutions at runtime.</p>
</td>
        </tr><tr>
            <td>FULL_RESOLUTION</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>DOWNSCALED_RESOLUTION</td>
            <td>8</td>
            <td><p>ML request a DS stream for Video Conferencing which is fixed resolution</p>
</td>
        </tr><tr>
            <td>VIDEO_CONFERENCE</td>
            <td>16</td>
            <td><p>This is Video Conferencing Stream which could support
multiple resolutions at runtime.</p>
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
            <td><p>Maximum number of image formats per stream.</p>
</td>
        </tr>
    
</table>

