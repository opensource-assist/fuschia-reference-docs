[TOC]

# fuchsia.wlan.policy


## **PROTOCOLS**

## AccessPointProvider {#AccessPointProvider}
*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#18)*

 The AccessPointProvider API provides a mechanism for access point
 control and is intended to be called by applications or entities representing
 the user (ex, Settings). This API is not intended to be called by other
 applications to change wlan state without explicit user control.

 The second aim of this API design is to eliminate the "last-caller wins"
 paradigm by limiting the number of controlling applications.  A single caller
 at a time is permitted to make API calls that impact wlan state.

### GetController {#GetController}

 Control channel used by a single caller to trigger wlan access point (ap) mode
 state changes.  The caller also provides a channel to receive wlan ap updates.
 Only one caller can have the control channel open at a time.  Attempts to
 register as a controller while there is an active control registration
 will result in the new caller's provided channel being closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requests</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AccessPointController'>AccessPointController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>updates</code></td>
            <td>
                <code><a class='link' href='#AccessPointStateUpdates'>AccessPointStateUpdates</a></code>
            </td>
        </tr></table>



## AccessPointListener {#AccessPointListener}
*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#30)*

 The AccessPointListener API provides a mechanism for callers to receive state change
 updates about wlan access point operation.

### GetListener {#GetListener}

 Registration for callers to receive wlan access point (ap) mode state updates.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>updates</code></td>
            <td>
                <code><a class='link' href='#AccessPointStateUpdates'>AccessPointStateUpdates</a></code>
            </td>
        </tr></table>



## AccessPointController {#AccessPointController}
*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#38)*

 AccessPointControllers allow the caller to trigger wlan state changes.  This
 includes whether the device will act as an access point and provide a wlan
 network for other co-located devices.

### StartAccessPoint {#StartAccessPoint}

 Enables wlan to initiate AccessPoint operation using the provided network
 configuration, connectivity mode and band.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr><tr>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#ConnectivityMode'>ConnectivityMode</a></code>
            </td>
        </tr><tr>
            <td><code>band</code></td>
            <td>
                <code><a class='link' href='#OperatingBand'>OperatingBand</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

### StopAccessPoint {#StopAccessPoint}

 Deactivate AccessPoint operation for a specified network configuration.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

### StopAllAccessPoints {#StopAllAccessPoints}

 Deactivates all AccessPoints currently operating on the device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## AccessPointStateUpdates {#AccessPointStateUpdates}
*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#52)*

 AccessPoint operation status changes along with associated connection status.

### OnAccessPointStateUpdate {#OnAccessPointStateUpdate}

 Updates registered listeners with the current summary of wlan access point
 operating states.  This will be called when there are changes with active
 access point networks - both the number of access points and their
 individual activity.  Registered listeners are responsible for deciding
 what information has changed (this is dependent on when they last
 acknowledged the update).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>access_points</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AccessPointState'>AccessPointState</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## ClientProvider {#ClientProvider}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#19)*

 The ClientProvider API provides a mechanism for wlan control and is intended
 to be called by applications or entities representing the user (ex, Settings).
 This API is not intended to be called by other applications to change wlan
 state without explicit user control.

 The second aim of this API design is to eliminate the "last-caller wins"
 paradigm by limiting the number of controlling applications.  A single caller
 at a time is permitted to make API calls that impact wlan state.

### GetController {#GetController}

 Control channel used by a single caller to trigger wlan client mode state
 changes.  The caller also provides a channel to receive wlan updates.
 Only one caller can have the control channel open at a time.  Attempts to
 register as a controller while there is an active control registration
 will result in the new caller's provided channel being closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requests</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ClientController'>ClientController</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>updates</code></td>
            <td>
                <code><a class='link' href='#ClientStateUpdates'>ClientStateUpdates</a></code>
            </td>
        </tr></table>



## ClientListener {#ClientListener}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#31)*

 The ClientListener API provides a mechanism for callers to receive state change
 updates about wlan operation.

