Project: /_project.yaml
Book: /_book.yaml

# fuchsia.device


## **PROTOCOLS**

## Controller {:#Controller}
*Defined in [fuchsia.device/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#37)*

 Interface for manipulating a device in a devhost

### Bind {:#Bind}

 Attempt to bind the requested driver to this device

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>driver</code></td>
            <td>
                <code>string[1024]</code>
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

### ScheduleUnbind {:#ScheduleUnbind}

 Disconnect this device and allow its parent to be bound again.
 This may not complete before it returns.

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
        </tr></table>

### GetDriverName {:#GetDriverName}

 Return the name of the driver managing this the device

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
            <td><code>name</code></td>
            <td>
                <code>string[32]?</code>
            </td>
        </tr></table>

### GetDeviceName {:#GetDeviceName}

 Return the name of the device

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr></table>

### GetTopologicalPath {:#GetTopologicalPath}

 Return the topological path for this device

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
            <td><code>path</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr></table>

### GetEventHandle {:#GetEventHandle}

 Get an event for monitoring device conditions (see `DEVICE_SIGNAL_*` constants)

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
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;?</code>
            </td>
        </tr></table>

### GetDriverLogFlags {:#GetDriverLogFlags}

 Return the current logging flags for this device's driver

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
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetDriverLogFlags {:#SetDriverLogFlags}

 Set the logging flags for this device's driver.
 Each set bit in `clear_flags` will be cleared in the log flags state.
 Each set bit in `set_flags` will then be set in the log flags state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>clear_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>set_flags</code></td>
            <td>
                <code>uint32</code>
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

### DebugSuspend {:#DebugSuspend}

 Debug command: execute the device's suspend hook

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
        </tr></table>

### DebugResume {:#DebugResume}

 Debug command: execute the device's resume hook

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
        </tr></table>

### RunCompatibilityTests {:#RunCompatibilityTests}

 RunCompatibilityTests: Runs compatibility tests for the driver that binds to this device.
 The |hook_wait_time| is the time that the driver expects to take for each device hook in
 nanoseconds.
 Returns whether the driver passed the compatibility check.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hook_wait_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

## NameProvider {:#NameProvider}
*Defined in [fuchsia.device/name-provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/name-provider.fidl#13)*

 Interface for getting device names.

### GetDeviceName {:#GetDeviceName}

 Return the name of this Fuchsia device.

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
                <code><a class='link' href='#NameProvider_GetDeviceName_Result'>NameProvider_GetDeviceName_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### NameProvider_GetDeviceName_Response {:#NameProvider_GetDeviceName_Response}
*Defined in [fuchsia.device/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### NameProvider_GetDeviceName_Result {:#NameProvider_GetDeviceName_Result}
*Defined in [fuchsia.device/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#27)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#NameProvider_GetDeviceName_Response'>NameProvider_GetDeviceName_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#10">MAX_DEVICE_NAME_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#12">MAX_DEVICE_PATH_LEN</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#14">MAX_DRIVER_NAME_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#16">MAX_DRIVER_PATH_LEN</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#20">DEVICE_SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#24">DEVICE_SIGNAL_OOB</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#27">DEVICE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#30">DEVICE_SIGNAL_ERROR</a></td>
            <td>
                    <code>134217728</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#33">DEVICE_SIGNAL_HANGUP</a></td>
            <td>
                    <code>268435456</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/name-provider.fidl#9">DEFAULT_DEVICE_NAME</a></td>
            <td><code>fuchsia</code></td>
                    <td><code>String</code></td>
        </tr>
    
</table>

