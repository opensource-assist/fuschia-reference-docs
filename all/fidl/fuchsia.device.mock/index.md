Project: /_project.yaml
Book: /_book.yaml

# fuchsia.device.mock


## **PROTOCOLS**

## MockDevice {:#MockDevice}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#75)*

 Interface for controlling a mock device.  The test suite will implement this interface.
 Any method that returns a list of actions is interpreted as requesting the corresponding hook
 to perform that list of actions in order.

### Bind {:#Bind}

 `record.device_id` corresponds to the parent here.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Release {:#Release}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr></table>



### GetProtocol {:#GetProtocol}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr><tr>
            <td><code>protocol_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Open {:#Open}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Close {:#Close}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Unbind {:#Unbind}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Read {:#Read}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>off</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Write {:#Write}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16384]</code>
            </td>
        </tr><tr>
            <td><code>off</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### GetSize {:#GetSize}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Suspend {:#Suspend}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Resume {:#Resume}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Message {:#Message}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### Rxrpc {:#Rxrpc}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>

### AddDeviceDone {:#AddDeviceDone}

 Notification that the requested action was done

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### RemoveDeviceDone {:#RemoveDeviceDone}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## MockDeviceThread {:#MockDeviceThread}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#100)*

 Interface for requesting a mock device thread do something.  The mock device implements
 this interface.  Closing the interface causes the thread to exit.

### PerformActions {:#PerformActions}

 Perform the actions in the given list.  Threads may not create other threads.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>



### AddDeviceDone {:#AddDeviceDone}

 Notification that the requested action was done



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### RemoveDeviceDone {:#RemoveDeviceDone}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## **STRUCTS**

### HookInvocation {:#HookInvocation}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#10)*



 A record of the invocation of a hook


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>process_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Process that the hook was invoked in
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>thread_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Thread that the hook was invoked on
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>device_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> An opaque identifier identifying a specific device
</td>
            <td>No default</td>
        </tr>
</table>

### RemoveDeviceAction {:#RemoveDeviceAction}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#20)*



 Marker struct for remove action


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Value that will be echoed back in the completion message
</td>
            <td>No default</td>
        </tr>
</table>

### AddDeviceAction {:#AddDeviceAction}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#29)*



 Request to add a new child device


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Value that will be echoed back in the completion message
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>do_bind</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, will let the device go through the bind protocol.
 Otherwise, will just create another mock device and skip binding.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code><a class='link' href='#MockDevice'>MockDevice</a>?</code>
            </td>
            <td> If creating a mock device, the service the new device will listen to.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td> The name that should be given to the new device.  Used by devfs and
 debug messages.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>vector&lt;uint64&gt;[32]</code>
            </td>
            <td> The properties to attach the newly created device
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>expect_status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> The expected return status from device_add()
</td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Action {:#Action}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#52)*

 What a hook should do.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>return_status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> Return this status.
</td>
        </tr><tr>
            <td><code>write</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16384]</code>
            </td>
            <td> Write these bytes to the buffer associated with the hook.
</td>
        </tr><tr>
            <td><code>create_thread</code></td>
            <td>
                <code>request&lt;<a class='link' href='#MockDeviceThread'>MockDeviceThread</a>&gt;</code>
            </td>
            <td> Create a new thread with a processing loop.
</td>
        </tr><tr>
            <td><code>remove_device</code></td>
            <td>
                <code><a class='link' href='#RemoveDeviceAction'>RemoveDeviceAction</a></code>
            </td>
            <td> Invoke device_remove() on our device.
</td>
        </tr><tr>
            <td><code>add_device</code></td>
            <td>
                <code><a class='link' href='#AddDeviceAction'>AddDeviceAction</a></code>
            </td>
            <td> Create a new child device
</td>
        </tr></table>







## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#25">MAX_PROPERTIES_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#26">MAX_NAME_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#69">MAX_ACTIONS</a></td>
            <td>
                    <code>10</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#70">MAX_WRITE_BYTES</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

