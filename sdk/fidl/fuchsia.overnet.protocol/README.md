[TOC]

# fuchsia.overnet.protocol


## **PROTOCOLS**

## Diagnostic {#Diagnostic}
*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#127)*

<p>Diagnostic information exported by Overnet peers.
This interface is additionally exported to the Overnet mesh.</p>

### Probe {#Probe}

<p>Probe some basic statistics from this node</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>selector</code></td>
            <td>
                <code><a class='link' href='#ProbeSelector'>ProbeSelector</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ProbeResult'>ProbeResult</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### StreamId {#StreamId}
*Defined in [fuchsia.overnet.protocol/labels.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/labels.fidl#8)*



<p>Identifies a single overnet stream between two processes on the Overnet mesh</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NodeId {#NodeId}
*Defined in [fuchsia.overnet.protocol/labels.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/labels.fidl#13)*



<p>Address of a node on the overlay network.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Empty {#Empty}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### UpdateLinkStatus {#UpdateLinkStatus}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#45)*



<p>Update status of all links starting from a given node
By bundling all link updates together, we guarantee:</p>
<ul>
<li>a simple protocol that can deal with updates, additions, and deletions to the link set</li>
<li>no routing decisions based on partial information from any one node</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>link_status</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LinkStatus'>LinkStatus</a>&gt;</code>
            </td>
            <td><p>Status of all active links originating at the sending node</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ConnectToService {#ConnectToService}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#52)*



<p>Create a new stream, labelled <code>stream_id</code>, to communicate with the
advertised service <code>service_name</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td><p>Which service to connect to.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>On which quic stream will this service connection be formed.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectToServiceOptions'>ConnectToServiceOptions</a></code>
            </td>
            <td><p>Ancillary options for this connection.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### LinkStatus {#LinkStatus}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#80)*



<p>Status packet for a single link. A link is a unidirectional connection between two peers,
and is owned by the first peer. The target node is identified by <code>to</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>to</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td><p>Link target node.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_id</code></td>
            <td>
                <code><a class='link' href='#LinkId'>LinkId</a></code>
            </td>
            <td><p>An identifier (chosen by the link owner) to label this link.
The link owner must guarantee that the tuple (to, local_id) is unique for each of it's held
links.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code><a class='link' href='#LinkMetrics'>LinkMetrics</a></code>
            </td>
            <td><p>Metrics associated with this link.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ZirconChannelMessage {#ZirconChannelMessage}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#10)*



<p>A single message proxied from a Zircon channel over an Overnet stream.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;[65536]</code>
            </td>
            <td><p>Bytes part of the payload.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ZirconHandle'>ZirconHandle</a>&gt;[64]</code>
            </td>
            <td><p>Handles part of the payload.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ChannelHandle {#ChannelHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#27)*



<p>A proxied channel.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code><a class='link' href='#StreamId'>StreamId</a></code>
            </td>
            <td><p>The Overnet proxy stream that was created to carry this channel.
The protocol over said stream will be a <code>ZirconChannel</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### SocketHandle {#SocketHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#34)*



<p>A proxied socket.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code><a class='link' href='#StreamId'>StreamId</a></code>
            </td>
            <td><p>The Overnet proxy stream that was created to carry this socket.
The protocol over said stream will be a <code>ZirconSocket</code>.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Socket options, per <code>zx_socket_create</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### OperatingSystem {#OperatingSystem}
Type: <code>uint32</code>

*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#74)*

<p>The operating system running a node.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FUCHSIA</code></td>
            <td><code>0</code></td>
            <td><p>Fuchsia</p>
</td>
        </tr><tr>
            <td><code>LINUX</code></td>
            <td><code>1</code></td>
            <td><p>Linux</p>
</td>
        </tr><tr>
            <td><code>MAC</code></td>
            <td><code>2</code></td>
            <td><p>MacOS</p>
</td>
        </tr></table>

### Implementation {#Implementation}
Type: <code>uint32</code>

*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#84)*

<p>The implementation of a node that's running.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNIT_TEST</code></td>
            <td><code>0</code></td>
            <td><p>Some unit test... shouldn't be seen in the wild.</p>
</td>
        </tr><tr>
            <td><code>OVERNET_STACK</code></td>
            <td><code>1</code></td>
            <td><p>The overnetstack daemon on Fuchsia.</p>
</td>
        </tr><tr>
            <td><code>ASCENDD</code></td>
            <td><code>2</code></td>
            <td><p>The non-Fuchsia routing daemon Ascendd.</p>
</td>
        </tr><tr>
            <td><code>HOIST_RUST_CRATE</code></td>
            <td><code>3</code></td>
            <td><p>The <code>hoist</code> Rust crate embedding Overnet.</p>
</td>
        </tr></table>



## **TABLES**

### PeerConnectionDiagnosticInfo {#PeerConnectionDiagnosticInfo}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#8)*

<p>Diagnostic data on a single peer connection.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td><p>Source address.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>destination</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td><p>Destination address.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>is_client</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether this connection is a client.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>is_established</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if the connection established and ready to send traffic.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>received_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of packets received.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>sent_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of packets sent.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>lost_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of packets lost.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>round_trip_time_microseconds</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Round trip time for the connection in microseconds.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>congestion_window_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Current congestion window in bytes.</p>
</td>
        </tr><tr>
            <td>10</td>
            <td><code>messages_sent</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of overnet messages sent.</p>
</td>
        </tr><tr>
            <td>11</td>
            <td><code>bytes_sent</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of bytes sent due to overnet messages.</p>
</td>
        </tr><tr>
            <td>12</td>
            <td><code>connect_to_service_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of connect to service requests.</p>
</td>
        </tr><tr>
            <td>13</td>
            <td><code>connect_to_service_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of bytes sent due to connect to service requests.</p>
</td>
        </tr><tr>
            <td>14</td>
            <td><code>update_node_description_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of node description updates.</p>
</td>
        </tr><tr>
            <td>15</td>
            <td><code>update_node_description_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of bytes sent due to node description updates.</p>
</td>
        </tr><tr>
            <td>16</td>
            <td><code>update_link_status_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of link status updates.</p>
</td>
        </tr><tr>
            <td>17</td>
            <td><code>update_link_status_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of bytes sent due to link status updates.</p>
</td>
        </tr><tr>
            <td>18</td>
            <td><code>update_link_status_ack_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of link status update acknowledgements sent.</p>
</td>
        </tr><tr>
            <td>19</td>
            <td><code>update_link_status_ack_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of bytes sent due to link status update acknowledgements.</p>
</td>
        </tr></table>

### LinkDiagnosticInfo {#LinkDiagnosticInfo}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#50)*

<p>Diagnostic data on a single link.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td><p>Source address.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>destination</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td><p>Destination address.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>source_local_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Source identifier for this link.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>received_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of packets received.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>sent_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of packets sent.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>received_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of bytes received.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>sent_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of bytes sent.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>round_trip_time_microseconds</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Round trip time for the connection in microseconds.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>pings_sent</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of ping requests sent.</p>
</td>
        </tr><tr>
            <td>10</td>
            <td><code>packets_forwarded</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Number of packets forwarded.</p>
</td>
        </tr></table>

### NodeDescription {#NodeDescription}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#96)*

<p>Diagnostic data on a single node.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>operating_system</code></td>
            <td>
                <code><a class='link' href='#OperatingSystem'>OperatingSystem</a></code>
            </td>
            <td><p>A string saying something about what operating system this node is running on
Currently used: 'fuchsia', 'linux', 'mac'</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>implementation</code></td>
            <td>
                <code><a class='link' href='#Implementation'>Implementation</a></code>
            </td>
            <td><p>A string saying something about the runtime environment of a node</p>
</td>
        </tr></table>

### ProbeResult {#ProbeResult}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#105)*

<p>Composition of results from Diagnostic/Probe.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_description</code></td>
            <td>
                <code><a class='link' href='#NodeDescription'>NodeDescription</a></code>
            </td>
            <td><p>Node description, obtained by probing ProbeSelector.NODE_DESCRIPTION</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>peer_connections</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PeerConnectionDiagnosticInfo'>PeerConnectionDiagnosticInfo</a>&gt;</code>
            </td>
            <td><p>Peer connections list, obtained by probing ProbeSelector.PEER_CONNECTIONS</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>links</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LinkDiagnosticInfo'>LinkDiagnosticInfo</a>&gt;</code>
            </td>
            <td><p>Link list, obtained by probing ProbeSelector.LINKS</p>
</td>
        </tr></table>

### ConfigRequest {#ConfigRequest}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#23)*

<p>Overall connection configuration request</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### ConfigResponse {#ConfigResponse}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#28)*

<p>Overall connection configuration response - sent as the first response message
on the connection stream.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### ConnectToServiceOptions {#ConnectToServiceOptions}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#62)*

<p>Options for service connection formation.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### PeerDescription {#PeerDescription}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#66)*

<p>Description of a single node.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The set of services published by this node.</p>
</td>
        </tr></table>

### LinkMetrics {#LinkMetrics}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#73)*

<p>Metrics associated with a link.
Note that a link is a uni-directional connection between two nodes.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>round_trip_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Current round trip time for requests across this link in microseconds.</p>
</td>
        </tr></table>

### StreamSocketGreeting {#StreamSocketGreeting}


*Defined in [fuchsia.overnet.protocol/stream_socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/stream_socket.fidl#8)*

<p>Introduction packet sent on stream oriented links between Overnet nodes</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>magic_string</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td><p>Protocol identification string; different kinds of streams might choose a different value here</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>node_id</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td><p>Overnet NodeId of the sender</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>connection_label</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td><p>Optional label for debugging</p>
</td>
        </tr></table>





## **XUNIONS**

### PeerMessage {#PeerMessage}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#12)*

<p>Peer-to-peer protocol between two Overnet nodes.
Client quic connections send this xunion to servers over quic stream 0.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>connect_to_service</code></td>
            <td>
                <code><a class='link' href='#ConnectToService'>ConnectToService</a></code>
            </td>
            <td><p>Request to create a channel to a service exported by this peer.</p>
</td>
        </tr><tr>
            <td><code>update_node_description</code></td>
            <td>
                <code><a class='link' href='#PeerDescription'>PeerDescription</a></code>
            </td>
            <td><p>Update this peers description on the server.</p>
</td>
        </tr><tr>
            <td><code>update_link_status</code></td>
            <td>
                <code><a class='link' href='#UpdateLinkStatus'>UpdateLinkStatus</a></code>
            </td>
            <td><p>Update information about a link that this peer knows about on the
remote peer.</p>
</td>
        </tr></table>

### PeerReply {#PeerReply}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#33)*

<p>Reply messages for PeerMessage, where appropriate.
The ConfigResponse message must have been sent already.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>update_link_status_ack</code></td>
            <td>
                <code><a class='link' href='#Empty'>Empty</a></code>
            </td>
            <td><p>Acknowledge an UpdateLinkStatus message</p>
</td>
        </tr></table>

### ZirconHandle {#ZirconHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#19)*

<p>A single handle to be proxied.
Not all Zircon types are supported.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>channel</code></td>
            <td>
                <code><a class='link' href='#ChannelHandle'>ChannelHandle</a></code>
            </td>
            <td><p>A proxied channel.</p>
</td>
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code><a class='link' href='#SocketHandle'>SocketHandle</a></code>
            </td>
            <td><p>A proxied socket.</p>
</td>
        </tr></table>



## **BITS**

### ProbeSelector {#ProbeSelector}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>NODE_DESCRIPTION</td>
            <td>1</td>
            <td><p>Request ProbeResult.node_description is present in the result</p>
</td>
        </tr><tr>
            <td>PEER_CONNECTIONS</td>
            <td>2</td>
            <td><p>Request ProbeResult.peer_connections is present in the result</p>
</td>
        </tr><tr>
            <td>LINKS</td>
            <td>4</td>
            <td><p>Request ProbeResult.links is present in the result</p>
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_SERVICE_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#8">MAX_SERVICE_NAME_LENGTH</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="LinkId">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/labels.fidl#18">LinkId</a></td>
            <td>
                <code>uint64</code></td>
            <td><p>Node-local link label</p>
</td>
        </tr></table>

