Project: /_project.yaml
Book: /_book.yaml

# fuchsia.telephony.snoop


## **PROTOCOLS**

## Publisher {:#Publisher}
*Defined in [fuchsia.telephony.snoop/tel-snoop.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-telephony-snoop/tel-snoop.fidl#28)*

 Protocol for forwarding QMI messages from driver to Snoop CLI

### SendMessage {:#SendMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>msg</code></td>
            <td>
                <code><a class='link' href='../fuchsia.telephony.snoop/index.html#Message'>Message</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### QmiMessage {:#QmiMessage}
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
                <code><a class='link' href='../fuchsia.telephony.snoop/index.html#Direction'>Direction</a></code>
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

### Direction {:#Direction}
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

### Message {:#Message}
*Defined in [fuchsia.telephony.snoop/tel-snoop.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-telephony-snoop/tel-snoop.fidl#22)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>qmi_message</code></td>
            <td>
                <code><a class='link' href='../fuchsia.telephony.snoop/index.html#QmiMessage'>QmiMessage</a></code>
            </td>
            <td></td>
        </tr></table>







