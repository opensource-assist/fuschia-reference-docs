Project: /_project.yaml
Book: /_book.yaml

# fuchsia.overnet.streamlinkfuzzer




## **STRUCTS**

### UntrustedInputPlan {:#UntrustedInputPlan}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#9)*



 A list of packets to process on a stream link
 For stream_link_untrusted_fuzzer


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>link_description</code></td>
            <td>
                <code><a class='link' href='#UntrustedLinkDescription'>UntrustedLinkDescription</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UntrustedReliableLink {:#UntrustedReliableLink}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### UntrustedUnreliableLink {:#UntrustedUnreliableLink}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerToPeerPlan {:#PeerToPeerPlan}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#26)*



 A list of actions to perform on a peer to peer fixture
 For stream_link_peer_to_peer_fuzzer


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>link_description</code></td>
            <td>
                <code><a class='link' href='#PeerToPeerLinkDescription'>PeerToPeerLinkDescription</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PeerToPeerAction'>PeerToPeerAction</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PeerToPeerAction {:#PeerToPeerAction}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#38)*



 An action in a peer to peer test


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node</code></td>
            <td>
                <code><a class='link' href='#NodeId'>NodeId</a></code>
            </td>
            <td> Which node performs the action
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#PeerToPeerActionType'>PeerToPeerActionType</a></code>
            </td>
            <td> The action to perform
</td>
            <td>No default</td>
        </tr>
</table>

### Void {:#Void}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#46)*



 Helper empty type for union below


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerToPeerReliableLink {:#PeerToPeerReliableLink}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#58)*



 A reliable link: uses the ReliableFramer class


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerToPeerUnreliableLink {:#PeerToPeerUnreliableLink}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#62)*



 An unreliable link: uses the UnreliableFramer class
 and additionally has a mutation plan to modify bytes on the wire


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mutation_plan_1_to_2</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StreamMutation'>StreamMutation</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mutation_plan_2_to_1</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StreamMutation'>StreamMutation</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InsertByte {:#InsertByte}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#79)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>byte</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### NodeId {:#NodeId}
Type: <code>uint8</code>

*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#32)*

 Which node does an action apply to


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>A</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>B</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>







## **XUNIONS**

### UntrustedLinkDescription {:#UntrustedLinkDescription}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#19)*

 A description of a link between nodes

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>reliable</code></td>
            <td>
                <code><a class='link' href='#UntrustedReliableLink'>UntrustedReliableLink</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unreliable</code></td>
            <td>
                <code><a class='link' href='#UntrustedUnreliableLink'>UntrustedUnreliableLink</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerToPeerActionType {:#PeerToPeerActionType}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#48)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>send_packet</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td> Request to send a packet from node --> the other node
</td>
        </tr><tr>
            <td><code>sent_packet</code></td>
            <td>
                <code><a class='link' href='#Void'>Void</a></code>
            </td>
            <td> Acknowledge a prior send_packet request on node
</td>
        </tr><tr>
            <td><code>allow_bytes</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Allow this many bytes to flow from node --> the other node
</td>
        </tr></table>

### PeerToPeerLinkDescription {:#PeerToPeerLinkDescription}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#68)*

 A description of a link between nodes

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>reliable</code></td>
            <td>
                <code><a class='link' href='#PeerToPeerReliableLink'>PeerToPeerReliableLink</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unreliable</code></td>
            <td>
                <code><a class='link' href='#PeerToPeerUnreliableLink'>PeerToPeerUnreliableLink</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamMutation {:#StreamMutation}
*Defined in [fuchsia.overnet.streamlinkfuzzer/stream_link_fuzzer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/overnet/deprecated/lib/links/stream_link_fuzzer.test.fidl#74)*

 Describes a mutation to apply to a data stream

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>flip_bit</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> bit[flip_bit] ^= 1
</td>
        </tr></table>





