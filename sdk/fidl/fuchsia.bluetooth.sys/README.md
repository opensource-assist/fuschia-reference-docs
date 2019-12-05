[TOC]

# fuchsia.bluetooth.sys


## **PROTOCOLS**

## ProcedureToken {#ProcedureToken}
*Defined in [fuchsia.bluetooth.sys/access.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/access.fidl#22)*

<p>Represents an active procedure. The validity of a handle that supports this protocol is tied to
the activity of the procedure that it is attached to. To elaborate:</p>
<ol>
<li>Closing a token handle ends the procedure that it is attached to.</li>
<li>The system closes a token handle to communicate that a procedure was internally terminated.</li>
</ol>

## Access {#Access}
*Defined in [fuchsia.bluetooth.sys/access.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/access.fidl#33)*

<p>Protocol that abstracts the operational modes and procedures defined in the Bluetooth Generic
Access Profile (see Core Specification v5.1, Vol 3, Part C).</p>
<p>The procedures under this protocol apply to the system as a whole. The Bluetooth controller that
plays an active role in these procedures can be managed using the HostWatcher protocol.</p>
<p>The procedures initiated by an Access protocol instance are terminated when the underlying
channel is closed.</p>

### SetPairingDelegate {#SetPairingDelegate}

<p>Assign a PairingDelegate to respond to drive pairing procedures. The delegate will be
configured to use the provided I/O capabilities to determine the pairing method.</p>
<p>Only one PairingDelegate can be registered at a time. Closing a PairingDelegate aborts all
on-going pairing procedures associated with a delegate and closes the PairingDelegate
previously assigned for this Access instance.</p>
<ul>
<li>request <code>input</code> Bluetooth input capability</li>
<li>request <code>output</code> Bluetooth output capability</li>
<li>request <code>delegate</code> The client end of a PairingDelegate channel.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='#InputCapability'>InputCapability</a></code>
            </td>
        </tr><tr>
            <td><code>output</code></td>
            <td>
                <code><a class='link' href='#OutputCapability'>OutputCapability</a></code>
            </td>
        </tr><tr>
            <td><code>delegate</code></td>
            <td>
                <code><a class='link' href='#PairingDelegate'>PairingDelegate</a></code>
            </td>
        </tr></table>



### SetLocalName {#SetLocalName}

<p>Assign a local name for the Bluetooth system. This name will be visible to nearby peers
when the system is in discoverable mode and during name discovery procedures.</p>
<ul>
<li>request <code>name</code> The complete local name to assign to the system.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetDeviceClass {#SetDeviceClass}

<p>Set the local device class that will be visible to nearby peers when the system is in
discoverable mode.</p>
<ul>
<li>request <code>device_class</code> The device class to assign to the system.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_class</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#DeviceClass'>DeviceClass</a></code>
            </td>
        </tr></table>



### MakeDiscoverable {#MakeDiscoverable}

<p>Put the system into the &quot;General Discoverable&quot; mode on the BR/EDR transport. The active
host will respond to general inquiry (by regularly entering the inquiry scan mode).</p>
<ul>
<li>request <code>token</code> <a class='link' href='#ProcedureToken'>ProcedureToken</a> that will remain valid while a
discoverable mode session is active. NOTE: The system may remain discoverable until all
<a class='link' href='#Access'>Access</a> clients drop their tokens.</li>
</ul>
<ul>
<li>error Reports Error.FAILED if inquiry mode cannot be entered.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ProcedureToken'>ProcedureToken</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Access_MakeDiscoverable_Result'>Access_MakeDiscoverable_Result</a></code>
            </td>
        </tr></table>

### StartDiscovery {#StartDiscovery}

<p>Start a general discovery procedure. All general discoverable BR/EDR, LE,
and BR/EDR/LE devices will appear in the peer list, which can be observed by calling
<a class='link' href='#Access.WatchPeers'>Access.WatchPeers</a>.</p>
<ul>
<li>request <code>token</code> <a class='link' href='#ProcedureToken'>ProcedureToken</a> that will remain valid while
discovery is in progress. NOTE: The radio will continue performing discovery until all
<a class='link' href='#Access'>Access</a> drop their tokens.</li>
</ul>
<ul>
<li>error Reports Error.FAILED if discovery on either transport cannot be initiated.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ProcedureToken'>ProcedureToken</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Access_StartDiscovery_Result'>Access_StartDiscovery_Result</a></code>
            </td>
        </tr></table>

### WatchPeers {#WatchPeers}

<p>Returns a list of all peers (connectable Bluetooth devices) known to the system. The first
call results in a snapshot of all known peers to be sent immediately in the <code>updated</code> return
paremeter. Subsequent calls receive a response only when one or more entries have been
added, modified, or removed from the entries reported since the most recent call.</p>
<ul>
<li>response <code>updated</code> Peers that were added or updated since the last call to WatchPeers().</li>
<li>response <code>removed</code> Ids of peers that were removed since the last call to WatchPeers().</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>updated</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Peer'>Peer</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>removed</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a>&gt;</code>
            </td>
        </tr></table>

### Connect {#Connect}

<p>Initiate a connection to the peer with the given <code>id</code>. This method connects both BR/EDR and
LE transports depending on the technologies that the peer is known to support.</p>
<ul>
<li>request <code>id</code> The id of the peer to connect.</li>
</ul>
<ul>
<li>error Reports <code>Error.FAILED</code> if a connection to the peer cannot be initiated.</li>
<li>error Reports <code>Error.PEER_NOT_FOUND</code> if <code>id</code> is not recognized.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Access_Connect_Result'>Access_Connect_Result</a></code>
            </td>
        </tr></table>

### Disconnect {#Disconnect}

<p>Disconnect all logical links to the peer with the given <code>id</code>. This includes LE and
BR/EDR links that have been initiated using all Access and fuchsia.bluetooth.le protocol
instances.</p>
<ul>
<li>request <code>id</code> The id of the peer to disconnect.</li>
</ul>
<ul>
<li>error Reports <code>Error.PEER_NOT_FOUND</code> if <code>id</code> is not recognized.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Access_Disconnect_Result'>Access_Disconnect_Result</a></code>
            </td>
        </tr></table>

### Forget {#Forget}

<p>Removes all bonding information and disconnects any existing links with the peer with the
given <code>id</code>.</p>
<ul>
<li>request <code>id</code> The id of the peer to forget.</li>
</ul>
<ul>
<li>error Reports <code>Error.PEER_NOT_FOUND</code> if <code>id</code> is not recognized.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Access_Forget_Result'>Access_Forget_Result</a></code>
            </td>
        </tr></table>

## Bootstrap {#Bootstrap}
*Defined in [fuchsia.bluetooth.sys/bootstrap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/bootstrap.fidl#23)*

<p>Protocol used to initialize persistent core Bluetooth data. This protocol populates data that
determine the identity of this device as perceived by other Bluetooth devices.</p>
<p>This protocol can be obtained only before the core Bluetooth host subsystem has generated its
own identity. Once initial data is committed, this capability becomes unavailable and remains
unavailable even if new Bluetooth adapters are attached.</p>
<p>Due to the privacy and bonding secrets involved, as well as the capability to make this device
assume the Bluetooth identity of another device, this protocol should only be exposed to
privileged components that can vouchsafe the origin of the data.</p>

### AddIdentities {#AddIdentities}

<p>Adds identities to be added to the unpopulated Bluetooth stack.</p>
<p>Repeated calls will append identities.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identities</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Identity'>Identity</a>&gt;</code>
            </td>
        </tr></table>



### Commit {#Commit}

<p>Writes all added bootstrapping data to the Bluetooth core stack. The server will close the
channel regardless of success. Returns without error if successful and the stack will be
considered initialized even if no bootstrapping data was written. Returns
INVALID_HOST_IDENTITY if any host or bonded peer data is insufficient or inconsistent, with
no effect (the client may retry by obtaining another protocol handle).</p>

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
                <code><a class='link' href='#Bootstrap_Commit_Result'>Bootstrap_Commit_Result</a></code>
            </td>
        </tr></table>

## HostWatcher {#HostWatcher}
*Defined in [fuchsia.bluetooth.sys/host_watcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/host_watcher.fidl#45)*

<p>Protocol used to observe and manage the Bluetooth controllers on the system.</p>

### Watch {#Watch}

<p>Obtain a list of all available Bluetooth controllers and their state. A response is sent
only if this list has changed since the last time the client has sent this message.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hosts</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#HostInfo'>HostInfo</a>&gt;</code>
            </td>
        </tr></table>

### SetActive {#SetActive}

<p>Designates the host with the given <code>id</code> as active. All Bluetooth procedures will be routed
over this host. Any previously assigned active host will be disabled and all of its pending
procedures will be terminated.</p>
<ul>
<li>error This can fail if a host with <code>id</code> was not found.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#HostWatcher_SetActive_Result'>HostWatcher_SetActive_Result</a></code>
            </td>
        </tr></table>

## PairingDelegate {#PairingDelegate}
*Defined in [fuchsia.bluetooth.sys/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/pairing_delegate.fidl#55)*


### OnPairingRequest {#OnPairingRequest}

<p>Called to initiate a pairing request. The delegate must respond with “true” or “false” to
either accept or reject the pairing request. If the pairing method requires a passkey
this is returned as well.</p>
<p>Any response from this method will be ignored if the OnPairingComplete
event has already been sent for <code>peer</code>.</p>
<p>The <code>displayed_passkey</code> parameter should be displayed to the user if <code>method</code> equals
<code>PairingMethod.PASSKEY_DISPLAY</code> or <code>PairingMethod.PASSKEY_COMPARISON</code>. Otherwise, this parameter
has no meaning and should be ignored.</p>
<p>The <code>entered_passkey</code> parameter only has meaning if <code>method</code> equals
<code>PairingMethod.PASSKEY_ENTRY</code>. It will be ignored otherwise.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer</code></td>
            <td>
                <code><a class='link' href='#Peer'>Peer</a></code>
            </td>
        </tr><tr>
            <td><code>method</code></td>
            <td>
                <code><a class='link' href='#PairingMethod'>PairingMethod</a></code>
            </td>
        </tr><tr>
            <td><code>displayed_passkey</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>accept</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>entered_passkey</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### OnPairingComplete {#OnPairingComplete}

<p>Called if the pairing procedure for the device with the given ID is completed.
This can be due to successful completion or an error (e.g. due to cancellation
by the peer, a timeout, or disconnection) which is indicated by <code>success</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
        </tr><tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnRemoteKeypress {#OnRemoteKeypress}

<p>Called to notify keypresses from the peer device during pairing using
<code>PairingMethod.PASSKEY_DISPLAY</code>.</p>
<p>This event is used to provide key press events to the delegate for a responsive user
experience as the user types the passkey on the peer device. This event will be called
once for each key-press.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
        </tr><tr>
            <td><code>keypress</code></td>
            <td>
                <code><a class='link' href='#PairingKeypress'>PairingKeypress</a></code>
            </td>
        </tr></table>



### OnLocalKeypress {#OnLocalKeypress}

<p>The delegate can send this event to notify the peer of local keypresses
during pairing using <code>PairingMethod.PASSKEY_ENTRY</code>.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
        </tr><tr>
            <td><code>keypress</code></td>
            <td>
                <code><a class='link' href='#PairingKeypress'>PairingKeypress</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Access_MakeDiscoverable_Response {#Access_MakeDiscoverable_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Access_StartDiscovery_Response {#Access_StartDiscovery_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Access_Connect_Response {#Access_Connect_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Access_Disconnect_Response {#Access_Disconnect_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Access_Forget_Response {#Access_Forget_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Bootstrap_Commit_Response {#Bootstrap_Commit_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### HostWatcher_SetActive_Response {#HostWatcher_SetActive_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### SecurityProperties {#SecurityProperties}
*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>authenticated</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>secure_connections</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>encryption_key_size</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Key {#Key}
*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#16)*



<p>Represents a 128-bit secret key.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PeerKey {#PeerKey}
*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#21)*



<p>Represents a key that was received from a peer.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>security</code></td>
            <td>
                <code><a class='link' href='#SecurityProperties'>SecurityProperties</a></code>
            </td>
            <td><p>The security properties of this link under which this key was received.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td><p>The contents of the key.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Ltk {#Ltk}
*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#34)*



<p>Represents a LE Long-Term peer key used for link encyrption. The |ediv| and |rand|
fields are zero if distributed using LE Secure Connections pairing.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#PeerKey'>PeerKey</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ediv</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rand</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LeConnectionParameters {#LeConnectionParameters}
*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#41)*



<p>The preferred LE connection parameters of the peer.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>connection_interval</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>connection_latency</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>supervision_timeout</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.sys/access.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/access.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td><p>Operation could not be performed.</p>
</td>
        </tr><tr>
            <td><code>PEER_NOT_FOUND</code></td>
            <td><code>2</code></td>
            <td><p>The peer designated for the operation was not found.</p>
</td>
        </tr></table>

### BootstrapError {#BootstrapError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.sys/bootstrap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/bootstrap.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID_HOST_IDENTITY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>WRITE_FAILURE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### InputCapability {#InputCapability}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.sys/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/pairing_delegate.fidl#11)*

<p>Input and Output Capabilities for pairing exchanges.
See Volume 3, Part C, Table 5.3 and 5.4</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONFIRMATION</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYBOARD</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### OutputCapability {#OutputCapability}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.sys/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/pairing_delegate.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISPLAY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### PairingMethod {#PairingMethod}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.sys/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/pairing_delegate.fidl#24)*

<p>Different types required by the Security Manager for pairing methods.
Bluetooth SIG has different requirements for different device capabilities.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONSENT</code></td>
            <td><code>1</code></td>
            <td><p>The user is asked to accept or reject pairing.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_DISPLAY</code></td>
            <td><code>2</code></td>
            <td><p>The user is shown a 6-digit numerical passkey which they must enter on the
peer device.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_COMPARISON</code></td>
            <td><code>3</code></td>
            <td><p>The user is shown a 6-digit numerical passkey which will also shown on the
peer device. The user must compare the passkeys and accept the pairing if
the passkeys match.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_ENTRY</code></td>
            <td><code>4</code></td>
            <td><p>The user is asked to enter a 6-digit passkey.</p>
</td>
        </tr></table>

### PairingKeypress {#PairingKeypress}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.sys/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/pairing_delegate.fidl#41)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DIGIT_ENTERED</code></td>
            <td><code>1</code></td>
            <td><p>The user has entered a single digit.</p>
</td>
        </tr><tr>
            <td><code>DIGIT_ERASED</code></td>
            <td><code>2</code></td>
            <td><p>The user has erased a single digit.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_CLEARED</code></td>
            <td><code>3</code></td>
            <td><p>The user has cleared the entire passkey.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_ENTERED</code></td>
            <td><code>4</code></td>
            <td><p>The user has finished entering the passkey.</p>
</td>
        </tr></table>

### TechnologyType {#TechnologyType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.sys/peer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/peer.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOW_ENERGY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLASSIC</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DUAL_MODE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### HostInfo {#HostInfo}


*Defined in [fuchsia.bluetooth.sys/host_watcher.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/host_watcher.fidl#11)*

<p>Information about a Bluetooth controller and its associated host-subsystem state.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Id'>Id</a></code>
            </td>
            <td><p>Uniquely identifies a host on the current system.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>technology</code></td>
            <td>
                <code><a class='link' href='#TechnologyType'>TechnologyType</a></code>
            </td>
            <td><p>The Bluetooth technologies that are supported by this adapter.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>The identity address.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Indicates whether or not this is the active host. The system has one active host which
handles all Bluetooth procedures.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>local_name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The local name of this host. This is the name that is visible to other devices when this
host is in the discoverable mode.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>discoverable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not the local adapter is currently discoverable over BR/EDR and
LE physical channels.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>discovering</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not device discovery is currently being performed.</p>
</td>
        </tr></table>

### LeData {#LeData}


*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#47)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>The identity address of the peer.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>connection_parameters</code></td>
            <td>
                <code><a class='link' href='#LeConnectionParameters'>LeConnectionParameters</a></code>
            </td>
            <td><p>The peer's preferred connection parameters, if known.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Uuid'>Uuid</a>&gt;</code>
            </td>
            <td><p>Known GATT service UUIDs.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>ltk</code></td>
            <td>
                <code><a class='link' href='#Ltk'>Ltk</a></code>
            </td>
            <td><p>The LE long-term key. Present if the link was encrypted.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>irk</code></td>
            <td>
                <code><a class='link' href='#PeerKey'>PeerKey</a></code>
            </td>
            <td><p>Identity Resolving RemoteKey used to generate and resolve random addresses.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>csrk</code></td>
            <td>
                <code><a class='link' href='#PeerKey'>PeerKey</a></code>
            </td>
            <td><p>Connection Signature Resolving RemoteKey used for data signing without encryption.</p>
</td>
        </tr></table>

### BredrData {#BredrData}


*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#67)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>The public device address of the peer.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>role_preference</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#ConnectionRole'>ConnectionRole</a></code>
            </td>
            <td><p>The peer's preferred piconet role. This is determined by role switch procedures. Paging and
connecting from a peer does not automatically set this flag. If absent, the peer has not
expressed a preference.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Uuid'>Uuid</a>&gt;</code>
            </td>
            <td><p>Known service UUIDs obtained from EIR data or SDP.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>link_key</code></td>
            <td>
                <code><a class='link' href='#PeerKey'>PeerKey</a></code>
            </td>
            <td><p>The semi-permanent BR/EDR key. Present if link was paired with Secure
Simple Pairing or stronger.</p>
</td>
        </tr></table>

### BondingData {#BondingData}


*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#85)*

<p>Represents the bonding data for a single peer.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>identifier</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
            <td><p>The identifier that uniquely identifies this peer.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>local_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>The local Bluetooth identity address that this bond is associated with.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The name of the peer, if known.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>le</code></td>
            <td>
                <code><a class='link' href='#LeData'>LeData</a></code>
            </td>
            <td><p>Bonding data that is present when this peer is paired on the LE transport.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>bredr</code></td>
            <td>
                <code><a class='link' href='#BredrData'>BredrData</a></code>
            </td>
            <td><p>Bonding data that is present when this peer is paired on the BR/EDR transport.</p>
</td>
        </tr></table>

### HostData {#HostData}


*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#103)*

<p>Represents persistent local host data.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>irk</code></td>
            <td>
                <code><a class='link' href='#Key'>Key</a></code>
            </td>
            <td><p>The local Identity Resolving Key used by a bt-host device to generate Resolvable Private
Addresses when privacy is enabled.</p>
<p>May be absent for hosts that do not use LE privacy, or that only use Non-Resolvable Private
Addresses.</p>
<p>NOTE: This key is distributed to LE peers during pairing procedures. The client must take
care to assign an IRK that consistent with the local bt-host identity.</p>
</td>
        </tr></table>

### Identity {#Identity}


*Defined in [fuchsia.bluetooth.sys/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#125)*

<p>Represents the persistent configuration of a single host-subsystem instance. This is used for
identity presentation (inquiry, inquiry response, and advertisement) and for bonding secrets
recall (encrypting link data to peers associated with this identity).</p>
<p>Each BR/EDR BD_ADDR and Low Energy public identity address used to bond should have its own
Identity instance containing corresponding peers.</p>
<p>Each Identity instance that supports LE privacy should have an Identity Resolving Key (IRK) that
is consistent with that distributed to its bonded peers.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>host</code></td>
            <td>
                <code><a class='link' href='#HostData'>HostData</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>bonds</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#BondingData'>BondingData</a>&gt;</code>
            </td>
            <td><p>All bonds that use a public identity address must contain the same local address.</p>
</td>
        </tr></table>

### Peer {#Peer}


*Defined in [fuchsia.bluetooth.sys/peer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/peer.fidl#16)*

<p>Represents a remote BR/EDR, LE, or dual-mode BR/EDR/LE peer.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
            <td><p>Uniquely identifies this peer on the current system.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>Bluetooth device address that identifies this peer. Clients
should display this field to the user when |name| is not available.</p>
<p>This field is always present.</p>
<p>NOTE: Clients should use the <code>identifier</code> field to keep track of peers instead of their
address.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>technology</code></td>
            <td>
                <code><a class='link' href='#TechnologyType'>TechnologyType</a></code>
            </td>
            <td><p>The Bluetooth technologies that are supported by this peer.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>connected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not a BR/EDR and/or LE connection exists to this peer.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>bonded</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not this peer is bonded.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The name of the peer, if known.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>appearance</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Appearance'>Appearance</a></code>
            </td>
            <td><p>The LE appearance property. Present if this peer supports LE and the
appearance information was obtained over advertising and/or GATT.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>device_class</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#DeviceClass'>DeviceClass</a></code>
            </td>
            <td><p>The class of device for this device, if known.</p>
</td>
        </tr><tr>
            <td>9</td>
            <td><code>rssi</code></td>
            <td>
                <code>int8</code>
            </td>
            <td><p>The most recently obtained advertising signal strength for this peer. Present if known.</p>
</td>
        </tr><tr>
            <td>10</td>
            <td><code>tx_power</code></td>
            <td>
                <code>int8</code>
            </td>
            <td><p>The most recently obtained transmission power for this peer. Present if known.</p>
</td>
        </tr><tr>
            <td>11</td>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Uuid'>Uuid</a>&gt;</code>
            </td>
            <td><p>The list of service UUIDs known to be available on this peer.</p>
</td>
        </tr></table>



## **UNIONS**

### Access_MakeDiscoverable_Result {#Access_MakeDiscoverable_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Access_MakeDiscoverable_Response'>Access_MakeDiscoverable_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Access_StartDiscovery_Result {#Access_StartDiscovery_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Access_StartDiscovery_Response'>Access_StartDiscovery_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Access_Connect_Result {#Access_Connect_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Access_Connect_Response'>Access_Connect_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Access_Disconnect_Result {#Access_Disconnect_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Access_Disconnect_Response'>Access_Disconnect_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Access_Forget_Result {#Access_Forget_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Access_Forget_Response'>Access_Forget_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Bootstrap_Commit_Result {#Bootstrap_Commit_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Bootstrap_Commit_Response'>Bootstrap_Commit_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#BootstrapError'>BootstrapError</a></code>
            </td>
            <td></td>
        </tr></table>

### HostWatcher_SetActive_Result {#HostWatcher_SetActive_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#HostWatcher_SetActive_Response'>HostWatcher_SetActive_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>









## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.sys/identity.fidl#30">LocalKey</a></td>
            <td>
                <code>fuchsia.bluetooth.sys/Key</code></td>
            <td><p>Represents a locally generated key that is distributed across one or more bonds.</p>
</td>
        </tr></table>

