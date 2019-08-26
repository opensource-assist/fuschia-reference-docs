Project: /_project.yaml
Book: /_book.yaml

# fuchsia.wlan.policy


## **PROTOCOLS**

## ClientProvider {:#ClientProvider}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#19)*

 The ClientProvider API provides a mechanism for wlan control and is intended
 to be called by applications or entities representing the user (ex, Settings).
 This API is not intended to be called by other applications to change wlan
 state without explicit user control.

 The second aim of this API design is to eliminate the "last-caller wins"
 paradigm by limiting the number of controlling applications.  A single caller
 at a time is permitted to make API calls that impact wlan state.

### GetController {:#GetController}

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



## ClientListener {:#ClientListener}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#31)*

 The ClientListener API provides a mechanism for callers to receive state change
 updates about wlan operation.

### GetListener {:#GetListener}

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



## ClientController {:#ClientController}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#42)*

 ClientControllers allow the caller to trigger wlan state changes.  This includes
 whether connections will be attempted, scan triggers and saved network
 configuration changes.

 Individual calls provided by the API are triggered after registering with
 the wlan ClientProvider via the OpenControlChannel call.

### StartClientConnections {:#StartClientConnections}

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
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

### StopClientConnections {:#StopClientConnections}

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
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

### ScanForNetworks {:#ScanForNetworks}

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



### SaveNetwork {:#SaveNetwork}

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

### RemoveNetwork {:#RemoveNetwork}

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

### GetSavedNetworks {:#GetSavedNetworks}

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



### Connect {:#Connect}

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
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#RequestStatus'>RequestStatus</a></code>
            </td>
        </tr></table>

## ScanResultIterator {:#ScanResultIterator}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#87)*

 Iterator used to send back scan results to the caller.  The corresponding channel
 will be closed after the scan is complete and results are returned or fails due
 to an error.

### GetNext {:#GetNext}

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

## NetworkConfigIterator {:#NetworkConfigIterator}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#136)*

 Iterator used by callers to retrieve saved network information.

### GetNext {:#GetNext}

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

## ClientStateUpdates {:#ClientStateUpdates}
*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#149)*

 Wlan status changes for client connections and the associated network state.
 These updates contain information about whether or not the device will attempt
 to connect to networks, saved network configuration change information,
 individual connection state information by NetworkIdentifier and connection
 attempt information.  The connection and network related calls are based on
 NetworkIdentifier to allow multiple simultaneous connections on supporting
 devices.

### OnClientStateUpdate {:#OnClientStateUpdate}

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

### ClientController_SaveNetwork_Response {:#ClientController_SaveNetwork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ClientController_RemoveNetwork_Response {:#ClientController_RemoveNetwork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ScanResultIterator_GetNext_Response {:#ScanResultIterator_GetNext_Response}
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

### NetworkIdentifier {:#NetworkIdentifier}
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

### Empty {:#Empty}
*Defined in [fuchsia.wlan.policy/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/types.fidl#54)*



 Empty struct used in place of optional values.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ScanErrorCode {:#ScanErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#96)*

 Wlan scan error codes.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>GENERAL_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CANCELLED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### WlanClientState {:#WlanClientState}
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

### Compatibility {:#Compatibility}
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
            <td></td>
        </tr><tr>
            <td><code>DISALLOWED_INSECURE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISALLOWED_NOT_SUPPORTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### NetworkConfigChangeError {:#NetworkConfigChangeError}
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

### ConnectionState {:#ConnectionState}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#210)*

 Connection states used to update registered wlan observers.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISCONNECTED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTING</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTED</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### DisconnectStatus {:#DisconnectStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.policy/client_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.policy/client_provider.fidl#226)*

 Disconnect and connection attempt failure status codes


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>TIMED_OUT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CREDENTIALS_FAILED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_STOPPED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_FAILED</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### SecurityType {:#SecurityType}
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



## **TABLES**

### ScanResult {:#ScanResult}


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

### Bss {:#Bss}


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
                <code>int32</code>
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

### ClientStateSummary {:#ClientStateSummary}


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

### NetworkState {:#NetworkState}


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

### NetworkConfig {:#NetworkConfig}


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

### ClientController_SaveNetwork_Result {:#ClientController_SaveNetwork_Result}
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

### ClientController_RemoveNetwork_Result {:#ClientController_RemoveNetwork_Result}
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

### ScanResultIterator_GetNext_Result {:#ScanResultIterator_GetNext_Result}
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

### Credential {:#Credential}
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





