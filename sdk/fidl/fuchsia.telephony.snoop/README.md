[TOC]

# fuchsia.telephony.snoop


## **PROTOCOLS**

## Publisher {#Publisher}
*Defined in [fuchsia.telephony.snoop/tel-snoop.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-telephony-snoop/tel-snoop.fidl#27)*

 Protocol for forwarding messages to Snooper.

### SendMessage {#SendMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>msg</code></td>
            <td>
                <code><a class='link' href='#Message'>Message</a></code>
            </td>
        </tr></table>



## Snooper {#Snooper}
*Defined in [fuchsia.telephony.snoop/tel-snoop.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-telephony-snoop/tel-snoop.fidl#33)*

 Protocol for forwarding Message from Snooper.

### GetDeviceNum {#GetDeviceNum}

 Get number of devices that connect to Snooper.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_num</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### OnMessage {#OnMessage}

 Snoop message which receives by Snooper client.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>msg</code></td>
            <td>
                <code><a class='link' href='#Message'>Message</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### QmiMessage {#QmiMessage}
*Defined in [fuchsia.telephony.snoop/tel-snoop.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-telephony-snoop/tel-snoop.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>direction</code></td>
            <td>
                <code><a class='link' href='#Direction'>Direction</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_partial_copy</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>opaque_bytes</code></td>
            <td>
                <code>uint8[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Direction {#Direction}
Type: <code>uint32</code>

*Defined in [fuchsia.telephony.snoop/tel-snoop.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-telephony-snoop/tel-snoop.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FROM_MODEM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TO_MODEM</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Message {#Message}
*Defined in [fuchsia.telephony.snoop/tel-snoop.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-telephony-snoop/tel-snoop.fidl#22)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>qmi_message</code></td>
            <td>
                <code><a class='link' href='#QmiMessage'>QmiMessage</a></code>
            </td>
            <td></td>
        </tr></table>







