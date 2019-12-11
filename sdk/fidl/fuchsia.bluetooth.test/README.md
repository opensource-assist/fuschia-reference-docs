[TOC]

# fuchsia.bluetooth.test


## **PROTOCOLS**

## Peer {#Peer}
*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#109)*

<p>Protocol used to drive the state of a fake peer device.</p>

### AssignConnectionStatus {#AssignConnectionStatus}

<p>Assign a HCI <code>status</code> for the controller to generate in response to connection requests.
Applies to all successive HCI_Create_Connection and HCI_LE_Create_Connection commands. The
procedure is acknowledged with an empty response.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#HciError'>HciError</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### EmulateLeConnectionComplete {#EmulateLeConnectionComplete}

<p>Emulates a LE connection event. Does nothing if the peer is already connected. The
<code>role</code> parameter determines the link layer connection role.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#ConnectionRole'>ConnectionRole</a></code>
            </td>
        </tr></table>



### EmulateDisconnectionComplete {#EmulateDisconnectionComplete}

<p>Emulate disconnection. Does nothing if the peer is not connected.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### WatchConnectionStates {#WatchConnectionStates}

<p>Watch connection state changes using the
<a href="/docs/development/api/fidl.md#delay-responses-using-hanging-gets">hanging get pattern</a>.
Notifies the most recent controller connection state if there has been a change since the
last time this method was called.</p>
<p>Multiple calls to this method can be outstanding at a given time. All calls will resolve in
a response as soon as there is a change to the connection state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>states</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ConnectionState'>ConnectionState</a>&gt;</code>
            </td>
        </tr></table>

## HciEmulator {#HciEmulator}
*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#134)*

<p>Protocol used to emulate a Bluetooth controller that supports the standard Bluetooth HCI.</p>

### Publish {#Publish}

<p>Publish a bt-hci device using the provided <code>settings</code>. Each HciEmulator instance can only
manage a single bt-hci device. Returns Emulator.<code>HCI_ALREADY_PUBLISHED</code> if the device has
already been published.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#EmulatorSettings'>EmulatorSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#HciEmulator_Publish_Result'>HciEmulator_Publish_Result</a></code>
            </td>
        </tr></table>

### AddLowEnergyPeer {#AddLowEnergyPeer}

<p>Inserts a new LE peer device to be emulated by this controller. Once registered, the state
of the fake peer can be driven and observed using the <code>peer</code> handle.</p>
<p>A reply will be sent to acknowledge the creation of the fake peer. If a peer cannot be
initialized (e.g. due to a missing required field in <code>parameters</code> or for containing an
address that is already emulated) the <code>peer</code> handle will be closed and an error reply will
be sent.</p>
<p>The peer will appear in advertising reports and respond to requests according to its
configuration as long as the <code>peer</code> channel is open. The emulator stops emulating this peer
when the channel gets closed, which makes it no longer discoverable and not respond to any
requests.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>parameters</code></td>
            <td>
                <code><a class='link' href='#LowEnergyPeerParameters'>LowEnergyPeerParameters</a></code>
            </td>
        </tr><tr>
            <td><code>peer</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Peer'>Peer</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#HciEmulator_AddLowEnergyPeer_Result'>HciEmulator_AddLowEnergyPeer_Result</a></code>
            </td>
        </tr></table>

### AddBredrPeer {#AddBredrPeer}

<p>Inserts a new BR/EDR peer device to be emulated by this controller. Once registered, the state
of the fake peer can be driven and observed using the <code>peer</code> handle.</p>
<p>A reply will be sent to acknowledge the creation of the fake peer. If a peer cannot be
initialized (e.g. due to a missing required field in <code>parameters</code> or for containing an
address that is already emulated) the <code>peer</code> handle will be closed and an error reply will
be sent.</p>
<p>The peer will appear in inquiry results and respond to requests according to its
configuration as long as the <code>peer</code> channel is open. The emulator stops emulating this peer
when the channel gets closed, which makes it no longer discoverable and not respond to any
requests.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>parameters</code></td>
            <td>
                <code><a class='link' href='#BredrPeerParameters'>BredrPeerParameters</a></code>
            </td>
        </tr><tr>
            <td><code>peer</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Peer'>Peer</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#HciEmulator_AddBredrPeer_Result'>HciEmulator_AddBredrPeer_Result</a></code>
            </td>
        </tr></table>

### WatchControllerParameters {#WatchControllerParameters}