### GetListener {#GetListener}

 Registration for callers to receive wlan client mode state updates.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>updates</code></td>
            <td>
                <code><a class='link' href='#ClientStateUpdates'>ClientStateUpdates</a></code>
            </td>
        </tr></table>



## ClientController {#ClientController}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#42)*

 ClientControllers allow the caller to trigger wlan state changes.  This includes
 whether connections will be attempted, scan triggers and saved network
 configuration changes.

 Individual calls provided by the API are triggered after registering with
 the wlan ClientProvider via the OpenControlChannel call.

### StartClientConnections {#StartClientConnections}

 Enables wlan to initiate connections to networks (either autoconnect to
 saved networks or act on incoming calls triggering connections).  Depending
 on the underlying capabilities of the device, this call may impact other
 device operation (for example, acting as an access point).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

### StopClientConnections {#StopClientConnections}

 Disables connections to wlan networks and tears down any existing connections.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

### ScanForNetworks {#ScanForNetworks}

 Triggers a network scan.  Note, even in normal operation, some scan requests
 may be rejected due to timing with connection establishment or other critical
 connection maintenance.  If the scan is cancelled or errors, the caller is
 notified via a status update in the ScanResultIterator.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ScanResultIterator'>ScanResultIterator</a>&gt;</code>
            </td>
        </tr></table>



### SaveNetwork {#SaveNetwork}

 Saves a network and any credential information needed to connect.  Multiple
 entries for the same NetworkIdentifier can exist if the credentials are
 different.  If a caller attempts to save a NetworkConfig with the same
 NetworkIdentifier and same Credentials as a previously saved network
 the method will effectively be a no-op.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ClientController_SaveNetwork_Result'>ClientController_SaveNetwork_Result</a></code>
            </td>
        </tr></table>

### RemoveNetwork {#RemoveNetwork}

 Removes a saved network configuration, if one exists.  This method will
 automatically trigger a disconnection if the NetworkConfig was used to
 establish the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#NetworkConfig'>NetworkConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ClientController_RemoveNetwork_Result'>ClientController_RemoveNetwork_Result</a></code>
            </td>
        </tr></table>

### GetSavedNetworks {#GetSavedNetworks}

 Retrieve the currently saved networks using the provided iterator.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iterator</code></td>
            <td>
                <code>request&lt;<a class='link' href='#NetworkConfigIterator'>NetworkConfigIterator</a>&gt;</code>
            </td>
        </tr></table>



### Connect {#Connect}

 Request to attempt a connection to the specified network.  The target of the
 connect call must already be a saved network.  This call is not a
 blocking call for the duration of the connection attempt.  If the call cannot
 be immediately attempted, a failure status will be returned.  If the connection
 request will be attempted, an acknowledgment status will be returned.  Updates
 to the connection status are disseminated via the ClientStateUpdates protocol.
 If the connect attempt fails, the service will fall back to default behavior
 with scanning and connecting via network selection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#NetworkIdentifier'>NetworkIdentifier</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

## ScanResultIterator {#ScanResultIterator}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#87)*

 Iterator used to send back scan results to the caller.  The corresponding channel
 will be closed after the scan is complete and results are returned or fails due
 to an error.

### GetNext {#GetNext}

 Allows caller to request the next set of scan results.  When all scan results
 have been handled, GetNext will return an empty vector and the channel will
 be closed.  If an error is encountered during the scan, it will be returned
 after all scan results have been retrieved.

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
                <code><a class='link' href='#ScanResultIterator_GetNext_Result'>ScanResultIterator_GetNext_Result</a></code>
            </td>
        </tr></table>

## NetworkConfigIterator {#NetworkConfigIterator}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#136)*

 Iterator used by callers to retrieve saved network information.

### GetNext {#GetNext}

 Method allowing the next block of saved networks to be handled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NetworkConfig'>NetworkConfig</a>&gt;</code>
            </td>
        </tr></table>

## ClientStateUpdates {#ClientStateUpdates}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#149)*

 Wlan status changes for client connections and the associated network state.
 These updates contain information about whether or not the device will attempt
 to connect to networks, saved network configuration change information,
 individual connection state information by NetworkIdentifier and connection
 attempt information.  The connection and network related calls are based on
 NetworkIdentifier to allow multiple simultaneous connections on supporting
 devices.

