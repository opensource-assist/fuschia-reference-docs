Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.test


## **PROTOCOLS**

## HciEmulator {:#HciEmulator}
*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#144)*

 Protocol used to emulate a Bluetooth controller that supports the standard Bluetooth HCI.

### Publish {:#Publish}

 Publish a bt-hci device using the provided `settings`. Each HciEmulator instance can only
 manage a single bt-hci device. Returns Emulator.HCI_ALREADY_PUBLISHED if the device has
 already been published.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#EmulatorSettings'>EmulatorSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#HciEmulator_Publish_Result'>HciEmulator_Publish_Result</a></code>
            </td>
        </tr></table>

### AddPeer {:#AddPeer}

 Inserts a new peer device to be emulated by this controller. Returns an error if `peer` is
 improperly configured (e.g. does not contain an address). On success, returns an `id` that
 can be used to refer to the created peer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#FakePeer'>FakePeer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#HciEmulator_AddPeer_Result'>HciEmulator_AddPeer_Result</a></code>
            </td>
        </tr></table>

### RemovePeer {:#RemovePeer}

 Remove a previously inserted peer. Returns EmulatorPeerError.NOT_FOUND if `id` is not
 recognized.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#PeerId'>PeerId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#HciEmulator_RemovePeer_Result'>HciEmulator_RemovePeer_Result</a></code>
            </td>
        </tr></table>

