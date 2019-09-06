Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.icmp


## **PROTOCOLS**

## Provider {:#Provider}
*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-icmp/echo.fidl#35)*

 Provides clients access to ICMP echo sockets through EchoSockets.

### OpenEchoSocket {:#OpenEchoSocket}

 Open an ICMP socket soley for sending ICMP echo requests and receiving
 ICMP echo replies. A protocol request `socket` provides an interface to
 the EchoSocket for the new ICMP echo socket.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#EchoSocketConfig'>EchoSocketConfig</a></code>
            </td>
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EchoSocket'>EchoSocket</a>&gt;</code>
            </td>
        </tr></table>



## EchoSocket {:#EchoSocket}
*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-icmp/echo.fidl#49)*

 EchoSocket is a socket that allows sending ICMP echo requests and receiving
 ICMP echo replies.

 Other ICMP operations, such as sending and receiving error messages, are
 handled by the network stack itself and not exposed by this API.

 The OnOpen event will trigger with a status code once opened.

### SendRequest {:#SendRequest}

 Send an ICMP echo request.

 The source address on the packet is chosen purely based on the remote
 address for the time being. The configured local address from
 `EchoSocketConfig` is ignored.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#EchoPacket'>EchoPacket</a></code>
            </td>
        </tr></table>



### Watch {:#Watch}

 Watch for an ICMP echo reply or error. If a reply or error hasn't been
 received yet, block until one arrives; otherwise, return immediately.

 Any incoming echo replies from the configured remote address will be
 received, regardless of their destination address. This is due to the
 ignored local address from `EchoSocketConfig`.

 Returns status:
  - `ADDRESS_UNREACHABLE` when the remote host is unreachable
  - `OUT_OF_RANGE` when the packet is larger than the MTU

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#EchoSocket_Watch_Result'>EchoSocket_Watch_Result</a></code>
            </td>
        </tr></table>

### OnOpen {:#OnOpen}

 Triggers when the socket opens. Indicates the success or failure of the
 open operation.

 Returns status `INVALID_ARUGMENT` when the `local` and `remote` IP
 addresses do not match IP versions.



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

### EchoSocket_Watch_Response {:#EchoSocket_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reply</code></td>
            <td>
                <code><a class='link' href='#EchoPacket'>EchoPacket</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EchoPacket {:#EchoPacket}
*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-icmp/echo.fidl#79)*



 EchoPacket specifies ICMP fields for an echo request or reply. IP fields
 are set and verified upon `OpenEchoSocket`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sequence_num</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> Sequence numbers are used to match requests and replies.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> The payload can be of arbitrary length and content. The size, including IP
 and ICMP headers, must be less than the Maximum Transmission Limit (MTU)
 of the network to avoid being fragmented.
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### EchoSocketConfig {:#EchoSocketConfig}


*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-icmp/echo.fidl#11)*

 Configuration for an ICMP echo socket.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>local</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td> Local IPv4 or IPv6 address used as the source for ICMP echo requests
 sent through this EchoSocket.

 This field is currently ignored and has no effect, but may have an
 effect in the future for source-based routing. It is highly encouraged
 to specify this field, if possible.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td> Remote IPv4 or IPv6 address used as the destination for ICMP echo
 requests sent through this EchoSocket.

 The version of IP used for `remote` needs to match the version used
 by `source`. If this criterion is not met, an `EchoSocket.OnOpen` event
 will be sent with status `INVALID_ARGUMENT`.

 In other words, `source` and `remote` can either both be IPv4 or IPv6.
 Having `source` as IPv4 and `remote` as IPv6, or vice versa, will result
 in error.
</td>
        </tr></table>



## **UNIONS**

### EchoSocket_Watch_Result {:#EchoSocket_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#EchoSocket_Watch_Response'>EchoSocket_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







