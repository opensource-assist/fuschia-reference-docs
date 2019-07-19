Project: /_project.yaml
Book: /_book.yaml

# fuchsia.overnet.protocol


## **PROTOCOLS**

## Peer {:#Peer}
*Defined in [fuchsia.overnet.protocol/peer_protocol.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/peer_protocol.fidl#12)*

 Peer-to-peer protocol between two Overnet nodes.
 Each end of the Overnet connection stream implements this protocol.

### ConnectToService {:#ConnectToService}

 Create a new stream, labelled `stream_id`, to communicate with the
 advertised service `service_name`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#StreamId'>StreamId</a></code>
            </td>
        </tr></table>



### Ping {:#Ping}

 Ping request/response. Return value is the amount of time the service
 used to fulfill the response.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### UpdateNodeDescription {:#UpdateNodeDescription}

 Update the description of a single node.
 This message is broadcast from a node whenever the description changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>desc</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#PeerDescription'>PeerDescription</a></code>
            </td>
        </tr></table>



### UpdateNodeStatus {:#UpdateNodeStatus}

 Gossip routing: update the status of a single node.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#NodeStatus'>NodeStatus</a></code>
            </td>
        </tr></table>



### UpdateLinkStatus {:#UpdateLinkStatus}

 Gossip routing: update the status of a single link between nodes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>link</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#LinkStatus'>LinkStatus</a></code>
            </td>
        </tr></table>



## ZirconChannel {:#ZirconChannel}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#46)*

 Proxy protocol for channels.
 This protocol is published for each side of the Overnet stream.

### Message {:#Message}

 Send a message to the stream's peer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>message</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#ZirconChannelMessage'>ZirconChannelMessage</a></code>
            </td>
        </tr></table>



## ZirconSocket {:#ZirconSocket}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#54)*

 Proxy protocol for sockets.
 This protocol is published for each side of the Overnet stream.

### Message {:#Message}

 Send some bytes to the stream's peer.
 For datagram sockets, this is one datagram.
 For stream sockets, this is the next bundle of bytes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### Control {:#Control}

 Send a control message to the stream's peer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### Share {:#Share}

 Share a handle to the stream's peer (to be collected via zx_socket_accept).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>socket</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#SocketHandle'>SocketHandle</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### StreamId {:#StreamId}
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

### NodeId {:#NodeId}
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

### LinkStatus {:#LinkStatus}
*Defined in [fuchsia.overnet.protocol/routing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/routing.fidl#32)*



 Status packet for a single link.
 Traffic on the link flows from `from` to `to`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>from</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
            <td> Link originating node.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>to</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
            <td> Link target node.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> An identifier (chosen by node `from`) to label this link.
 `from` must guarantee that the tuple (from, to, local_id) is unique
 for each of it's held links.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>version</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A monotonically increasing version counter for this links status.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#LinkMetrics'>LinkMetrics</a></code>
            </td>
            <td> Metrics associated with this link.
</td>
            <td>No default</td>
        </tr>
</table>

### NodeStatus {:#NodeStatus}
*Defined in [fuchsia.overnet.protocol/routing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/routing.fidl#55)*



 Status packet for a node.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
            <td> The node to which we refer.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>version</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A monotonically increasing version counter for this nodes status.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#NodeMetrics'>NodeMetrics</a></code>
            </td>
            <td> Metrics associated with this node.
</td>
            <td>No default</td>
        </tr>
</table>

### ZirconChannelMessage {:#ZirconChannelMessage}
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
                <code>vector&lt;<a class='link' href='../fuchsia.overnet.protocol/index.html#ZirconHandle'>ZirconHandle</a>&gt;[64]</code>
            </td>
            <td> Handles part of the payload.
</td>
            <td>No default</td>
        </tr>
</table>

### ChannelHandle {:#ChannelHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#27)*



 A proxied channel.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#StreamId'>StreamId</a></code>
            </td>
            <td> The Overnet proxy stream that was created to carry this channel.
 The protocol over said stream will be a `ZirconChannel`.
</td>
            <td>No default</td>
        </tr>
</table>

### SocketHandle {:#SocketHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#34)*



 A proxied socket.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stream_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#StreamId'>StreamId</a></code>
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

### ReliabilityAndOrdering {:#ReliabilityAndOrdering}
Type: <code>uint32</code>

*Defined in [fuchsia.overnet.protocol/labels.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/labels.fidl#21)*

 Reliability and ordering constraints for a stream.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ReliableOrdered</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UnreliableOrdered</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ReliableUnordered</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>UnreliableUnordered</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>TailReliable</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### PeerDescription {:#PeerDescription}


*Defined in [fuchsia.overnet.protocol/routing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/routing.fidl#12)*

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

### LinkMetrics {:#LinkMetrics}


*Defined in [fuchsia.overnet.protocol/routing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/routing.fidl#19)*

 Metrics associated with a link.
 Note that a link is a uni-directional connection between two nodes.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>bw_link</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> How much bandwidth is currently available across a link (in bits per second).
</td>
        </tr><tr>
            <td>2</td>
            <td><code>bw_used</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> How much bandwidth is currently in use across the link (in bits per second).
</td>
        </tr><tr>
            <td>3</td>
            <td><code>rtt</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Current round trip time for requests across this link.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>mss</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Maximum send size for a datagram across this link.
</td>
        </tr></table>

### NodeMetrics {:#NodeMetrics}


*Defined in [fuchsia.overnet.protocol/routing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/routing.fidl#49)*

 Metrics associated with a node.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>forwarding_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> How long does this node take to forward a message between two links?
</td>
        </tr></table>

### StreamSocketGreeting {:#StreamSocketGreeting}


*Defined in [fuchsia.overnet.protocol/stream_socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/stream_socket.fidl#8)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>magic_string</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>node_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#NodeId'>NodeId</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>local_link_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### ZirconHandle {:#ZirconHandle}
*Defined in [fuchsia.overnet.protocol/zircon_proxy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/zircon_proxy.fidl#19)*

 A single handle to be proxied.
 Not all Zircon types are supported.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>channel</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#ChannelHandle'>ChannelHandle</a></code>
            </td>
            <td> A proxied channel.
</td>
        </tr><tr>
            <td><code>socket</code></td>
            <td>
                <code><a class='link' href='../fuchsia.overnet.protocol/index.html#SocketHandle'>SocketHandle</a></code>
            </td>
            <td> A proxied socket.
</td>
        </tr></table>





## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.overnet.protocol/routing.fidl#9">METRIC_VERSION_TOMBSTONE</a></td>
            <td>
                    <code>18446744073709551615</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    
</table>

