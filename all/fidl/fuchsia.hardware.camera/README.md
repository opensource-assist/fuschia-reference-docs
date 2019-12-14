[TOC]

# fuchsia.hardware.camera


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.hardware.camera/camera.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-camera/camera.fidl#8)*


### GetChannel {#GetChannel}

<p>Note: this method obtains a channel to the capture device which
communicates using a non-simple fidl interface.  Once the
system has been updated to support normal fidl protocols, this method
can be replaced with the protocol itself.
Additionally, while the camera stack is migrating from camera to
camera2, two methods are available, corresponding to the two
versions of the protocol.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### GetChannel2 {#GetChannel2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



















