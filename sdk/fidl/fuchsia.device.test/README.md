[TOC]

# fuchsia.device.test


## **PROTOCOLS**

## Test {#Test}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#23)*


### RunTests {#RunTests}

<p>Execute the tests for this device. Returns the status from the test. If
used as part of the Device protocol then Test output will be streamed to
the socket set by SetOutputSocket().</p>

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

## Device {#Device}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#32)*

<p>Interface for controlling a device created via RootDevice.CreateDevice</p>

### RunTests {#RunTests}

<p>Execute the tests for this device. Returns the status from the test. If
used as part of the Device protocol then Test output will be streamed to
the socket set by SetOutputSocket().</p>

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

### SetOutputSocket {#SetOutputSocket}

<p>Set a socket to stream test output to.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sock</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr></table>



### SetChannel {#SetChannel}

<p>Set a channel for the test to use in a test-specific manner.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>chan</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Destroy {#Destroy}

<p>Unload this device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## RootDevice {#RootDevice}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#53)*

<p>Interface for creating devices within a devhost.</p>

### CreateDevice {#CreateDevice}

<p>Create a device with the given <code>name</code> that is a child of this device.
If <code>name</code> contains a trailing &quot;.so&quot;, it will be removed.</p>
<p>On success, <code>path</code> will be the filesystem path of the new device.</p>

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

### TestReport {#TestReport}
*Defined in [fuchsia.device.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#13)*



<p>Returns the result summary of a test run</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>test_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Total number of tests</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>success_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of successful tests</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>failure_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of failed tests</p>
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
            <td><p>The path which can be used to open the control device</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#46">MAX_DEVICE_NAME_LEN</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum device name len.  This value must match <code>ZX_DEVICE_NAME_MAX</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-test/test.fidl#49">MAX_DEVICE_PATH_LEN</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum device path len</p>
</td>
        </tr>
    
</table>



