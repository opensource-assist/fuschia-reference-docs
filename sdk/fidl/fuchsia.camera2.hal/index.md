Project: /_project.yaml
Book: /_book.yaml

# fuchsia.camera2.hal


## **PROTOCOLS**

## Controller {:#Controller}
*Defined in [fuchsia.camera2.hal/hal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2.hal/hal.fidl#46)*

 This is the interface to the camera driver
 which allows setting up a given configuration
 and setting up a stream.

### GetConfigs {:#GetConfigs}

 Get a list of all available configurations which the camera driver supports.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Config'>Config</a>&gt;[256]?</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### CreateStream {:#CreateStream}

 Set a particular configuration and create the requested stream.
 |config_index| : Configuration index from the vector which needs to be applied.
 |stream_index| : Stream index from the vector of streams provided within a config.
 |buffer_collection| : Buffer collections for the stream.
 |stream| : Stream channel for the stream requested
 |image_format_index| : Image format index which needs to be set up upon creation.
 If there is already an active configuration which is different than the one
 which is requested to be set, then the HAL will be closing all existing streams
 and honor this new setup call.
 If the new stream requested is already part of the existing running configuration
 the HAL will just be creating this new stream while the other stream still exists as is.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config_index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>stream_index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>image_format_index</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>buffer_collection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionInfo_2'>BufferCollectionInfo_2</a></code>
            </td>
        </tr><tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.camera2/index.html'>fuchsia.camera2</a>/<a class='link' href='../fuchsia.camera2/index.html#Stream'>Stream</a>&gt;</code>
            </td>
        </tr></table>



### EnableStreaming {:#EnableStreaming}

 Enable/Disable Streaming

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### DisableStreaming {:#DisableStreaming}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetDeviceInfo {:#GetDeviceInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera2/index.html'>fuchsia.camera2</a>/<a class='link' href='../fuchsia.camera2/index.html#DeviceInfo'>DeviceInfo</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### StreamConfig {:#StreamConfig}
*Defined in [fuchsia.camera2.hal/hal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2.hal/hal.fidl#18)*



 Represents one stream within a particular configuration.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frame_rate</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera2/index.html'>fuchsia.camera2</a>/<a class='link' href='../fuchsia.camera2/index.html#FrameRate'>FrameRate</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>constraints</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionConstraints'>BufferCollectionConstraints</a></code>
            </td>
            <td> |constraints| should allow for all the image formats listed in image_formats.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera2/index.html'>fuchsia.camera2</a>/<a class='link' href='../fuchsia.camera2/index.html#StreamProperties'>StreamProperties</a></code>
            </td>
            <td> Properties of the stream:
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_formats</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#ImageFormat_2'>ImageFormat_2</a>&gt;[256]</code>
            </td>
            <td> We need to specify both the constraints & the image formats because
 there are fixed set of resolutions supported by the Camera Controller
 so a range within the |constraints| won't be sufficient.
 Some streams support multiple resolutions for same configuration
 We would need to change the resolution runtime, without stopping the
 streaming. This provides a list of resolutions a stream would be providing.
 At least one format must be provided.
</td>
            <td>No default</td>
        </tr>
</table>

### Config {:#Config}
*Defined in [fuchsia.camera2.hal/hal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2.hal/hal.fidl#37)*



 Represents one configuration


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_configs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StreamConfig'>StreamConfig</a>&gt;[64]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2.hal/hal.fidl#12">MAX_CONFIGURATIONS</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maximum number of configurations per device.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.camera2.hal/hal.fidl#15">MAX_STREAMS</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maximum number of streams per config.
</td>
        </tr>
    
</table>