### WatchLeScanState {:#WatchLeScanState}

 Returns the latest state of the link layer LE scan procedure. This method returns when there
 is a state change since the last invocation of this method by this client (see [hanging get
 pattern](//docs/development/api/fidl.md#delay-responses-using-hanging-gets))

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#LeScanState'>LeScanState</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### HciEmulator_Publish_Response {:#HciEmulator_Publish_Response}
*Defined in [fuchsia.bluetooth.test/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#2)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### HciEmulator_AddPeer_Response {:#HciEmulator_AddPeer_Response}
*Defined in [fuchsia.bluetooth.test/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#PeerId'>PeerId</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HciEmulator_RemovePeer_Response {:#HciEmulator_RemovePeer_Response}
*Defined in [fuchsia.bluetooth.test/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AclBufferSettings {:#AclBufferSettings}
*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#111)*



 The HCI ACL data flow-control parameters.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data_packet_length</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> ACL frame MTU in bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>total_num_data_packets</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td> The maximum number of ACL frames that the controller can buffer.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### EmulatorError {:#EmulatorError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#13)*

 Error codes that can be generated for emulator-wide configurations.


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

### EmulatorPeerError {:#EmulatorPeerError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#19)*

 Error codes that are generated for functions that manipulate fake peers.


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

### LeAddressType {:#LeAddressType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#26)*

 The Bluetooth device address type used with link layer procedures.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PUBLIC</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>RANDOM</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### HciConfig {:#HciConfig}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#102)*

 Pre-set HCI configurations.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DUAL_MODE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>LE_ONLY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### HciError {:#HciError}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.test/hci_errors.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_errors.fidl#9)*

 Defines the list of HCI protocol error codes that a Bluetooth controller can report. These
 values are taken from Bluetooth Core Specification v5.1, Vol 2, Part D.


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

### FakePeer {:#FakePeer}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#32)*

 Represents a peer that a FakeController can be configured to emulate.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Address'>Address</a></code>
            </td>
            <td> The LE identity address and/or BD_ADDR of the peer. This field is mandatory.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>le</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#LeParameters'>LeParameters</a></code>
            </td>
            <td> Parameters used by this peer on the Low Energy transport. This field is optional. The peer
 will not be active on the LE transport if this field is not present. However, the peer must
 support at least one transport.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>bredr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#BrEdrParameters'>BrEdrParameters</a></code>
            </td>
            <td> Parameters used by this peer on the BR/EDR transport. This field is optional. The peer
 will not be active on the BR/EDR transport if this field is not present. However, the peer
 must support at least one transport.
</td>
        </tr></table>

### LeParameters {:#LeParameters}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#53)*

 Parameters used to emulate a peer's behavior over the Low Energy transport.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the peer will send connectable advertisements and accept connection requests. The
 peer will ignore connection requests if not connectable.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>advertisement</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td> The advertising data contents. If not present, the advertising data sent by this peer will
 be empty.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>scan_response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td> The scan response data contents. When present, the fake controller will generate scannable
 advertising packets and scan response events.
</td>
        </tr></table>

### BrEdrParameters {:#BrEdrParameters}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#70)*

 Parameters used to emulate a peer's behavior over the BR/EDR transport.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### LeScanState {:#LeScanState}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#76)*

 Represents the LE scan state. The fields are present if scan parameters have been
 configured.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if a scan is enabled.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>active</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if an active scan is enabled. Otherwise the scan is passive.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>interval</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> The scan interval and window parameters. These are defined in Bluetotoh controller
 "timeslices" where 1 slice = 0.625 ms. Valid values range from 0x4 (2.5 ms) to 0x4000 (10.24
 ms).
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
            <td> True if duplicate filtering has been enabled.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>own_address_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#LeAddressType'>LeAddressType</a></code>
            </td>
            <td> The type of local device address used.
</td>
        </tr></table>

### EmulatorSettings {:#EmulatorSettings}


*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#120)*

 Controller settings used by the emulator.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Address'>Address</a></code>
            </td>
            <td> The BD_ADDR (BR/EDR) or LE Public Device Address. Defaults to "00:00:00:00:00:00".
</td>
        </tr><tr>
            <td>2</td>
            <td><code>hci_config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#HciConfig'>HciConfig</a></code>
            </td>
            <td> Supported HCI command configuration. Defaults to "DUAL_MODE".
</td>
        </tr><tr>
            <td>3</td>
            <td><code>extended_advertising</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if the 5.0 extended advertising features are supported. Defaults to "false".
</td>
        </tr><tr>
            <td>4</td>
            <td><code>acl_buffer_settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#AclBufferSettings'>AclBufferSettings</a></code>
            </td>
            <td> The ACL-U data buffer settings. Defaults to
    data_packet_length: 1024
    total_num_data_packets: 5
 IF `hci_config` is set to DUAL_MODE. Defaults to null otherwise.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>le_acl_buffer_settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#AclBufferSettings'>AclBufferSettings</a></code>
            </td>
            <td> The LE-U ACL data buffer settings. Defaults to
    data_packet_length: 251
    total_num_data_packets: 5
</td>
        </tr></table>



## **UNIONS**

### HciEmulator_Publish_Result {:#HciEmulator_Publish_Result}
*Defined in [fuchsia.bluetooth.test/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#5)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#HciEmulator_Publish_Response'>HciEmulator_Publish_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#EmulatorError'>EmulatorError</a></code>
            </td>
            <td></td>
        </tr></table>

### HciEmulator_AddPeer_Result {:#HciEmulator_AddPeer_Result}
*Defined in [fuchsia.bluetooth.test/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#12)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#HciEmulator_AddPeer_Response'>HciEmulator_AddPeer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#EmulatorPeerError'>EmulatorPeerError</a></code>
            </td>
            <td></td>
        </tr></table>

### HciEmulator_RemovePeer_Result {:#HciEmulator_RemovePeer_Result}
*Defined in [fuchsia.bluetooth.test/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#19)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#HciEmulator_RemovePeer_Response'>HciEmulator_RemovePeer_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.test/index.html#EmulatorPeerError'>EmulatorPeerError</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### AdvertisingData {:#AdvertisingData}
*Defined in [fuchsia.bluetooth.test/hci_emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#47)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>legacy_data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[31]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>extended_data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[251]</code>
            </td>
            <td></td>
        </tr></table>





## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#9">MAX_LEGACY_ADVERTISING_DATA_LENGTH</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint8</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.test/hci_emulator.fidl#10">MAX_EXTENDED_ADVERTISING_DATA_LENGTH</a></td>
            <td>
                    <code>251</code>
                </td>
                <td><code>uint8</code></td>
        </tr>
    
</table>

