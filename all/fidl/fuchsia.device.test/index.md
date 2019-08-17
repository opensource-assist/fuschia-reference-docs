Project: /_project.yaml
Book: /_book.yaml

# fuchsia.device.test


## **PROTOCOLS**

## Test {:#Test}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#23)*


### RunTests {:#RunTests}

 Execute the tests for this device. Returns the status from the test. If
 used as part of the Device protocol then Test output will be streamed to
 the socket set by SetOutputSocket().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>report</code></td>
            <td>
                <code><a class='link' href='#TestReport'>TestReport</a></code>
            </td>
        </tr></table>

## Device {:#Device}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#32)*

 Interface for controlling a device created via RootDevice.CreateDevice

### RunTests {:#RunTests}

 Execute the tests for this device. Returns the status from the test. If
 used as part of the Device protocol then Test output will be streamed to
 the socket set by SetOutputSocket().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>report</code></td>
            <td>
                <code><a class='link' href='#TestReport'>TestReport</a></code>
            </td>
        </tr></table>

### SetOutputSocket {:#SetOutputSocket}

 Set a socket to stream test output to.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sock</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>



### SetChannel {:#SetChannel}

 Set a channel for the test to use in a test-specific manner.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>chan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Destroy {:#Destroy}

 Unload this device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## RootDevice {:#RootDevice}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#53)*

 Interface for creating devices within a devhost.

### CreateDevice {:#CreateDevice}

 Create a device with the given `name` that is a child of this device.
 If `name` contains a trailing ".so", it will be removed.

 On success, `path` will be the filesystem path of the new device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[31]</code>
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
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr></table>



## **STRUCTS**

### TestReport {:#TestReport}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#13)*



 Returns the result summary of a test run


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>test_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Total number of tests
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>success_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of successful tests
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>failure_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Number of failed tests
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#10">CONTROL_DEVICE</a></td>
            <td><code>/dev/test/test</code></td>
                    <td><code>String</code></td>
            <td> The path which can be used to open the control device
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#46">MAX_DEVICE_NAME_LEN</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum device name len.  This value must match `ZX_DEVICE_NAME_MAX`.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#49">MAX_DEVICE_PATH_LEN</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum device path len
</td>
        </tr>
    
</table>

