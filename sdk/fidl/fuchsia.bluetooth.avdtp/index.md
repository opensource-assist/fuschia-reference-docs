Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.avdtp


## **PROTOCOLS**

## PeerManager {:#PeerManager}
*Defined in [fuchsia.bluetooth.avdtp/avdtp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avdtp/avdtp.fidl#11)*

 Control service for an AVDTP Peer.

### GetPeer {:#GetPeer}

 Connects to the server specified by a `peer_id`.
 On success, `handle` will be used for initiating PeerController procedures.
 On peer disconnect, the handle will be dropped and closed on the server side.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#PeerId'>PeerId</a></code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>request&lt;<a class='link' href='#PeerController'>PeerController</a>&gt;</code>
            </td>
        </tr></table>



### ConnectedPeers {:#ConnectedPeers}

 Returns the `bt.PeerId` of each currently connected peer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_ids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#PeerId'>PeerId</a>&gt;[8]</code>
            </td>
        </tr></table>

### OnPeerConnected {:#OnPeerConnected}

 Incoming connection events from the AVDTP peer.
 Returns the <a class='link' href='#fuchsia.bluetooth..PeerId'>fuchsia.bluetooth..PeerId</a> of the newly connected peer.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#PeerId'>PeerId</a></code>
            </td>
        </tr></table>

## PeerController {:#PeerController}
*Defined in [fuchsia.bluetooth.avdtp/avdtp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avdtp/avdtp.fidl#34)*

 PeerController is an indirect control protocol used for driving the AVDTP library.
 This protocol provides the client with an interface for initiating AVDTP commands
 out of band. To drive end-to-end functionality of AVDTP see
 [bt-profiles](//src/connectivity/bluetooth/profiles).
 * `error PeerError` indicates a procedure failure.
 The current Get(), Set() methods can be interpreted as only initiating an AVDTP procedure.
 The implementation of Get() and Set() methods use generic capabilities and stream information.
 TODO(fxb/36563): Add arguments and responses for Get() and Set() methods to allow the
 client to specify and receive the results of the procedures.

### SetConfiguration {:#SetConfiguration}

 Initiate a stream configuration procedure.
 No configuration information is specified because generic config information will
 be used to initiate the procedure.

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
                <code><a class='link' href='#PeerController_SetConfiguration_Result'>PeerController_SetConfiguration_Result</a></code>
            </td>
        </tr></table>

### GetConfiguration {:#GetConfiguration}

 Initiate a procedure to get the configuration information of the peer stream.
 The result is discarded because PeerController only initiates the procedure.

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
                <code><a class='link' href='#PeerController_GetConfiguration_Result'>PeerController_GetConfiguration_Result</a></code>
            </td>
        </tr></table>

### SuspendStream {:#SuspendStream}

 Initiate a suspend request to the stream.
 This command will not resume nor reconfigure the stream.

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
                <code><a class='link' href='#PeerController_SuspendStream_Result'>PeerController_SuspendStream_Result</a></code>
            </td>
        </tr></table>

### SuspendAndReconfigure {:#SuspendAndReconfigure}

 A "chained" set of procedures on the current stream.
 SuspendStream() followed by ReconfigureStream().
 Reconfigure() configures the stream that is currently open.

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
                <code><a class='link' href='#PeerController_SuspendAndReconfigure_Result'>PeerController_SuspendAndReconfigure_Result</a></code>
            </td>
        </tr></table>

### EstablishStream {:#EstablishStream}

 Initiate stream establishment with the peer.

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
                <code><a class='link' href='#PeerController_EstablishStream_Result'>PeerController_EstablishStream_Result</a></code>
            </td>
        </tr></table>

### ReleaseStream {:#ReleaseStream}

 Release the current stream that is owned by the peer.
 If the streaming channel doesn't exist, no action will be taken.

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
                <code><a class='link' href='#PeerController_ReleaseStream_Result'>PeerController_ReleaseStream_Result</a></code>
            </td>
        </tr></table>

### ReconfigureStream {:#ReconfigureStream}

 Initiate a reconfiguration procedure for the current stream.
 No configuration information is specified because a generic set of config
 information will be used to initiate the procedure.

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
                <code><a class='link' href='#PeerController_ReconfigureStream_Result'>PeerController_ReconfigureStream_Result</a></code>
            </td>
        </tr></table>

### GetCapabilities {:#GetCapabilities}

 Initiate a procedure to get the capabilities of the peer.
 The result is discarded because PeerController only initiates the procedure.

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
                <code><a class='link' href='#PeerController_GetCapabilities_Result'>PeerController_GetCapabilities_Result</a></code>
            </td>
        </tr></table>

### GetAllCapabilities {:#GetAllCapabilities}

 Initiate a procedure to get the capabilities of the peer.
 The result is discarded because PeerController only initiates the procedure.

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
                <code><a class='link' href='#PeerController_GetAllCapabilities_Result'>PeerController_GetAllCapabilities_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### PeerController_SetConfiguration_Response {:#PeerController_SetConfiguration_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_GetConfiguration_Response {:#PeerController_GetConfiguration_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_SuspendStream_Response {:#PeerController_SuspendStream_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_SuspendAndReconfigure_Response {:#PeerController_SuspendAndReconfigure_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_EstablishStream_Response {:#PeerController_EstablishStream_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_ReleaseStream_Response {:#PeerController_ReleaseStream_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_ReconfigureStream_Response {:#PeerController_ReconfigureStream_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_GetCapabilities_Response {:#PeerController_GetCapabilities_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PeerController_GetAllCapabilities_Response {:#PeerController_GetAllCapabilities_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### PeerError {:#PeerError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.avdtp/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avdtp/types.fidl#12)*

 Represents the return status of a <a class='link' href='#fuchsia.bluetooth.avdtp.Peer'>fuchsia.bluetooth.avdtp.Peer</a> method


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN_FAILURE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROTOCOL_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### PeerController_SetConfiguration_Result {:#PeerController_SetConfiguration_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_SetConfiguration_Response'>PeerController_SetConfiguration_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_GetConfiguration_Result {:#PeerController_GetConfiguration_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_GetConfiguration_Response'>PeerController_GetConfiguration_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_SuspendStream_Result {:#PeerController_SuspendStream_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_SuspendStream_Response'>PeerController_SuspendStream_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_SuspendAndReconfigure_Result {:#PeerController_SuspendAndReconfigure_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_SuspendAndReconfigure_Response'>PeerController_SuspendAndReconfigure_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_EstablishStream_Result {:#PeerController_EstablishStream_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_EstablishStream_Response'>PeerController_EstablishStream_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_ReleaseStream_Result {:#PeerController_ReleaseStream_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_ReleaseStream_Response'>PeerController_ReleaseStream_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_ReconfigureStream_Result {:#PeerController_ReconfigureStream_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_ReconfigureStream_Response'>PeerController_ReconfigureStream_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_GetCapabilities_Result {:#PeerController_GetCapabilities_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_GetCapabilities_Response'>PeerController_GetCapabilities_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### PeerController_GetAllCapabilities_Result {:#PeerController_GetAllCapabilities_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerController_GetAllCapabilities_Response'>PeerController_GetAllCapabilities_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeerError'>PeerError</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avdtp/types.fidl#9">MAX_PICONET_SIZE</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maximum number of peers that can be connected to a node.
 (Core Spec 5.0, Vol 2, Part B, Section 1)
</td>
        </tr>
    
</table>

