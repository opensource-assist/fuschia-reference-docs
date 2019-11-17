[TOC]

# fuchsia.hardware.usb.peripheral


## **PROTOCOLS**

## Events {#Events}
*Defined in [fuchsia.hardware.usb.peripheral/usb-peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-usb-peripheral/usb-peripheral.fidl#42)*

<p>Events protocol that is used as a callback to inform the client
of the completion of various server-side events.
This callback interface can be registered using the SetStateChangeListener
method on the Device protocol.</p>

### FunctionRegistered {#FunctionRegistered}

<p>Invoked when a function registers</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### FunctionsCleared {#FunctionsCleared}

<p>Invoked when all functions have been cleared.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Device {#Device}
*Defined in [fuchsia.hardware.usb.peripheral/usb-peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-usb-peripheral/usb-peripheral.fidl#49)*


### SetConfiguration {#SetConfiguration}

<p>Sets the device's descriptors, adds the functions and creates the child devices for the
configuration's interfaces.
At least one function descriptor must be provided.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_desc</code></td>
            <td>
                <code><a class='link' href='#DeviceDescriptor'>DeviceDescriptor</a></code>
            </td>
        </tr><tr>
            <td><code>function_descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FunctionDescriptor'>FunctionDescriptor</a>&gt;[32]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_SetConfiguration_Result'>Device_SetConfiguration_Result</a></code>
            </td>
        </tr></table>

### ClearFunctions {#ClearFunctions}

<p>Tells the device to remove the child devices for the configuration's interfaces
and reset the list of functions to empty.
The caller should wait for the |FunctionsCleared| event.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetStateChangeListener {#SetStateChangeListener}

<p>Adds a state change listener that is invoked when a state change completes.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Events'>Events</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### Device_SetConfiguration_Response {#Device_SetConfiguration_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### FunctionDescriptor {#FunctionDescriptor}
*Defined in [fuchsia.hardware.usb.peripheral/usb-peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-usb-peripheral/usb-peripheral.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>interface_class</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>interface_subclass</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>interface_protocol</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceDescriptor {#DeviceDescriptor}
*Defined in [fuchsia.hardware.usb.peripheral/usb-peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-usb-peripheral/usb-peripheral.fidl#22)*



<p>The fields in DeviceDescriptor match those in usb_descriptor_t in the USB specification,
except for the string fields.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bcdUSB</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bDeviceClass</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bDeviceSubClass</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bDeviceProtocol</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bMaxPacketSize0</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>idVendor</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>idProduct</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bcdDevice</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer</code></td>
            <td>
                <code>string[127]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>product</code></td>
            <td>
                <code>string[127]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>serial</code></td>
            <td>
                <code>string[127]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bNumConfigurations</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Device_SetConfiguration_Result {#Device_SetConfiguration_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_SetConfiguration_Response'>Device_SetConfiguration_Response</a></code>
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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-usb-peripheral/usb-peripheral.fidl#9">MAX_FUNCTION_DESCRIPTORS</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-usb-peripheral/usb-peripheral.fidl#10">MAX_STRING_DESCRIPTORS</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-usb-peripheral/usb-peripheral.fidl#12">MAX_STRING_LENGTH</a></td>
            <td>
                    <code>127</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

