[TOC]

# fuchsia.hardware.input


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.hardware.input/input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#40)*


### GetBootProtocol {#GetBootProtocol}

<p>Get the HID boot interface protocol this device supports</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#BootProtocol'>BootProtocol</a></code>
            </td>
        </tr></table>

### GetDeviceIds {#GetDeviceIds}

<p>Get the Device's IDs. If this is a real HID device, the IDs will come from the device.
If it is a mock HID decice, the IDs will either be 0's or user defined.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ids</code></td>
            <td>
                <code><a class='link' href='#DeviceIds'>DeviceIds</a></code>
            </td>
        </tr></table>

### GetReportDescSize {#GetReportDescSize}

<p>Get the size of the report descriptor</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### GetReportDesc {#GetReportDesc}

<p>Get the report descriptor</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>desc</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### GetNumReports {#GetNumReports}

<p>Get the number of reports in the report descriptor</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>count</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### GetReportIds {#GetReportIds}

<p>Get the report ids that are used in the report descriptor</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ids</code></td>
            <td>
                <code>vector&lt;uint8&gt;[256]</code>
            </td>
        </tr></table>

### GetReportSize {#GetReportSize}

<p>Get the size of a single report for the given (type, id) pair.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ReportType'>ReportType</a></code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#ReportId'>ReportId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### GetMaxInputReportSize {#GetMaxInputReportSize}

<p>Get the maximum size of a single input report.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### GetReports {#GetReports}

<p>Receive up to MAX_REPORT_DATA bytes of reports that have been sent from a device.
This is the interface that is supposed to be used for continuous polling.
Multiple reports can be returned from this API at a time, it is up to the client
to do the parsing of the reports with the correct sizes and offset.
It is guaranteed that only whole reports will be sent.
If there are no reports, this will return ZX_ERR_SHOULD_WAIT, and the client can
wait on the event from |GetReportsEvent|.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### GetReportsEvent {#GetReportsEvent}

<p>Receive an event that will be signalled when there are reports in the
Device's report FIFO.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>

### GetReport {#GetReport}

<p>Get a single report of the given (type, id) pair.  This interface is not intended
to be used for continuous polling of the reports.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ReportType'>ReportType</a></code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#ReportId'>ReportId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr><tr>
            <td><code>report</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### SetReport {#SetReport}

<p>Set a single report of the given (type, id) pair.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ReportType'>ReportType</a></code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#ReportId'>ReportId</a></code>
            </td>
        </tr><tr>
            <td><code>report</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SetTraceId {#SetTraceId}

<p>Set the trace ID that is used for HID report flow events.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>





## **STRUCTS**

### DeviceIds {#DeviceIds}
*Defined in [fuchsia.hardware.input/input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#33)*



<p>DeviceIds lets a clients determine the vendor and product id for a device.
If the device is real HID device, then the id information
will come from the device itself. Mock HID devices may assign the
ids in the driver. If the mock HID driver does not assign ids, zeros
will be used instead.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vendor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>product_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>version</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### BootProtocol {#BootProtocol}
Type: <code>uint32</code>

*Defined in [fuchsia.hardware.input/input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#11)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>KBD</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>MOUSE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ReportType {#ReportType}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.input/input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#22)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INPUT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>OUTPUT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FEATURE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_DESC_LEN">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#17">MAX_DESC_LEN</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAX_REPORT_LEN">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#18">MAX_REPORT_LEN</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAX_REPORT_DATA">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#19">MAX_REPORT_DATA</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr id="MAX_REPORT_IDS">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#20">MAX_REPORT_IDS</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="ReportId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#9">ReportId</a></td>
            <td>
                <code>uint8</code></td>
            <td></td>
        </tr></table>

