[TOC]

# fuchsia.overnet.protocol


## **PROTOCOLS**

## Diagnostic {#Diagnostic}
*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#127)*

 Diagnostic information exported by Overnet peers.
 This interface is additionally exported to the Overnet mesh.

### Probe {#Probe}

 Probe some basic statistics from this node

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



 Identifies a single overnet stream between two processes on the Overnet mesh


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



 Address of a node on the overlay network.


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
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### UpdateLinkStatus {#UpdateLinkStatus}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#35)*



 Update status of all links starting from a given node
 By bundling all link updates together, we guarantee:
  - a simple protocol that can deal with updates, additions, and deletions to the link set
  - no routing decisions based on partial information from any one node


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>link_status</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LinkStatus'>LinkStatus</a>&gt;</code>
            </td>
            <td> Status of all active links originating at the sending node
</td>
            <td>No default</td>
        </tr>
</table>

### ConnectToService {#ConnectToService}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#42)*



 Create a new stream, labelled `stream_id`, to communicate with the
 advertised service `service_name`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service_name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td> Which service to connect to.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> On which quic stream will this service connection be formed.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectToServiceOptions'>ConnectToServiceOptions</a></code>
            </td>
            <td> Ancillary options for this connection.
</td>
            <td>No default</td>
        </tr>
</table>

### LinkStatus {#LinkStatus}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#70)*



 Status packet for a single link. A link is a unidirectional connection between two peers,
 and is owned by the first peer. The target node is identified by `to`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>to</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td> Link target node.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> An identifier (chosen by the link owner) to label this link.
 The link owner must guarantee that the tuple (to, local_id) is unique for each of it's held
 links.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code><a class='link' href='#LinkMetrics'>LinkMetrics</a></code>
            </td>
            <td> Metrics associated with this link.
</td>
            <td>No default</td>
        </tr>
</table>

### ZirconChannelMessage {#ZirconChannelMessage}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#10)*



 A single message proxied from a Zircon channel over an Overnet stream.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;[65536]</code>
            </td>
            <td> Bytes part of the payload.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ZirconHandle'>ZirconHandle</a>&gt;[64]</code>
            </td>
            <td> Handles part of the payload.
</td>
            <td>No default</td>
        </tr>
</table>

### ChannelHandle {#ChannelHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#27)*



 A proxied channel.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code><a class='link' href='#StreamId'>StreamId</a></code>
            </td>
            <td> The Overnet proxy stream that was created to carry this channel.
 The protocol over said stream will be a `ZirconChannel`.
</td>
            <td>No default</td>
        </tr>
</table>

### SocketHandle {#SocketHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#34)*



 A proxied socket.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code><a class='link' href='#StreamId'>StreamId</a></code>
            </td>
            <td> The Overnet proxy stream that was created to carry this socket.
 The protocol over said stream will be a `ZirconSocket`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Socket options, per `zx_socket_create`.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### OperatingSystem {#OperatingSystem}
Type: <code>uint32</code>

*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#74)*

 The operating system running a node.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FUCHSIA</code></td>
            <td><code>0</code></td>
            <td> Fuchsia
</td>
        </tr><tr>
            <td><code>LINUX</code></td>
            <td><code>1</code></td>
            <td> Linux
</td>
        </tr><tr>
            <td><code>MAC</code></td>
            <td><code>2</code></td>
            <td> MacOS
</td>
        </tr></table>

### Implementation {#Implementation}
Type: <code>uint32</code>

*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#84)*

 The implementation of a node that's running.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNIT_TEST</code></td>
            <td><code>0</code></td>
            <td> Some unit test... shouldn't be seen in the wild.
</td>
        </tr><tr>
            <td><code>OVERNET_STACK</code></td>
            <td><code>1</code></td>
            <td> The overnetstack daemon on Fuchsia.
