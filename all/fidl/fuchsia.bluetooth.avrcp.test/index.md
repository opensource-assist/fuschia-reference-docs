Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.avrcp.test


## **PROTOCOLS**

## PeerManagerExt {:#PeerManagerExt}
*Defined in [fuchsia.bluetooth.avrcp.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp.test/test.fidl#11)*


### GetControllerForTarget {:#GetControllerForTarget}

 Returns a test controller client to a remote target service at the peer specified by
 `peer_id`. This client is to be used alongside the primary controller client.
 The test protocol provides additional methods not exposed by primary controller protocol
 that are designed to be used for PTS qualification testing and debugging purposes only.
 WARNING: This test controller can cause breaking side-effects for other controller clients
 connected to this the same peer. Use with caution and avoid having additional primary
 controller clients interacting with the same remote peer while using the test controller.
 TODO (BT-305): change peer_id to fuchsia.bluetooth.PeerId type after BrEdr profile service
 switches.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>client</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ControllerExt'>ControllerExt</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#PeerManagerExt_GetControllerForTarget_Result'>PeerManagerExt_GetControllerForTarget_Result</a></code>
            </td>
        </tr></table>

### RegisterIncomingTargetHandler {:#RegisterIncomingTargetHandler}

 Sets an implementation of target handler that will vend delegates for each incoming
 remote TG -> local CT connections to handle the commands being sent by the remote TG.
 If no target handler is set, a default handler will be used internally that will
 dispatch to the MediaSession service. This should only be used for PTS qualification testing
 and debugging purposes only.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handler</code></td>
            <td>
                <code><a class='link' href='#TargetHandler'>TargetHandler</a></code>
            </td>
        </tr></table>



## TargetHandler {:#TargetHandler}
*Defined in [fuchsia.bluetooth.avrcp.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp.test/test.fidl#33)*

 An implementation of this interface is registered with the TestPeerManager service to handle
 incoming connections.

### OnControllerConnected {:#OnControllerConnected}

 Called when an incoming target is connected. `delegate` should be fulfilled with an
 interface that will be used to handle commands from the connected Controller.
 TODO (BT-305): change peer_id to fuchsia.bluetooth.PeerId type after BrEdr profile service
 switches.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>delegate</code></td>
            <td>
                <code>request&lt;<a class='link' href='#TargetDelegate'>TargetDelegate</a>&gt;</code>
            </td>
        </tr></table>



## TargetDelegate {:#TargetDelegate}
*Defined in [fuchsia.bluetooth.avrcp.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp.test/test.fidl#55)*

 Returned by an implementer of the TargetHandler interface.
 Handles incoming connection commands by a remote CT device.

### OnCommand {:#OnCommand}

 Called after Panel key down and up events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>command</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.avrcp/index.html'>fuchsia.bluetooth.avrcp</a>/<a class='link' href='../fuchsia.bluetooth.avrcp/index.html#AvcPanelCommand'>AvcPanelCommand</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='#ResponseCode'>ResponseCode</a></code>
            </td>
        </tr></table>

## ControllerExt {:#ControllerExt}
*Defined in [fuchsia.bluetooth.avrcp.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp.test/test.fidl#61)*

 Provides additional methods not in `Controller` that are strictly for testing and debug.

### IsConnected {:#IsConnected}

 Returns whether there is an underlying connection open with the remote device currently.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>connected</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### GetEventsSupported {:#GetEventsSupported}

 Queries the target and returns what events are supported for notification.
 Sends GetCapabilties(0x03 (`EVENTS_SUPPORTED`)) command for all events supported by
 the negoitated version of AVRCP.

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
                <code><a class='link' href='#ControllerExt_GetEventsSupported_Result'>ControllerExt_GetEventsSupported_Result</a></code>
            </td>
        </tr></table>

### Connect {:#Connect}

 Explicitly attempt to connect to the remote peer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Disconnect {:#Disconnect}

 Explicitly disconnect any L2CAP channels, if any, to the remote peer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SendRawVendorDependentCommand {:#SendRawVendorDependentCommand}

 Send raw vendor depedent "Control" command packet to a specific PDU on the remote peer.
 Returns the entire response packet including the headers or error if the remote endpoint
 disconnects or does not return a response in set amount of time.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pdu_id</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>command</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ControllerExt_SendRawVendorDependentCommand_Result'>ControllerExt_SendRawVendorDependentCommand_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### PeerManagerExt_GetControllerForTarget_Response {:#PeerManagerExt_GetControllerForTarget_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ControllerExt_GetEventsSupported_Response {:#ControllerExt_GetEventsSupported_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>events_supported</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.avrcp/index.html'>fuchsia.bluetooth.avrcp</a>/<a class='link' href='../fuchsia.bluetooth.avrcp/index.html#TargetEvent'>TargetEvent</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ControllerExt_SendRawVendorDependentCommand_Response {:#ControllerExt_SendRawVendorDependentCommand_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ResponseCode {:#ResponseCode}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.avrcp.test/test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.avrcp.test/test.fidl#43)*

 Defined by the AV/C Digital Interface Command Set General Specification and AV/C Panel Subunit
 Specification (http://1394ta.org/specifications/)


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_IMPLEMENTED</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>ACCEPTED</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>REJECTED</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>IN_TRANSITION</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr><tr>
            <td><code>IMPLEMENTED_STABLE</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHANGED</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERIM</code></td>
            <td><code>15</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### PeerManagerExt_GetControllerForTarget_Result {:#PeerManagerExt_GetControllerForTarget_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#PeerManagerExt_GetControllerForTarget_Response'>PeerManagerExt_GetControllerForTarget_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### ControllerExt_GetEventsSupported_Result {:#ControllerExt_GetEventsSupported_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ControllerExt_GetEventsSupported_Response'>ControllerExt_GetEventsSupported_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.avrcp/index.html'>fuchsia.bluetooth.avrcp</a>/<a class='link' href='../fuchsia.bluetooth.avrcp/index.html#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>

### ControllerExt_SendRawVendorDependentCommand_Result {:#ControllerExt_SendRawVendorDependentCommand_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ControllerExt_SendRawVendorDependentCommand_Response'>ControllerExt_SendRawVendorDependentCommand_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.avrcp/index.html'>fuchsia.bluetooth.avrcp</a>/<a class='link' href='../fuchsia.bluetooth.avrcp/index.html#ControllerError'>ControllerError</a></code>
            </td>
            <td></td>
        </tr></table>







