[TOC]

# fuchsia.factory.camera


## **PROTOCOLS**

## CameraFactory {#CameraFactory}
*Defined in [fuchsia.factory.camera/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory.camera/factory.fidl#28)*

<p>A protocol for all devices with cameras going through factory calibration
procedures. The devices are exposed as servers; this is meant to receive calls from
and send data back to a SL4F Facade.</p>

### DetectCamera {#DetectCamera}

<p>Checks whether the device under test has a camera and provides information about
it. If the device has multiple cameras, the first one listed is chosen.</p>
<ul>
<li>response <code>camera_id</code> Identifies the camera. This should not change throughout
the lifetime of the camera. Is null if no camera exists.</li>
<li>response <code>camera_info</code> A table providing identifying information about the
camera. Is null if no camera exists.</li>
</ul>
<ul>
<li>error A value indicating whether there is a camera.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_DetectCamera_Result'>CameraFactory_DetectCamera_Result</a></code>
            </td>
        </tr></table>

### Start {#Start}

<p>Initializes the camera sensor (and associated MIPI) and connects to a stream.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Stop {#Stop}

<p>Stops the camera sensor (and associated MIPI) stream.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetConfig {#SetConfig}

<p>Sets the parameters for the camera's sensor config.</p>
<ul>
<li>request <code>mode</code> One of the camera's predefined sensor modes (fpms, resolution,
etc).</li>
<li>request <code>exposure</code> The camera's sensor exposure parameter.</li>
<li>request <code>analog_gain</code> The camera's sensor analog gain parameter.</li>
<li>request <code>digital_gain</code> The camera's sensor digital gain parameter.</li>
</ul>
<ul>
<li>error A value indicating the type of failure, if any. This may occur if there
is no camera or it is not streaming.</li>
<li>See <a class='link' href='#camerasensor.banjo'>camerasensor.banjo</a> for more information on these params:
//zircon/system/banjo/ddk.protocol.camerasensor/camerasensor.banjo</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>exposure</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>analog_gain</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>digital_gain</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_SetConfig_Result'>CameraFactory_SetConfig_Result</a></code>
            </td>
        </tr></table>

### CaptureImage {#CaptureImage}

<p>Instructs the device to save a frame from the stream, and send it back to the
host.</p>
<ul>
<li>response <code>image_data</code> A blob of bytes representing the captured image.</li>
<li>response <code>image_info</code> A struct outlining the image's properties, e.g.
width/height, pixel format, etc.</li>
</ul>
<ul>
<li>error A value indicating the type of failure, if any. This may occur if there
is no camera or it is not streaming.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_CaptureImage_Result'>CameraFactory_CaptureImage_Result</a></code>
            </td>
        </tr></table>

### WriteCalibrationData {#WriteCalibrationData}

<p>Instructs the device to save tuning data to a persistent factory partition.</p>
<ul>
<li>request <code>calibration_data</code> A blob of calibration data to be written to disk.</li>
<li>request <code>file_path</code> Outlines where on device the data is to be written.</li>
</ul>
<ul>
<li>error A value indicating an IO failure, if any.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>calibration_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr><tr>
            <td><code>file_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_WriteCalibrationData_Result'>CameraFactory_WriteCalibrationData_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### CameraFactory_DetectCamera_Response {#CameraFactory_DetectCamera_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>camera_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.camera2/'>fuchsia.camera2</a>/<a class='link' href='../fuchsia.camera2/#DeviceInfo'>DeviceInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CameraFactory_SetConfig_Response {#CameraFactory_SetConfig_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### CameraFactory_CaptureImage_Response {#CameraFactory_CaptureImage_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>image_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImageInfo'>ImageInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CameraFactory_WriteCalibrationData_Response {#CameraFactory_WriteCalibrationData_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### CameraFactoryError {#CameraFactoryError}
Type: <code>uint32</code>

*Defined in [fuchsia.factory.camera/factory.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory.camera/factory.fidl#14)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_CAMERA</code></td>
            <td><code>1</code></td>
            <td><p>The device does not have a camera, or the camera stack can otherwise not be
reached.</p>
</td>
        </tr><tr>
            <td><code>STREAMING</code></td>
            <td><code>2</code></td>
            <td><p>No image could be captured. Most likely because the stream has not been started.</p>
</td>
        </tr></table>





## **UNIONS**

### CameraFactory_DetectCamera_Result {#CameraFactory_DetectCamera_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_DetectCamera_Response'>CameraFactory_DetectCamera_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#CameraFactoryError'>CameraFactoryError</a></code>
            </td>
            <td></td>
        </tr></table>

### CameraFactory_SetConfig_Result {#CameraFactory_SetConfig_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_SetConfig_Response'>CameraFactory_SetConfig_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#CameraFactoryError'>CameraFactoryError</a></code>
            </td>
            <td></td>
        </tr></table>

### CameraFactory_CaptureImage_Result {#CameraFactory_CaptureImage_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_CaptureImage_Response'>CameraFactory_CaptureImage_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#CameraFactoryError'>CameraFactoryError</a></code>
            </td>
            <td></td>
        </tr></table>

### CameraFactory_WriteCalibrationData_Result {#CameraFactory_WriteCalibrationData_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#CameraFactory_WriteCalibrationData_Response'>CameraFactory_WriteCalibrationData_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="FILE_PATH_MAX_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.factory.camera/factory.fidl#12">FILE_PATH_MAX_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