<p>Returns the current controller parameter state. If the parameters have not changed since the
last time this message was received, then this method does not return until there is a
change.
(see <a href="//docs/development/api/fidl.md#delay-responses-using-hanging-gets">hanging get pattern</a>)</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>parameters</code></td>
            <td>
                <code><a class='link' href='#ControllerParameters'>ControllerParameters</a></code>
            </td>
        </tr></table>

### WatchLeScanStates {#WatchLeScanStates}

<p>Returns the most recent set of state transitions for the link layer LE scan procedure. This
method returns when there has been a state change since the last invocation of this method
by this client.</p>
<p>Multiple calls to this method can be outstanding at a given time. All calls will resolve in
a response as soon as there is a change to the scan state.
(see <a href="//docs/development/api/fidl.md#delay-responses-using-hanging-gets">hanging get pattern</a>)</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>states</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LeScanState'>LeScanState</a>&gt;</code>
            </td>
        </tr></table>

### WatchLegacyAdvertisingStates {#WatchLegacyAdvertisingStates}

<p>Returns the most recent set of state transitions for the link layer LE legacy advertising
procedure. This method returns when there has been a state change since the last invocation
of this method by this client.</p>
<p>Only one call to this method can be outstanding at a given time. The
<a class='link' href='#HciEmulator'>HciEmulator</a> channel will be closed if a call received when one is
already pending.
(see <a href="//docs/development/api/fidl.md#delay-responses-using-hanging-gets">hanging get pattern</a>)</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>states</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#LegacyAdvertisingState'>LegacyAdvertisingState</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### HciEmulator_Publish_Response {#HciEmulator_Publish_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### HciEmulator_AddLowEnergyPeer_Response {#HciEmulator_AddLowEnergyPeer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### HciEmulator_AddBredrPeer_Response {#HciEmulator_AddBredrPeer_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AclBufferSettings {#AclBufferSettings}
*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#37)*



