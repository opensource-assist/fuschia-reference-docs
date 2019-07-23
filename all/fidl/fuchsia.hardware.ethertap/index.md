Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.ethertap


## **PROTOCOLS**

## TapDevice {:#TapDevice}
*Defined in [fuchsia.hardware.ethertap/ethertap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#45)*

 Provides control over the created tap device. The lifetime of the device itself is tied to the
 channel over which this protocol is served, closing a `TapDevice` channel will trigger the
 destruction and deallocation of the underlying tap device.

### WriteFrame {:#WriteFrame}

 Writes data to the tap device. If device is offline, data will just be discarded.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[2000]</code>
            </td>
        </tr></table>



### OnFrame {:#OnFrame}

 Triggered when data is sent on this tap device.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[2000]</code>
            </td>
        </tr></table>

### SetOnline {:#SetOnline}

 Sets online status of ethertap device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>online</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnReportParams {:#OnReportParams}

 If `OPT_REPORT_PARAM` is set on `options`, calls to EthernetImplcSetParam will be routed to
 this event, containing the set parameters request arguments.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>param</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[64]?</code>
            </td>
        </tr></table>

## TapControl {:#TapControl}
*Defined in [fuchsia.hardware.ethertap/ethertap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#60)*

 Ethertap driver interface.

### OpenDevice {:#OpenDevice}

 Opens a named device with given `name` and `config`.
 `name` is only used for debugging purposes.
 If `config` is not valid or the tap device could not be created, an error status is returned
 and no `device` is created.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[30]</code>
            </td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethertap/index.html#Config'>Config</a></code>
            </td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.ethertap/index.html#TapDevice'>TapDevice</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



## **STRUCTS**

### Config {:#Config}
*Defined in [fuchsia.hardware.ethertap/ethertap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#29)*



 Configuration of an ethertap device.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Ethertap options, a bit mask of OPT_* constants.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>features</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Features that will be reported to Ethernet protocol.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mtu</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Ethertap device mtu. If a value greater than MAX_MTU is provided, creating an ethertap
 device will fail.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/index.html'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/index.html#MacAddress'>MacAddress</a></code>
            </td>
            <td> MAC address to report.
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#11">OPT_TRACE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#13">OPT_TRACE_PACKETS</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#17">OPT_REPORT_PARAM</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#19">OPT_ONLINE</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#22">MAX_MTU</a></td>
            <td>
                    <code>2000</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#24">MAX_PARAM_DATA</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#26">MAX_NAME_LENGTH</a></td>
            <td>
                    <code>30</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

