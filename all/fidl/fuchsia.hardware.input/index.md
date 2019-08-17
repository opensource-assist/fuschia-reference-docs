Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.input


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.input/input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#28)*


### GetBootProtocol {:#GetBootProtocol}


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

### GetReportDescSize {:#GetReportDescSize}


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

### GetReportDesc {:#GetReportDesc}


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

### GetNumReports {:#GetNumReports}


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

### GetReportIds {:#GetReportIds}


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

### GetReportSize {:#GetReportSize}


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
                <code>uint8</code>
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
            <td><code>size</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### GetMaxInputReportSize {:#GetMaxInputReportSize}


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

### GetReport {:#GetReport}


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
                <code>uint8</code>
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
            <td><code>report</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
        </tr></table>

### SetReport {:#SetReport}


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
                <code>uint8</code>
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
                <code>int32</code>
            </td>
        </tr></table>

### SetTraceId {:#SetTraceId}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>







## **ENUMS**

### BootProtocol {:#BootProtocol}
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

### ReportType {:#ReportType}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.input/input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#21)*



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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#17">MAX_DESC_LEN</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#18">MAX_REPORT_LEN</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-input/input.fidl#19">MAX_REPORT_IDS</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>