<p>The HCI ACL data flow-control parameters.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data_packet_length</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>ACL frame MTU in bytes.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_num_data_packets</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>The maximum number of ACL frames that the controller can buffer.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AdvertisingData {#AdvertisingData}
*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#68)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[31]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### LegacyAdvertisingType {#LegacyAdvertisingType}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.test/controller_states.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/controller_states.fidl#31)*

<p>LE legacy advertising types from Bluetooth Core Specification 5.1 Vol 2, Part E, Section 7.8.5.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADV_IND</code></td>
            <td><code>0</code></td>
            <td><p>Connectable and scannable.</p>
</td>
        </tr><tr>
            <td><code>ADV_DIRECT_IND</code></td>
            <td><code>1</code></td>
            <td><p>Connectable, high-duty cycle, directed.</p>
</td>
        </tr><tr>
            <td><code>ADV_SCAN_IND</code></td>
            <td><code>2</code></td>
            <td><p>Scannable, undirected.</p>
</td>
        </tr><tr>
            <td><code>ADV_NONCONN_IND</code></td>
            <td><code>3</code></td>
            <td><p>Non-connectable, undirected</p>
</td>
        </tr><tr>
            <td><code>SCAN_RSP</code></td>
            <td><code>4</code></td>
            <td><p>Scan response</p>
</td>
        </tr></table>

### EmulatorError {#EmulatorError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#10)*

<p>Error codes that can be generated for emulator-wide configurations.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>HCI_ALREADY_PUBLISHED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### EmulatorPeerError {#EmulatorPeerError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#16)*

<p>Error codes that are generated for functions that manipulate fake peers.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADDRESS_REPEATED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PARAMETERS_INVALID</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### HciConfig {#HciConfig}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#28)*

<p>Pre-set HCI configurations.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DUAL_MODE</code></td>
            <td><code>1</code></td>
            <td><p>Support both BR/EDR and LE in LMP features.</p>
</td>
        </tr><tr>
            <td><code>LE_ONLY</code></td>
            <td><code>2</code></td>
            <td><p>Limits supported features and HCI commands to those that are required for LE only.</p>
</td>
        </tr></table>

### ConnectionState {#ConnectionState}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#103)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONNECTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISCONNECTED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### HciError {#HciError}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.test/hci_errors.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_errors.fidl#9)*

<p>Defines the list of HCI protocol error codes that a Bluetooth controller can report. These
values are taken from Bluetooth Core Specification v5.1, Vol 2, Part D.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_COMMAND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_CONNECTION_ID</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>HARDWARE_FAILURE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAGE_TIMEOUT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTHENTICATION_FAILURE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>PIN_OR_KEY_MISSING</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEMORY_CAPACITY_EXCEEDED</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_TIMEOUT</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_LIMIT_EXCEEDED</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYNCHRONOUS_CONNECTION_LIMIT_EXCEEDED</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_ALREADY_EXISTS</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMAND_DISALLOWED</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_REJECTED_LIMITED_RESOURCES</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_REJECTED_SECURITY</code></td>
            <td><code>14</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_REJECTED_BAD_BD_ADDR</code></td>
            <td><code>15</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_ACCEPT_TIMEOUT_EXCEEDED</code></td>
            <td><code>16</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED_FEATURE_OR_PARAMETER</code></td>
            <td><code>17</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_HCICOMMAND_PARAMETERS</code></td>
            <td><code>18</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOTE_USER_TERMINATED_CONNECTION</code></td>
            <td><code>19</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOTE_DEVICE_TERMINATED_CONNECTION_LOW_RESOURCES</code></td>
            <td><code>20</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOTE_DEVICE_TERMINATED_CONNECTION_POWER_OFF</code></td>
            <td><code>21</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_TERMINATED_BY_LOCAL_HOST</code></td>
            <td><code>22</code></td>
            <td></td>
        </tr><tr>
            <td><code>REPEATED_ATTEMPTS</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAIRING_NOT_ALLOWED</code></td>
            <td><code>24</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_LMP_PDU</code></td>
            <td><code>25</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED_REMOTE_FEATURE</code></td>
            <td><code>26</code></td>
            <td></td>
        </tr><tr>
            <td><code>SCO_OFFSET_REJECTED</code></td>
            <td><code>27</code></td>
            <td></td>
        </tr><tr>
            <td><code>SCO_INTERVAL_REJECTED</code></td>
            <td><code>28</code></td>
            <td></td>
        </tr><tr>
            <td><code>SCO_AIR_MODE_REJECTED</code></td>
            <td><code>29</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_LMP_OR_LL_PARAMETERS</code></td>
            <td><code>30</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSPECIFIED_ERROR</code></td>
            <td><code>31</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED_LMP_OR_LL_PARAMETER_VALUE</code></td>
            <td><code>32</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROLE_CHANGE_NOT_ALLOWED</code></td>
            <td><code>33</code></td>
            <td></td>
        </tr><tr>
            <td><code>LMP_OR_LL_RESPONSE_TIMEOUT</code></td>
            <td><code>34</code></td>
            <td></td>
        </tr><tr>
            <td><code>LMP_ERROR_TRANSACTION_COLLISION</code></td>
            <td><code>35</code></td>
            <td></td>
        </tr><tr>
            <td><code>LMP_PDU_NOT_ALLOWED</code></td>
            <td><code>36</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENCRYPTION_MODE_NOT_ACCEPTABLE</code></td>
            <td><code>37</code></td>
            <td></td>
        </tr><tr>
            <td><code>LINK_KEY_CANNOT_BE_CHANGED</code></td>
            <td><code>38</code></td>
            <td></td>
        </tr><tr>
            <td><code>REQUESTED_QOS_NOT_SUPPORTED</code></td>
            <td><code>39</code></td>
            <td></td>
        </tr><tr>
            <td><code>INSTANT_PASSED</code></td>
            <td><code>40</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAIRING_WITH_UNIT_KEY_NOT_SUPPORTED</code></td>
            <td><code>41</code></td>
            <td></td>
        </tr><tr>
            <td><code>DIFFERENT_TRANSACTION_COLLISION</code></td>
            <td><code>42</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED0</code></td>
            <td><code>43</code></td>
            <td></td>
        </tr><tr>
            <td><code>QOS_UNACCEPTABLE_PARAMETER</code></td>
            <td><code>44</code></td>
            <td></td>
        </tr><tr>
            <td><code>QOS_REJECTED</code></td>
            <td><code>45</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHANNEL_CLASSIFICATION_NOT_SUPPORTED</code></td>
            <td><code>46</code></td>
            <td></td>
        </tr><tr>
            <td><code>INSUFFICIENT_SECURITY</code></td>
            <td><code>47</code></td>
            <td></td>
        </tr><tr>
            <td><code>PARAMETER_OUT_OF_MANDATORY_RANGE</code></td>
            <td><code>48</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED1</code></td>
            <td><code>49</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROLE_SWITCH_PENDING</code></td>
            <td><code>50</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED2</code></td>
            <td><code>51</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESERVED_SLOT_VIOLATION</code></td>
            <td><code>52</code></td>
            <td></td>
        </tr><tr>
            <td><code>ROLE_SWITCH_FAILED</code></td>
            <td><code>53</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXTENDED_INQUIRY_RESPONSE_TOO_LARGE</code></td>
            <td><code>54</code></td>
            <td></td>
        </tr><tr>
            <td><code>SECURE_SIMPLE_PAIRING_NOT_SUPPORTED_BY_HOST</code></td>
            <td><code>55</code></td>
            <td></td>
        </tr><tr>
            <td><code>HOST_BUSY_PAIRING</code></td>
            <td><code>56</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_REJECTED_NO_SUITABLE_CHANNEL_FOUND</code></td>
            <td><code>57</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONTROLLER_BUSY</code></td>
            <td><code>58</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNACCEPTABLE_CONNECTION_PARAMETERS</code></td>
            <td><code>59</code></td>
            <td></td>
        </tr><tr>
            <td><code>DIRECTED_ADVERTISING_TIMEOUT</code></td>
            <td><code>60</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_TERMINATED_MIC_FAILURE</code></td>
            <td><code>61</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTION_FAILED_TO_BE_ESTABLISHED</code></td>
            <td><code>62</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAC_CONNECTION_FAILED</code></td>
            <td><code>63</code></td>
            <td></td>
        </tr><tr>
            <td><code>COARSE_CLOCK_ADJUSTMENT_REJECTED</code></td>
            <td><code>64</code></td>
            <td></td>
        </tr><tr>
            <td><code>TYPE0_SUBMAP_NOT_DEFINED</code></td>
            <td><code>65</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_ADVERTISING_IDENTIFIER</code></td>
            <td><code>66</code></td>
            <td></td>
        </tr><tr>
            <td><code>LIMIT_REACHED</code></td>
            <td><code>67</code></td>
            <td></td>
        </tr><tr>
            <td><code>OPERATION_CANCELLED_BY_HOST</code></td>
            <td><code>68</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ControllerParameters {#ControllerParameters}


*Defined in [fuchsia.bluetooth.test/controller_states.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/controller_states.fidl#20)*

<p>Contains Bluetooth controller &amp; baseband parameters that are writable by the host but don't
fall under a particular procedural category (as are those defined below).</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>local_name</code></td>
            <td>
                <code>string[248]</code>
            </td>
            <td><p>The local name used for the Link Layer name discovery procedure. This parameter only applies
for the BR/EDR transport. In LE, the local name is provided as an advertising parameter and
via GATT.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>device_class</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#DeviceClass'>DeviceClass</a></code>
            </td>
            <td><p>The local &quot;Class of Device&quot; used during the BR/EDR inquiry procedure.</p>
</td>
        </tr></table>

### LegacyAdvertisingState {#LegacyAdvertisingState}


*Defined in [fuchsia.bluetooth.test/controller_states.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/controller_states.fidl#49)*

<p>Controller parameters for legacy advertising.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if advertising has been enabled using the HCI_LE_Set_Advertising_Enable command.
This field is always present.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#LegacyAdvertisingType'>LegacyAdvertisingType</a></code>
            </td>
            <td><p>The most recently configured advertising type. This field is always present. Defaults to
<a class='link' href='#LegacyAdvertisingType.ADV_IND'>LegacyAdvertisingType.ADV_IND</a>.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>address_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#AddressType'>AddressType</a></code>
            </td>
            <td><p>The LE address type being used for advertising. This field is always present. Defaults to
<a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#AddressType.PUBLIC'>AddressType.PUBLIC</a>.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>interval_min</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The host-specified advertising interval range parameters. Present only if configured.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>interval_max</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>advertising_data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[31]</code>
            </td>
            <td><p>Any configured advertising and scan response data. Present only if either field is non-zero.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>scan_response</code></td>
            <td>
                <code>vector&lt;uint8&gt;[31]</code>
            </td>
            <td></td>
        </tr></table>

### LeScanState {#LeScanState}


*Defined in [fuchsia.bluetooth.test/controller_states.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/controller_states.fidl#73)*

<p>Represents the LE scan state. The fields are present if scan parameters have been
configured.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if a scan is enabled.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if an active scan is enabled. Otherwise the scan is passive.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>interval</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The scan interval and window parameters. These are defined in Bluetooth controller
&quot;timeslices&quot; where 1 slice = 0.625 ms. Valid values range from 0x4 (2.5 ms) to 0x4000 (10.24
ms).</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>window</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>filter_duplicates</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if duplicate filtering has been enabled.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>address_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#AddressType'>AddressType</a></code>
            </td>
            <td><p>The type of local device address used.</p>
</td>
        </tr></table>

### EmulatorSettings {#EmulatorSettings}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#46)*

<p>Controller settings used by the emulator.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>The <code>BD_ADDR</code> (BR/EDR) or LE Public Device Address. Defaults to &quot;00:00:00:00:00:00&quot;.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>hci_config</code></td>
            <td>
                <code><a class='link' href='#HciConfig'>HciConfig</a></code>
            </td>
            <td><p>Supported HCI command configuration. Defaults to &quot;<code>DUAL_MODE</code>&quot;.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>extended_advertising</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>True if the 5.0 extended advertising features are supported. Defaults to &quot;false&quot;.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>acl_buffer_settings</code></td>
            <td>
                <code><a class='link' href='#AclBufferSettings'>AclBufferSettings</a></code>
            </td>
            <td><p>The ACL-U data buffer settings. Defaults to
data_packet_length: 1024
total_num_data_packets: 5
IF <code>hci_config</code> is set to <code>DUAL_MODE</code>. Defaults to null otherwise.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>le_acl_buffer_settings</code></td>
            <td>
                <code><a class='link' href='#AclBufferSettings'>AclBufferSettings</a></code>
            </td>
            <td><p>The LE-U ACL data buffer settings. Defaults to
data_packet_length: 251
total_num_data_packets: 5</p>
</td>
        </tr></table>

### LowEnergyPeerParameters {#LowEnergyPeerParameters}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#73)*

<p>Parameters used to emulate a peer's behavior over the Low Energy transport.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>The LE identity address of the peer. This field is mandatory.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When present and true, the peer will send connectable advertisements and accept connection
requests. The peer will ignore connection requests if not connectable.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>advertisement</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td><p>The advertising data contents. If not present, the advertising data sent by this peer will
be empty.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>scan_response</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td><p>The scan response data contents. When present, the fake controller will generate scannable
advertising packets and scan response events.</p>
</td>
        </tr></table>

### BredrPeerParameters {#BredrPeerParameters}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#91)*

<p>Parameters used to emulate a peer's behavior over the BR/EDR transport.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Address'>Address</a></code>
            </td>
            <td><p>The BD_ADDR of the peer. This field is mandatory.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When present and true, the peer will accept connection requests. The peer will ignore
connection requests if not connectable.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>device_class</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#DeviceClass'>DeviceClass</a></code>
            </td>
            <td><p>The device class reported in the inquiry response for this peer during device discovery.</p>
</td>
        </tr></table>



## **UNIONS**

### HciEmulator_Publish_Result {#HciEmulator_Publish_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#HciEmulator_Publish_Response'>HciEmulator_Publish_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#EmulatorError'>EmulatorError</a></code>
            </td>
            <td></td>
        </tr></table>

### HciEmulator_AddLowEnergyPeer_Result {#HciEmulator_AddLowEnergyPeer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#HciEmulator_AddLowEnergyPeer_Response'>HciEmulator_AddLowEnergyPeer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#EmulatorPeerError'>EmulatorPeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### HciEmulator_AddBredrPeer_Result {#HciEmulator_AddBredrPeer_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#HciEmulator_AddBredrPeer_Response'>HciEmulator_AddBredrPeer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#EmulatorPeerError'>EmulatorPeerError</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_LOCAL_NAME_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/controller_states.fidl#11">MAX_LOCAL_NAME_LENGTH</a></td>
            <td>
                    <code>248</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>The maximum size (in bytes) of a local name assigned using the HCI_Write_Local_Name command
(see Core Specification v5.1, Vol 2, Part E, 7.3.11).</p>
</td>
        </tr>
    <tr id="MAX_LEGACY_ADVERTISING_DATA_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/controller_states.fidl#15">MAX_LEGACY_ADVERTISING_DATA_LENGTH</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint8</code></td>
            <td><p>Advertising data MTUs for legacy (4.x) and extended (5.x) advertising PDU types
(see Core Specification v5.1, Vol 2, Part E, sections 7.3.11 &amp; 7.8.54).</p>
</td>
        </tr>
    <tr id="MAX_EXTENDED_ADVERTISING_DATA_LENGTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/controller_states.fidl#16">MAX_EXTENDED_ADVERTISING_DATA_LENGTH</a></td>
            <td>
                    <code>251</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    
</table>