### OnClientStateUpdate {#OnClientStateUpdate}

 Updates registered listeners with the current summary of wlan client state.
 This will be called when there is any change to the state and the
 registered listeners are responsible for deciding what information has
 changed (since this is dependent on when they last acknowledged the update).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>summary</code></td>
            <td>
                <code><a class='link' href='#ClientStateSummary'>ClientStateSummary</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### ClientController_SaveNetwork_Response {#ClientController_SaveNetwork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ClientController_RemoveNetwork_Response {#ClientController_RemoveNetwork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ScanResultIterator_GetNext_Response {#ScanResultIterator_GetNext_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scan_results</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ScanResult'>ScanResult</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NetworkIdentifier {#NetworkIdentifier}
*Defined in [fuchsia.wlan.policy/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/types.fidl#23)*



 Primary means of distinguishing between available networks - the combination of
 the (mostly) human recognizable name and the security type.  The security type is used
 to distinguish between different network protection (or lack thereof) types.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td> Network name, often used by users to choose between networks in the UI.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#SecurityType'>SecurityType</a></code>
            </td>
            <td> Protection type (or not) for the network.
</td>
            <td>No default</td>
        </tr>
</table>

### Empty {#Empty}
*Defined in [fuchsia.wlan.policy/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/types.fidl#66)*



 Empty struct used in place of optional values.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ConnectivityMode {#ConnectivityMode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#83)*

 Connectivity operating mode for the access point.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOCAL_ONLY</code></td>
            <td><code>1</code></td>
            <td> Allows for connectivity between co-located devices.  Local only access points do not
 forward traffic to other network connections.
</td>
        </tr><tr>
            <td><code>UNRESTRICTED</code></td>
            <td><code>2</code></td>
            <td> Allows for full connectivity with traffic potentially being forwarded
 to other network connections (ex., tethering mode).
</td>
        </tr></table>

### OperatingState {#OperatingState}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#94)*

 Current detailed operating state for an access point.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td> Access point operation failed.  Access points that enter the failed state will
 have one update informing registered listeners of the failure and then an
 additional update with the access point removed from the list.
</td>
        </tr><tr>
            <td><code>STARTING</code></td>
            <td><code>2</code></td>
            <td> Access point operation is starting up.
</td>
        </tr><tr>
            <td><code>ACTIVE</code></td>
            <td><code>3</code></td>
            <td> Access point operation is active.
</td>
        </tr></table>

### ScanErrorCode {#ScanErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#96)*

 Wlan scan error codes.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>GENERAL_ERROR</code></td>
            <td><code>1</code></td>
            <td> Unexpected scan error without a specific cause.
</td>
        </tr><tr>
            <td><code>CANCELLED</code></td>
            <td><code>2</code></td>
            <td> Scan was cancelled and stopped.  This can happen due to operating state changes,
 higher priority operations or conflicting requests.
</td>
        </tr></table>

### WlanClientState {#WlanClientState}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#182)*

 Wlan operating state for client connections


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONNECTIONS_DISABLED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTIONS_ENABLED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Compatibility {#Compatibility}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#191)*

 High level compatibility for the scan result.  Not all network security protocols
 are supported.  New protocols may be detected before they are connectable
 and deprecated protocols may explicitly be unsupported due to security and
 privacy concerns.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUPPORTED</code></td>
            <td><code>1</code></td>
            <td> Denotes that the network is supported and connections can be attempted (given
 appropriate credentials when required).
</td>
        </tr><tr>
            <td><code>DISALLOWED_INSECURE</code></td>
            <td><code>2</code></td>
            <td> The network uses a deprecated security protocol and is explicitly not supported.
</td>
        </tr><tr>
            <td><code>DISALLOWED_NOT_SUPPORTED</code></td>
            <td><code>3</code></td>
            <td> The network uses a currently unsupported security protocol.
</td>
        </tr></table>

### NetworkConfigChangeError {#NetworkConfigChangeError}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#205)*

 Potential error cases for saving and removing network configurations.  This is
 intentionally sparse and will be expanded as use cases develop.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>GENERAL_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### ConnectionState {#ConnectionState}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#210)*

 Connection states used to update registered wlan observers.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td> The connection attempt was terminated due to an error.
</td>
        </tr><tr>
            <td><code>DISCONNECTED</code></td>
            <td><code>2</code></td>
            <td> The network is disconnected.
</td>
        </tr><tr>
            <td><code>CONNECTING</code></td>
            <td><code>3</code></td>
            <td> The device is attempting a connection to a network.
</td>
        </tr><tr>
            <td><code>CONNECTED</code></td>
            <td><code>4</code></td>
            <td> The connection is now established.  Note: This does not make any guarantees
 about higher level network reachability.
</td>
        </tr></table>

### DisconnectStatus {#DisconnectStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#226)*

 Disconnect and connection attempt failure status codes


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>TIMED_OUT</code></td>
            <td><code>1</code></td>
            <td> The requested connection attempt failed due to timeout.
</td>
        </tr><tr>
            <td><code>CREDENTIALS_FAILED</code></td>
            <td><code>2</code></td>
            <td> The requested connection attempt failed due to suspected credential failure.
</td>
        </tr><tr>
            <td><code>CONNECTION_STOPPED</code></td>
            <td><code>3</code></td>
            <td> The existing connection was explicitly disconnected by an action of wlan
 service on this device.  This can be the result of wlan connections being
 disabled, network configuration being removed or a connection attempt to a
 different network (as examples).
</td>
        </tr><tr>
            <td><code>CONNECTION_FAILED</code></td>
            <td><code>4</code></td>
            <td> The existing connection failed unexpectedly in a way that is not an
 explicitly triggered disconnect by the device (or user).  Examples
 of unexpected disconnections include: an underlying error (driver,
 firmware, etc.), beacon loss, access point failure.
</td>
        </tr></table>

### SecurityType {#SecurityType}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/types.fidl#12)*

 High level protection type for the network.  This does not convey all details needed
 for the mechanism of the connection, but is primarily used to map the target network
 to proper scan results.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>WEP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>WPA</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>WPA2</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>WPA3</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### OperatingBand {#OperatingBand}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/types.fidl#53)*

 Operating band for wlan control request and status updates.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ANY</code></td>
            <td><code>1</code></td>
            <td> Allows for band switching depending on device operating mode and environment.
</td>
        </tr><tr>
            <td><code>ONLY_2_4GHZ</code></td>
            <td><code>2</code></td>
            <td> Restricted to 2.4 GHz bands only.
</td>
        </tr><tr>
            <td><code>ONLY_5GHZ</code></td>
            <td><code>3</code></td>
            <td> Restricted to 5 GHz bands only.
</td>
        </tr></table>



## **TABLES**

### AccessPointState {#AccessPointState}


*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#65)*

 Information about the individual operating access points.  This includes limited
 information about any connected clients.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#OperatingState'>OperatingState</a></code>
            </td>
            <td> Current access point operating state
</td>
        </tr><tr>
            <td>2</td>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#ConnectivityMode'>ConnectivityMode</a></code>
            </td>
            <td> Requested operating connectivity mode
</td>
        </tr><tr>
            <td>3</td>
            <td><code>band</code></td>
            <td>
                <code><a class='link' href='#OperatingBand'>OperatingBand</a></code>
            </td>
            <td> Access point operating band.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>frequency</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Access point operating frequency (in MHz).
</td>
        </tr><tr>
            <td>5</td>
            <td><code>clients</code></td>
            <td>
                <code><a class='link' href='#ConnectedClientInformation'>ConnectedClientInformation</a></code>
            </td>
            <td> Information about connected clients
</td>
        </tr></table>

### ConnectedClientInformation {#ConnectedClientInformation}


*Defined in [fuchsia.wlan.policy/access_point_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/access_point_provider.fidl#109)*

 Connected client information.  This is initially limited to the number of
 connected clients.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>count</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td> Number of connected clients
</td>
        </tr></table>

### ScanResult {#ScanResult}


*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#108)*

 Information from an observed wlan network.  This includes the
 network name, security type, detected access point information and network
 compatibility information.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#NetworkIdentifier'>NetworkIdentifier</a></code>
            </td>
            <td> Network properties used to distinguish between networks and to group
 individual APs.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Bss'>Bss</a>&gt;</code>
            </td>
            <td> Individual access points offering the specified network.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>compatibility</code></td>
            <td>
                <code><a class='link' href='#Compatibility'>Compatibility</a></code>
            </td>
            <td> Indication if the detected network is supported by the implementation.
</td>
        </tr></table>

### Bss {#Bss}


*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#121)*

 Information for a particular ScanResult entry.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>bssid</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td> MAC address for the AP interface.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>rssi</code></td>
            <td>
                <code>int8</code>
            </td>
            <td> Calculated received signal strength for the beacon/probe response.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>frequency</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Operating frequency for this network (in MHz).
</td>
        </tr><tr>
            <td>4</td>
            <td><code>timestamp_nanos</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Realtime timestamp for this scan result entry.
</td>
        </tr></table>

### ClientStateSummary {#ClientStateSummary}


*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#161)*

 Information about the current client state for the device.  This includes if the
 device will attempt to connect to access points (when applicable), any existing
 connections and active connection attempts and their outcomes.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#WlanClientState'>WlanClientState</a></code>
            </td>
            <td> State indicating whether wlan will attempt to connect to networks or not.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>networks</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NetworkState'>NetworkState</a>&gt;</code>
            </td>
            <td> Active connections, connection attempts or failed connections.
</td>
        </tr></table>

### NetworkState {#NetworkState}


*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#170)*

 Information about current network connections and attempts.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#NetworkIdentifier'>NetworkIdentifier</a></code>
            </td>
            <td> Network id for the current connection (or attempt).
</td>
        </tr><tr>
            <td>2</td>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#ConnectionState'>ConnectionState</a></code>
            </td>
            <td> Current state for the connection.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#DisconnectStatus'>DisconnectStatus</a></code>
            </td>
            <td> Extra information for debugging or Settings display
</td>
        </tr></table>

### NetworkConfig {#NetworkConfig}


*Defined in [fuchsia.wlan.policy/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/types.fidl#32)*

 Network information used to establish a connection.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#NetworkIdentifier'>NetworkIdentifier</a></code>
            </td>
            <td> Identifier used to represent a specific network. No guarantee for uniqueness.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>credential</code></td>
            <td>
                <code><a class='link' href='#Credential'>Credential</a></code>
            </td>
            <td> Information needed to join a network.
</td>
        </tr></table>



## **UNIONS**

### ClientController_SaveNetwork_Result {#ClientController_SaveNetwork_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ClientController_SaveNetwork_Response'>ClientController_SaveNetwork_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#NetworkConfigChangeError'>NetworkConfigChangeError</a></code>
            </td>
            <td></td>
        </tr></table>

### ClientController_RemoveNetwork_Result {#ClientController_RemoveNetwork_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ClientController_RemoveNetwork_Response'>ClientController_RemoveNetwork_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#NetworkConfigChangeError'>NetworkConfigChangeError</a></code>
            </td>
            <td></td>
        </tr></table>

### ScanResultIterator_GetNext_Result {#ScanResultIterator_GetNext_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#ScanResultIterator_GetNext_Response'>ScanResultIterator_GetNext_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ScanErrorCode'>ScanErrorCode</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### Credential {#Credential}
*Defined in [fuchsia.wlan.policy/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/types.fidl#41)*

 Information used to verify access to a target network.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>none</code></td>
            <td>
                <code><a class='link' href='#Empty'>Empty</a></code>
            </td>
            <td> The network does not use credentials (open networks).
</td>
        </tr><tr>
            <td><code>password</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> Plaintext password (handled as binary data).
</td>
        </tr><tr>
            <td><code>psk</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> Hash representation of the network passphrase (handled as binary data).
</td>
        </tr></table>




