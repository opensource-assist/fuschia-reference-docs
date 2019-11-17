[TOC]

# fuchsia.net.icmp


## **PROTOCOLS**

## Provider {#Provider}
*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.icmp/echo.fidl#35)*

<p>Provides clients access to ICMP echo sockets through EchoSockets.</p>

### OpenEchoSocket {#OpenEchoSocket}

<p>Open an ICMP socket soley for sending ICMP echo requests and receiving
ICMP echo replies. A protocol request <code>socket</code> provides an interface to
the EchoSocket for the new ICMP echo socket.</p>

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



## EchoSocket {#EchoSocket}
*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.icmp/echo.fidl#49)*

<p>EchoSocket is a socket that allows sending ICMP echo requests and receiving
ICMP echo replies.</p>
<p>Other ICMP operations, such as sending and receiving error messages, are
handled by the network stack itself and not exposed by this API.</p>
<p>The OnOpen event will trigger with a status code once opened.</p>

### SendRequest {#SendRequest}

<p>Send an ICMP echo request.</p>
<p>The source address on the packet is chosen purely based on the remote
address for the time being. The configured local address from
<code>EchoSocketConfig</code> is ignored.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#EchoPacket'>EchoPacket</a></code>
            </td>
        </tr></table>



### Watch {#Watch}

<p>Watch for an ICMP echo reply or error. If a reply or error hasn't been
received yet, block until one arrives; otherwise, return immediately.</p>
<p>Any incoming echo replies from the configured remote address will be
received, regardless of their destination address. This is due to the
ignored local address from <code>EchoSocketConfig</code>.</p>
<p>Returns status:</p>
<ul>
<li><code>ADDRESS_UNREACHABLE</code> when the remote host is unreachable</li>
<li><code>OUT_OF_RANGE</code> when the packet is larger than the MTU</li>
</ul>

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

### OnOpen {#OnOpen}

<p>Triggers when the socket opens. Indicates the success or failure of the
open operation.</p>
<p>Returns status <code>INVALID_ARUGMENT</code> when the <code>local</code> and <code>remote</code> IP
addresses do not match IP versions.</p>



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

### EchoSocket_Watch_Response {#EchoSocket_Watch_Response}
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

### EchoPacket {#EchoPacket}
*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.icmp/echo.fidl#79)*



<p>EchoPacket specifies ICMP fields for an echo request or reply. IP fields
are set and verified upon <code>OpenEchoSocket</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sequence_num</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Sequence numbers are used to match requests and replies.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The payload can be of arbitrary length and content. The size, including IP
and ICMP headers, must be less than the Maximum Transmission Limit (MTU)
of the network to avoid being fragmented.</p>
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### EchoSocketConfig {#EchoSocketConfig}


*Defined in [fuchsia.net.icmp/echo.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.icmp/echo.fidl#11)*

<p>Configuration for an ICMP echo socket.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>local</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td><p>Local IPv4 or IPv6 address used as the source for ICMP echo requests
sent through this EchoSocket.</p>
<p>This field is currently ignored and has no effect, but may have an
effect in the future for source-based routing. It is highly encouraged
to specify this field, if possible.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>remote</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td><p>Remote IPv4 or IPv6 address used as the destination for ICMP echo
requests sent through this EchoSocket.</p>
<p>The version of IP used for <code>remote</code> needs to match the version used
by <code>source</code>. If this criterion is not met, an <code>EchoSocket.OnOpen</code> event
will be sent with status <code>INVALID_ARGUMENT</code>.</p>
<p>In other words, <code>source</code> and <code>remote</code> can either both be IPv4 or IPv6.
Having <code>source</code> as IPv4 and <code>remote</code> as IPv6, or vice versa, will result
in error.</p>
</td>
        </tr></table>



## **UNIONS**

### EchoSocket_Watch_Result {#EchoSocket_Watch_Result}
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