</td>
        </tr><tr>
            <td><code>ASCENDD</code></td>
            <td><code>2</code></td>
            <td> The non-Fuchsia routing daemon Ascendd.
</td>
        </tr><tr>
            <td><code>HOIST_RUST_CRATE</code></td>
            <td><code>3</code></td>
            <td> The `hoist` Rust crate embedding Overnet.
</td>
        </tr></table>



## **TABLES**

### PeerConnectionDiagnosticInfo {#PeerConnectionDiagnosticInfo}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#8)*

 Diagnostic data on a single peer connection.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td> Source address.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>destination</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td> Destination address.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>is_client</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether this connection is a client.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>is_established</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if the connection established and ready to send traffic.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>received_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of packets received.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>sent_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of packets sent.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>lost_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of packets lost.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>round_trip_time_microseconds</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Round trip time for the connection in microseconds.
</td>
        </tr><tr>
            <td>9</td>
            <td><code>congestion_window_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Current congestion window in bytes.
</td>
        </tr><tr>
            <td>10</td>
            <td><code>messages_sent</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of overnet messages sent.
</td>
        </tr><tr>
            <td>11</td>
            <td><code>bytes_sent</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of bytes sent due to overnet messages.
</td>
        </tr><tr>
            <td>12</td>
            <td><code>connect_to_service_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of connect to service requests.
</td>
        </tr><tr>
            <td>13</td>
            <td><code>connect_to_service_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of bytes sent due to connect to service requests.
</td>
        </tr><tr>
            <td>14</td>
            <td><code>update_node_description_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of node description updates.
</td>
        </tr><tr>
            <td>15</td>
            <td><code>update_node_description_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of bytes sent due to node description updates.
</td>
        </tr><tr>
            <td>16</td>
            <td><code>update_link_status_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of link status updates.
</td>
        </tr><tr>
            <td>17</td>
            <td><code>update_link_status_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of bytes sent due to link status updates.
</td>
        </tr><tr>
            <td>18</td>
            <td><code>update_link_status_ack_sends</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of link status update acknowledgements sent.
</td>
        </tr><tr>
            <td>19</td>
            <td><code>update_link_status_ack_send_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of bytes sent due to link status update acknowledgements.
</td>
        </tr></table>

### LinkDiagnosticInfo {#LinkDiagnosticInfo}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#50)*

 Diagnostic data on a single link.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td> Source address.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>destination</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td> Destination address.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>source_local_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Source identifier for this link.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>received_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of packets received.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>sent_packets</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of packets sent.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>received_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of bytes received.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>sent_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of bytes sent.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>round_trip_time_microseconds</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Round trip time for the connection in microseconds.
</td>
        </tr><tr>
            <td>9</td>
            <td><code>pings_sent</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of ping requests sent.
</td>
        </tr><tr>
            <td>10</td>
            <td><code>packets_forwarded</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Number of packets forwarded.
</td>
        </tr></table>

### NodeDescription {#NodeDescription}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#96)*

 Diagnostic data on a single node.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>operating_system</code></td>
            <td>
                <code><a class='link' href='#OperatingSystem'>OperatingSystem</a></code>
            </td>
            <td> A string saying something about what operating system this node is running on
 Currently used: 'fuchsia', 'linux', 'mac'
</td>
        </tr><tr>
            <td>2</td>
            <td><code>implementation</code></td>
            <td>
                <code><a class='link' href='#Implementation'>Implementation</a></code>
            </td>
            <td> A string saying something about the runtime environment of a node
</td>
        </tr></table>

### ProbeResult {#ProbeResult}


