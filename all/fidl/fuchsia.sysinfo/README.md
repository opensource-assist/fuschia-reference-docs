[TOC]

# fuchsia.sysinfo


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.sysinfo/sysinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysinfo/sysinfo.fidl#23)*


### GetHypervisorResource {#GetHypervisorResource}


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
            <td><code>resource</code></td>
            <td>
                <code>handle&lt;resource&gt;?</code>
            </td>
        </tr></table>

### GetBoardName {#GetBoardName}


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

### GetBoardRevision {#GetBoardRevision}


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
            <td><code>revision</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetInterruptControllerInfo {#GetInterruptControllerInfo}


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
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#InterruptControllerInfo'>InterruptControllerInfo</a>?</code>
            </td>
        </tr></table>



## **STRUCTS**

### InterruptControllerInfo {#InterruptControllerInfo}
*Defined in [fuchsia.sysinfo/sysinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysinfo/sysinfo.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#InterruptControllerType'>InterruptControllerType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### InterruptControllerType {#InterruptControllerType}
Type: <code>uint32</code>

*Defined in [fuchsia.sysinfo/sysinfo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysinfo/sysinfo.fidl#11)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>APIC</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>GIC_V2</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>GIC_V3</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-sysinfo/sysinfo.fidl#9">SYSINFO_BOARD_NAME_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    
</table>

