Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.telephony.transport


## **PROTOCOLS**

## Qmi {:#Qmi}
*Defined in [fuchsia.hardware.telephony.transport/qmi.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-telephony-transport/qmi.fidl#11)*


### SetChannel {:#SetChannel}

 Give a channel handle that transports bi-directional QMI messages

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

### SetNetwork {:#SetNetwork}

 Configure the network used by the transport
 Currently only sets network up/down

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

### SetSnoopChannel {:#SetSnoopChannel}

 Pass an interface for QMI message snooping

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interface</code></td>
            <td>
                <code><a class='link' href='../fuchsia.telephony.snoop/index.html'>fuchsia.telephony.snoop</a>/<a class='link' href='../fuchsia.telephony.snoop/index.html#Publisher'>Publisher</a></code>
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

### Qmi_SetChannel_Response {:#Qmi_SetChannel_Response}
*Defined in [fuchsia.hardware.telephony.transport/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#2)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Qmi_SetSnoopChannel_Response {:#Qmi_SetSnoopChannel_Response}
*Defined in [fuchsia.hardware.telephony.transport/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>







## **UNIONS**

### Qmi_SetChannel_Result {:#Qmi_SetChannel_Result}
*Defined in [fuchsia.hardware.telephony.transport/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#5)*


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

### Qmi_SetSnoopChannel_Result {:#Qmi_SetSnoopChannel_Result}
*Defined in [fuchsia.hardware.telephony.transport/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#14)*


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