*Defined in [fuchsia.overnet.protocol/diagnostic.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/diagnostic.fidl#105)*

 Composition of results from Diagnostic/Probe.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_description</code></td>
            <td>
                <code><a class='link' href='#NodeDescription'>NodeDescription</a></code>
            </td>
            <td> Node description, obtained by probing ProbeSelector.NODE_DESCRIPTION
</td>
        </tr><tr>
            <td>2</td>
            <td><code>peer_connections</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PeerConnectionDiagnosticInfo'>PeerConnectionDiagnosticInfo</a>&gt;</code>
            </td>
            <td> Peer connections list, obtained by probing ProbeSelector.PEER_CONNECTIONS
</td>
        </tr><tr>
            <td>3</td>
            <td><code>links</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LinkDiagnosticInfo'>LinkDiagnosticInfo</a>&gt;</code>
            </td>
            <td> Link list, obtained by probing ProbeSelector.LINKS
</td>
        </tr></table>

### ConnectToServiceOptions {#ConnectToServiceOptions}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#52)*

 Options for service connection formation.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### PeerDescription {#PeerDescription}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#56)*

 Description of a single node.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> The set of services published by this node.
</td>
        </tr></table>

### LinkMetrics {#LinkMetrics}


*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#63)*

 Metrics associated with a link.
 Note that a link is a uni-directional connection between two nodes.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>round_trip_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Current round trip time for requests across this link in microseconds.
</td>
        </tr></table>

### StreamSocketGreeting {#StreamSocketGreeting}


*Defined in [fuchsia.overnet.protocol/stream_socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/stream_socket.fidl#8)*

 Introduction packet sent on stream oriented links between Overnet nodes


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>magic_string</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td> Protocol identification string; different kinds of streams might choose a different value here
</td>
        </tr><tr>
            <td>2</td>
            <td><code>node_id</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td> Overnet NodeId of the sender
</td>
        </tr><tr>
            <td>3</td>
            <td><code>connection_label</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td> Optional label for debugging
</td>
        </tr></table>





## **XUNIONS**

### PeerMessage {#PeerMessage}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#12)*

 Peer-to-peer protocol between two Overnet nodes.
 Client quic connections send this xunion to servers over quic stream 0.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>connect_to_service</code></td>
            <td>
                <code><a class='link' href='#ConnectToService'>ConnectToService</a></code>
            </td>
            <td> Request to create a channel to a service exported by this peer.
</td>
        </tr><tr>
            <td><code>update_node_description</code></td>
            <td>
                <code><a class='link' href='#PeerDescription'>PeerDescription</a></code>
            </td>
            <td> Update this peers description on the server.
</td>
        </tr><tr>
            <td><code>update_link_status</code></td>
            <td>
                <code><a class='link' href='#UpdateLinkStatus'>UpdateLinkStatus</a></code>
            </td>
            <td> Update information about a link that this peer knows about on the
 remote peer.
</td>
        </tr></table>

### PeerReply {#PeerReply}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#23)*

 Reply messages for PeerMessage, where appropriate

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>update_link_status_ack</code></td>
            <td>
                <code><a class='link' href='#Empty'>Empty</a></code>
            </td>
            <td> Acknowledge an UpdateLinkStatus message
</td>
        </tr></table>

### ZirconHandle {#ZirconHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#19)*

 A single handle to be proxied.
 Not all Zircon types are supported.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>channel</code></td>
            <td>
                <code><a class='link' href='#ChannelHandle'>ChannelHandle</a></code>
            </td>
            <td> A proxied channel.
</td>
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code><a class='link' href='#SocketHandle'>SocketHandle</a></code>
            </td>
            <td> A proxied socket.
</td>
        </tr></table>



## **BITS**

### ProbeSelector {#ProbeSelector}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>NODE_DESCRIPTION</td>
            <td>1</td>
            <td> Request ProbeResult.node_description is present in the result
</td>
        </tr><tr>
            <td>PEER_CONNECTIONS</td>
            <td>2</td>
            <td> Request ProbeResult.peer_connections is present in the result
</td>
        </tr><tr>
            <td>LINKS</td>
            <td>4</td>
            <td> Request ProbeResult.links is present in the result
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#8">MAX_SERVICE_NAME_LENGTH</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>

