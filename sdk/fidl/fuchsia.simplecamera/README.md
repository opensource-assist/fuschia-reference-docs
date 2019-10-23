[TOC]

# fuchsia.simplecamera


## **PROTOCOLS**

## SimpleCamera {#SimpleCamera}
*Defined in [fuchsia.simplecamera/simple_camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.simplecamera/simple_camera.fidl#12)*

 Simple camera interface.  This will be deprecated when
 CameraManager replaces it.

### ConnectToCamera {#ConnectToCamera}

 Connect to a camera using the first enumerated format.
 The device opened will be /dev/class/camera/camera_id

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>image_pipe</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImagePipe'>ImagePipe</a></code>
            </td>
        </tr></table>

















