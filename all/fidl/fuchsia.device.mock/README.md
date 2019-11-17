[TOC]

# fuchsia.device.mock


## **PROTOCOLS**

## MockDevice {#MockDevice}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#78)*

<p>Interface for controlling a mock device.  The test suite will implement this interface.
Any method that returns a list of actions is interpreted as requesting the corresponding hook
to perform that list of actions in order.</p>

### Bind {#Bind}

<p><code>record.device_id</code> corresponds to the parent here.</p>

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

### Release {#Release}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>record</code></td>
            <td>
                <code><a class='link' href='#HookInvocation'>HookInvocation</a></code>
            </td>
        </tr></table>



### GetProtocol {#GetProtocol}


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

### Open {#Open}


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

### Close {#Close}


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

### Unbind {#Unbind}


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

### Read {#Read}


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

### Write {#Write}


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

### GetSize {#GetSize}


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

### Suspend {#Suspend}


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

### Resume {#Resume}


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

### Message {#Message}


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

### Rxrpc {#Rxrpc}


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

### AddDeviceDone {#AddDeviceDone}

<p>Notification that the requested action was done</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### UnbindReplyDone {#UnbindReplyDone}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## MockDeviceThread {#MockDeviceThread}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#103)*

<p>Interface for requesting a mock device thread do something.  The mock device implements
this interface.  Closing the interface causes the thread to exit.</p>

### PerformActions {#PerformActions}

<p>Perform the actions in the given list.  Threads may not create other threads.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[10]</code>
            </td>
        </tr></table>



### AddDeviceDone {#AddDeviceDone}

<p>Notification that the requested action was done</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### UnbindReplyDone {#UnbindReplyDone}




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

### HookInvocation {#HookInvocation}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#10)*



<p>A record of the invocation of a hook</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>process_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Process that the hook was invoked in</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>thread_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Thread that the hook was invoked on</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>device_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>An opaque identifier identifying a specific device</p>
</td>
            <td>No default</td>
        </tr>
</table>

### UnbindReplyAction {#UnbindReplyAction}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#20)*



<p>Marker struct for unbind reply action</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Value that will be echoed back in the completion message</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AddDeviceAction {#AddDeviceAction}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#29)*



<p>Request to add a new child device</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>action_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Value that will be echoed back in the completion message</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>do_bind</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If true, will let the device go through the bind protocol.
Otherwise, will just create another mock device and skip binding.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code><a class='link' href='#MockDevice'>MockDevice</a>?</code>
            </td>
            <td><p>If creating a mock device, the service the new device will listen to.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td><p>The name that should be given to the new device.  Used by devfs and
debug messages.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>vector&lt;uint64&gt;[32]</code>
            </td>
            <td><p>The properties to attach the newly created device</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>expect_status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The expected return status from device_add()</p>
</td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Action {#Action}
*Defined in [fuchsia.device.mock/mock-device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#52)*

<p>What a hook should do.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>return_status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>Return this status.</p>
</td>
        </tr><tr>
            <td><code>write</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16384]</code>
            </td>
            <td><p>Write these bytes to the buffer associated with the hook.</p>
</td>
        </tr><tr>
            <td><code>create_thread</code></td>
            <td>
                <code>request&lt;<a class='link' href='#MockDeviceThread'>MockDeviceThread</a>&gt;</code>
            </td>
            <td><p>Create a new thread with a processing loop.</p>
</td>
        </tr><tr>
            <td><code>async_remove_device</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Invoke device_async_remove() on our device.</p>
</td>
        </tr><tr>
            <td><code>unbind_reply</code></td>
            <td>
                <code><a class='link' href='#UnbindReplyAction'>UnbindReplyAction</a></code>
            </td>
            <td><p>Signal that the unbind has completed.</p>
</td>
        </tr><tr>
            <td><code>add_device</code></td>
            <td>
                <code><a class='link' href='#AddDeviceAction'>AddDeviceAction</a></code>
            </td>
            <td><p>Create a new child device</p>
</td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#25">MAX_PROPERTIES_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#26">MAX_NAME_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#72">MAX_ACTIONS</a></td>
            <td>
                    <code>10</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/dev/test/mock-device/mock-device.fidl#73">MAX_WRITE_BYTES</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

