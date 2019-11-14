[TOC]

# fuchsia.hardware.telephony.transport


## **PROTOCOLS**

## Qmi {#Qmi}
*Defined in [fuchsia.hardware.telephony.transport/qmi.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-telephony-transport/qmi.fidl#10)*


### SetChannel {#SetChannel}

<p>Give a channel handle that transports bi-directional QMI messages</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>transport</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Qmi_SetChannel_Result'>Qmi_SetChannel_Result</a></code>
            </td>
        </tr></table>

### SetNetwork {#SetNetwork}

<p>Configure the network used by the transport
Currently only sets network up/down</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>connected</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetSnoopChannel {#SetSnoopChannel}

<p>Pass an interface for QMI message snooping</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interface</code></td>
            <td>
                <code><a class='link' href='../fuchsia.telephony.snoop/'>fuchsia.telephony.snoop</a>/<a class='link' href='../fuchsia.telephony.snoop/#Publisher'>Publisher</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Qmi_SetSnoopChannel_Result'>Qmi_SetSnoopChannel_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Qmi_SetChannel_Response {#Qmi_SetChannel_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Qmi_SetSnoopChannel_Response {#Qmi_SetSnoopChannel_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>







## **UNIONS**

### Qmi_SetChannel_Result {#Qmi_SetChannel_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Qmi_SetChannel_Response'>Qmi_SetChannel_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Qmi_SetSnoopChannel_Result {#Qmi_SetSnoopChannel_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Qmi_SetSnoopChannel_Response'>Qmi_SetSnoopChannel_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







