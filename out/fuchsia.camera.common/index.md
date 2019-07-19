Project: /_project.yaml
Book: /_book.yaml

# fuchsia.camera.common


## **PROTOCOLS**

## Stream {:#Stream}
*Defined in [fuchsia.camera.common/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#84)*

 Protocol shared between the driver and the consumer.

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
                <code><a class='link' href='../fuchsia.camera.common/index.html#FrameAvailableEvent'>FrameAvailableEvent</a></code>
            </td>
        </tr></table>

## VirtualCameraFactory {:#VirtualCameraFactory}
*Defined in [fuchsia.camera.common/virtual.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/virtual.fidl#42)*

 Protocol for managing virtual cameras that need to be added for tests.

### CreateDevice {:#CreateDevice}

 Creates a new VirtualCameraDevice based on the configuration passed in.
 `config`: a VirtualCameraConfig defining how the new device should behave.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html#VirtualCameraConfig'>VirtualCameraConfig</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### DeviceInfo {:#DeviceInfo}
*Defined in [fuchsia.camera.common/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#24)*



 Identifying information about the device.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Currently populated by the camera manager
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>vendor_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>product_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> string vendor_name;
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_stream_count</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> string product_name;
 string serial_number;
 The maximum number of stream interfaces that the device can support
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
*Defined in [fuchsia.camera.common/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#51)*



 Extra information associated with the frame.


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
*Defined in [fuchsia.camera.common/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#58)*



 Sent by the driver to the client when a frame is available for processing,
 or an error occurred.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frame_status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html#FrameStatus'>FrameStatus</a></code>
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
                <code><a class='link' href='../fuchsia.camera.common/index.html#Metadata'>Metadata</a></code>
            </td>
            <td> Any associated metadata such as timestamp.
</td>
            <td>No default</td>
        </tr>
</table>

### FrameRate {:#FrameRate}
*Defined in [fuchsia.camera.common/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#70)*



 The number of frames being produced every second.


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
*Defined in [fuchsia.camera.common/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#77)*



 Video format includes the image format and frame rate of frames being produced.


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
                <code><a class='link' href='../fuchsia.camera.common/index.html#FrameRate'>FrameRate</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ArtificialStreamConfig {:#ArtificialStreamConfig}
*Defined in [fuchsia.camera.common/virtual.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/virtual.fidl#11)*



 Configuration for an artificial stream.
 TODO(eweeks): Replace this stand-in with the full design.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code>int16</code>
            </td>
            <td> Numeric identifier for the stream being configured.
</td>
            <td>No default</td>
        </tr>
</table>

### RealWorldStreamConfig {:#RealWorldStreamConfig}
*Defined in [fuchsia.camera.common/virtual.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/virtual.fidl#18)*



 Configuration for a stream generated from stored frames.
 TODO(eweeks): Replace this stand-in with the full design.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code>int16</code>
            </td>
            <td> Numeric identifier for the stream being configured.
</td>
            <td>No default</td>
        </tr>
</table>

### VirtualCameraConfig {:#VirtualCameraConfig}
*Defined in [fuchsia.camera.common/virtual.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/virtual.fidl#32)*



 Configuration used by VirtualManager to create a VirtualCameraDevice.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>formats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.camera.common/index.html#VideoFormat'>VideoFormat</a>&gt;</code>
            </td>
            <td> The formats that the controller will support.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html#DeviceInfo'>DeviceInfo</a></code>
            </td>
            <td> Device specific information that can be set by the user.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>stream_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html#VirtualStreamConfig'>VirtualStreamConfig</a></code>
            </td>
            <td> Either an ArtificialStreamConfig or a RealWorldStreamConfig.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### FrameStatus {:#FrameStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.camera.common/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#39)*

 Status to be set when a frame is signaled available.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR_FRAME</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR_BUFFER_FULL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>







## **XUNIONS**

### VirtualStreamConfig {:#VirtualStreamConfig}
*Defined in [fuchsia.camera.common/virtual.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/virtual.fidl#26)*

 Configuration for the stream.
 The Configuration must be either artificial or real
 TODO(eweeks): Replace this stand-in with the full design.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>artificial_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html#ArtificialStreamConfig'>ArtificialStreamConfig</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>real_world_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera.common/index.html#RealWorldStreamConfig'>RealWorldStreamConfig</a></code>
            </td>
            <td></td>
        </tr></table>





## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#13">CAMERA_OUTPUT_UNKNOWN</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#14">CAMERA_OUTPUT_STILL_IMAGE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#15">CAMERA_OUTPUT_BURST</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#16">CAMERA_OUTPUT_STREAM</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#17">CAMERA_OUTPUT_HDR</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#18">CAMERA_OUTPUT_DEPTH</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-camera-common/common.fidl#19">CAMERA_OUTPUT_STEREO</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

