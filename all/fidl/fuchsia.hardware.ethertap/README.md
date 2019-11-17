[TOC]

# fuchsia.hardware.ethertap


## **PROTOCOLS**

## TapDevice {#TapDevice}
*Defined in [fuchsia.hardware.ethertap/ethertap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#45)*

<p>Provides control over the created tap device. The lifetime of the device itself is tied to the
channel over which this protocol is served, closing a <code>TapDevice</code> channel will trigger the
destruction and deallocation of the underlying tap device.</p>

### WriteFrame {#WriteFrame}

<p>Writes data to the tap device. If device is offline, data will just be discarded.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[2000]</code>
            </td>
        </tr></table>



### OnFrame {#OnFrame}

<p>Triggered when data is sent on this tap device.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[2000]</code>
            </td>
        </tr></table>

### SetOnline {#SetOnline}

<p>Sets online status of ethertap device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>online</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnReportParams {#OnReportParams}

<p>If <code>OPT_REPORT_PARAM</code> is set on <code>options</code>, calls to EthernetImplcSetParam will be routed to
this event, containing the set parameters request arguments.</p>



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

## TapControl {#TapControl}
*Defined in [fuchsia.hardware.ethertap/ethertap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#60)*

<p>Ethertap driver interface.</p>

### OpenDevice {#OpenDevice}

<p>Opens a named device with given <code>name</code> and <code>config</code>.
<code>name</code> is only used for debugging purposes.
If <code>config</code> is not valid or the tap device could not be created, an error status is returned
and no <code>device</code> is created.</p>

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
                <code><a class='link' href='#Config'>Config</a></code>
            </td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code>request&lt;<a class='link' href='#TapDevice'>TapDevice</a>&gt;</code>
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

### Config {#Config}
*Defined in [fuchsia.hardware.ethertap/ethertap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#29)*



<p>Configuration of an ethertap device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Ethertap options, a bit mask of OPT_* constants.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>features</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Features that will be reported to Ethernet protocol.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mtu</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Ethertap device mtu. If a value greater than <code>MAX_MTU</code> is provided, creating an ethertap
device will fail.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/#MacAddress'>MacAddress</a></code>
            </td>
            <td><p>MAC address to report.</p>
</td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#11">OPT_TRACE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Enables tracing of the ethertap device itself.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#13">OPT_TRACE_PACKETS</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Enables tracing of individual packets.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#17">OPT_REPORT_PARAM</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Report EthernetImplSetParam() over EthertapController, and return success from
EthernetImplSetParam().  If this option is not set, EthernetImplSetParam() will return
<code>ZX_ERR_NOT_SUPPORTED</code>.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#19">OPT_ONLINE</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Starts ethertap device with link online.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#22">MAX_MTU</a></td>
            <td>
                    <code>2000</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum MTU supported by ethertap driver.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#24">MAX_PARAM_DATA</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum size of trailing data on params report.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-ethertap/ethertap.fidl#26">MAX_NAME_LENGTH</a></td>
            <td>
                    <code>30</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length of tap device name.</p>
</td>
        </tr>
    
</table>

