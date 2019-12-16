[TOC]

# fuchsia.bluetooth.control


## **PROTOCOLS**

## Control {#Control}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#56)*

<p>Primary Bluetooth control service to access bluetooth</p>

### IsBluetoothAvailable {#IsBluetoothAvailable}

<p>Returns whether or not Bluetooth is currently available on the system.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>available</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### SetPairingDelegate {#SetPairingDelegate}

<p>Registers a delegate to handle pairing requests.
Indicate the capability type of the PairingDelegate using <code>in</code> and <code>out</code>.
If your input/output capability is variable, call this function when it
changes to update.
Setting a pairing delegate closes the previously assigned pairing Delegate.</p>
<p>To disable pairing, set <code>delegate</code> to null.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>delegate</code></td>
            <td>
                <code><a class='link' href='#PairingDelegate'>PairingDelegate</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### GetAdapters {#GetAdapters}

<p>Returns information about all local adapters that are known to the system.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>adapters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AdapterInfo'>AdapterInfo</a>&gt;?</code>
            </td>
        </tr></table>

### SetActiveAdapter {#SetActiveAdapter}

<p>Sets the local adapter with the given <code>identifier</code> to act as the backing
adapter for all Bluetooth interfaces.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### GetActiveAdapterInfo {#GetActiveAdapterInfo}

<p>Returns information on the current active adapter, if it exists.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>adapter</code></td>
            <td>
                <code><a class='link' href='#AdapterInfo'>AdapterInfo</a>?</code>
            </td>
        </tr></table>

### RequestDiscovery {#RequestDiscovery}

<p>If <code>discovery</code> is true, active discovery is requested.
When requesting discovery, general discovery for BR/EDR and LE will be
active and newly discovered devices will be reported via
RemoteDeviceDelegate.OnDeviceUpdate().</p>
<p>Discovery may be active when not reqested.
If an error occurs when starting discovery, it is reflected in <code>status</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>discovery</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### GetKnownRemoteDevices {#GetKnownRemoteDevices}

<p>Retrieve the set of known remote devices.
Note: These devices are not guaranteed to still be reachable.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>devices</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RemoteDevice'>RemoteDevice</a>&gt;</code>
            </td>
        </tr></table>

### SetName {#SetName}

<p>Sets the public Bluetooth name for this device, or resets to the default
name if <code>name</code> is not present.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### SetDeviceClass {#SetDeviceClass}

<p>Set the Device Class for the active Bluetooth adapter.
Values are defined in https://www.bluetooth.com/specifications/assigned-numbers/baseband</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_class</code></td>
            <td>
                <code><a class='link' href='#DeviceClass'>DeviceClass</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### SetDiscoverable {#SetDiscoverable}

<p>Set the discoverability of this device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>discoverable</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### Connect {#Connect}

<p>Attempt to connect to the remote <code>device_id</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### Disconnect {#Disconnect}

<p>Disconnect a previously-connected device.
Note: This does not remove a device bond, see Control::Forget.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### Pair {#Pair}

<p>Initiate a pairing to the remote <code>id</code> with the given <code>options</code>. Returns an error
variant of fuchsia.bluetooth.Status if no connected peer with <code>id</code> is found or the pairing
procedure fails. If already paired, this will do nothing unless the pairing is over LE and
the PairingOptions.le_security_level is more secure than the current security level.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#PeerId'>PeerId</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#PairingOptions'>PairingOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### Forget {#Forget}

<p>Forget <code>device_id</code> completely, removing all bonding information.
This will disconnect a device if it is connected.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>

### SetIOCapabilities {#SetIOCapabilities}

<p>Set local IO Capabilities to use during pairing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='#InputCapabilityType'>InputCapabilityType</a></code>
            </td>
        </tr><tr>
            <td><code>output</code></td>
            <td>
                <code><a class='link' href='#OutputCapabilityType'>OutputCapabilityType</a></code>
            </td>
        </tr></table>



### OnActiveAdapterChanged {#OnActiveAdapterChanged}

<p>Sent when the active adapter has been updated. If <code>active_adapter</code> is
null, then no adapter is currently active.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>adapter</code></td>
            <td>
                <code><a class='link' href='#AdapterInfo'>AdapterInfo</a>?</code>
            </td>
        </tr></table>

### OnAdapterUpdated {#OnAdapterUpdated}

<p>Sent when an adapter has been updated.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>adapter</code></td>
            <td>
                <code><a class='link' href='#AdapterInfo'>AdapterInfo</a></code>
            </td>
        </tr></table>

### OnAdapterRemoved {#OnAdapterRemoved}

<p>Sent when an adapter with the given <code>identifier</code> has been removed from
the system.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### OnDeviceUpdated {#OnDeviceUpdated}

<p>Sent when a peer is updated.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr></table>

### OnDeviceRemoved {#OnDeviceRemoved}

<p>Sent when a peer is removed.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

## PairingDelegate {#PairingDelegate}
*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#55)*


### OnPairingRequest {#OnPairingRequest}

<p>Called for most pairing requests. The delegate must respond with “true” or “false” to
either accept or reject the pairing request. If the pairing method requires a passkey
this is returned as well.</p>
<p>Any response from this method will be ignored if the OnPairingComplete
event has already been sent for <code>device</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr><tr>
            <td><code>method</code></td>
            <td>
                <code><a class='link' href='#PairingMethod'>PairingMethod</a></code>
            </td>
        </tr><tr>
            <td><code>displayed_passkey</code></td>
            <td>
                <code>string?</code>
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
                <code>string?</code>
            </td>
        </tr></table>

### OnPairingComplete {#OnPairingComplete}

<p>Called if the pairing procedure for the device with the given ID is completed.
This can be due to successful completion or an error (e.g. due to cancellation
by the peer, a timeout, or disconnection) which is indicated by <code>status</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr></table>



### OnRemoteKeypress {#OnRemoteKeypress}

<p>Called to notify keypresses from the peer device during pairing using
PairingMethod.PASSKEY_DISPLAY.</p>
<p>This event is used to provide key press events to the delegate for a responsive user
experience as the user types the passkey on the peer device. This event will be called
once for each key-press.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>keypress</code></td>
            <td>
                <code><a class='link' href='#PairingKeypressType'>PairingKeypressType</a></code>
            </td>
        </tr></table>



### OnLocalKeypress {#OnLocalKeypress}

<p>The delegate can send this event to notify the peer of local keypresses
during pairing using PairingMethod.PASSKEY_ENTRY.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>keypress</code></td>
            <td>
                <code><a class='link' href='#PairingKeypressType'>PairingKeypressType</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### SecurityProperties {#SecurityProperties}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#7)*





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

### RemoteKey {#RemoteKey}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>security_properties</code></td>
            <td>
                <code><a class='link' href='#SecurityProperties'>SecurityProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LocalKey {#LocalKey}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#23)*





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

### LTK {#LTK}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='#RemoteKey'>RemoteKey</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key_size</code></td>
            <td>
                <code>uint8</code>
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

### LEConnectionParameters {#LEConnectionParameters}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#37)*





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

### LEData {#LEData}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#49)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>address</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>address_type</code></td>
            <td>
                <code><a class='link' href='#AddressType'>AddressType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>connection_parameters</code></td>
            <td>
                <code><a class='link' href='#LEConnectionParameters'>LEConnectionParameters</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ltk</code></td>
            <td>
                <code><a class='link' href='#LTK'>LTK</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>irk</code></td>
            <td>
                <code><a class='link' href='#RemoteKey'>RemoteKey</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>csrk</code></td>
            <td>
                <code><a class='link' href='#RemoteKey'>RemoteKey</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BREDRData {#BREDRData}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#71)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>address</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>piconet_leader</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>services</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_key</code></td>
            <td>
                <code><a class='link' href='#LTK'>LTK</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BondingData {#BondingData}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#89)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_address</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>le</code></td>
            <td>
                <code><a class='link' href='#LEData'>LEData</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bredr</code></td>
            <td>
                <code><a class='link' href='#BREDRData'>BREDRData</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HostData {#HostData}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#108)*



<p>Represents persistent local host data.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>irk</code></td>
            <td>
                <code><a class='link' href='#LocalKey'>LocalKey</a>?</code>
            </td>
            <td><p>The local Identity Resolving Key used by a bt-host device to generate Resolvable Private
Addresses when privacy is enabled.</p>
<p>NOTE: This key is distributed to LE peers during pairing procedures. The client must take
care to assign an IRK that consistent with the local bt-host identity.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AdapterInfo {#AdapterInfo}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#11)*



<p>Bluetooth controller and its associated host-subsystem state that is present
on the current platform.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>UUID that uniquely identifies this adapter on the current system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>technology</code></td>
            <td>
                <code><a class='link' href='#TechnologyType'>TechnologyType</a></code>
            </td>
            <td><p>The Bluetooth technologies that are supported by this adapter.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Public Bluetooth device address which can be displayed to the user.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#AdapterState'>AdapterState</a>?</code>
            </td>
            <td><p>The current adapter state. This field is only present when an AdapterInfo
is obtained via the Control and ControlDelegate interfaces. If present,
all optional members of <code>state</code> will also be present.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AdapterState {#AdapterState}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#29)*



<p>Contains static global information about a local Bluetooth adapter,
including its current state.  Each adapter instance represents a physical</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>local_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>discoverable</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Bool'>Bool</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>discovering</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Bool'>Bool</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceClass {#DeviceClass}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#50)*



<p>Device Class represents the Major and Minor Device Class and Service Class of an adapter
Values are defined in https://www.bluetooth.com/specifications/assigned-numbers/baseband</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RemoteDevice {#RemoteDevice}
*Defined in [fuchsia.bluetooth.control/remote_device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/remote_device.fidl#77)*



<p>Represents a remote BR/EDR, LE, or dual-mode BR/EDR/LE device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Uniquely identifies this device on the current system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Bluetooth device address that identifies this remote device. Clients
should display this field to the user when <code>name</code> is not available.</p>
<p>NOTE: Clients should use the <code>identifier</code> field to distinguish between
remote devices instead of using their address.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>technology</code></td>
            <td>
                <code><a class='link' href='#TechnologyType'>TechnologyType</a></code>
            </td>
            <td><p>The Bluetooth technologies that are supported by this device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The name of the remote device if present or known.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>appearance</code></td>
            <td>
                <code><a class='link' href='#Appearance'>Appearance</a></code>
            </td>
            <td><p>The LE appearance property. Present if this is a LE device and the
appearance information was obtained over advertising and/or GATT.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rssi</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Int8'>Int8</a>?</code>
            </td>
            <td><p>The most recently obtained advertising signal strength for this device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_power</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Int8'>Int8</a>?</code>
            </td>
            <td><p>The most recently obtained transmission power for this device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>connected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not a BR/EDR and/or LE connection exists between the local
adapter and this device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bonded</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not a bond exists between the local adapter and this device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>The list of service UUIDs known to be published on this remote device.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### AddressType {#AddressType}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#43)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LE_PUBLIC</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LE_RANDOM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>BREDR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### InputCapabilityType {#InputCapabilityType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#11)*

<p>Input and Output Capabilities for pairing exchanges.
See Volume 3, Part C, Table 5.3 and 5.4</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONFIRMATION</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYBOARD</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### OutputCapabilityType {#OutputCapabilityType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISPLAY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### PairingMethod {#PairingMethod}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#24)*

<p>Different types required by the Security Manager for pairing methods.
Bluetooth SIG has different requirements for different device capabilities.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONSENT</code></td>
            <td><code>0</code></td>
            <td><p>The user is asked to accept or reject pairing.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_DISPLAY</code></td>
            <td><code>1</code></td>
            <td><p>The user is shown a 6-digit numerical passkey which they must enter on the
peer device.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_COMPARISON</code></td>
            <td><code>2</code></td>
            <td><p>The user is shown a 6-digit numerical passkey which will also shown on the
peer device. The user must compare the passkeys and accept the pairing if
the passkeys match.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_ENTRY</code></td>
            <td><code>3</code></td>
            <td><p>The user is asked to enter a 6-digit passkey.</p>
</td>
        </tr></table>

### PairingKeypressType {#PairingKeypressType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#41)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DIGIT_ENTERED</code></td>
            <td><code>0</code></td>
            <td><p>The user has entered a single digit.</p>
</td>
        </tr><tr>
            <td><code>DIGIT_ERASED</code></td>
            <td><code>1</code></td>
            <td><p>The user has erased a single digit.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_CLEARED</code></td>
            <td><code>2</code></td>
            <td><p>The user has cleared the entire passkey.</p>
</td>
        </tr><tr>
            <td><code>PASSKEY_ENTERED</code></td>
            <td><code>3</code></td>
            <td><p>The user has finished entering the passkey.</p>
</td>
        </tr></table>

### PairingSecurityLevel {#PairingSecurityLevel}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_options.fidl#9)*

<p>The security level required for this pairing - corresponds to the security
levels defined in the Security Manager Protocol in Vol 3, Part H, Section 2.3.1</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ENCRYPTED</code></td>
            <td><code>1</code></td>
            <td><p>Encrypted without MITM protection (unauthenticated)</p>
</td>
        </tr><tr>
            <td><code>AUTHENTICATED</code></td>
            <td><code>2</code></td>
            <td><p>Encrypted with MITM protection (authenticated), although this level of security does not
fully protect against passive eavesdroppers</p>
</td>
        </tr></table>

### Appearance {#Appearance}
Type: <code>uint16</code>

*Defined in [fuchsia.bluetooth.control/remote_device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/remote_device.fidl#14)*

<p>Possible values for the LE Appearance property which describes the external
appearance of a
device at a high level.
(See the Bluetooth assigned-numbers document:
https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.characteristic.gap.appearance.xml)</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PHONE</code></td>
            <td><code>64</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMPUTER</code></td>
            <td><code>128</code></td>
            <td></td>
        </tr><tr>
            <td><code>WATCH</code></td>
            <td><code>192</code></td>
            <td></td>
        </tr><tr>
            <td><code>WATCH_SPORTS</code></td>
            <td><code>193</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLOCK</code></td>
            <td><code>256</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISPLAY</code></td>
            <td><code>320</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOTE_CONTROL</code></td>
            <td><code>384</code></td>
            <td></td>
        </tr><tr>
            <td><code>EYE_GLASSES</code></td>
            <td><code>448</code></td>
            <td></td>
        </tr><tr>
            <td><code>TAG</code></td>
            <td><code>512</code></td>
            <td></td>
        </tr><tr>
            <td><code>KEYRING</code></td>
            <td><code>576</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEDIA_PLAYER</code></td>
            <td><code>640</code></td>
            <td></td>
        </tr><tr>
            <td><code>BARCODE_SCANNER</code></td>
            <td><code>704</code></td>
            <td></td>
        </tr><tr>
            <td><code>THERMOMETER</code></td>
            <td><code>768</code></td>
            <td></td>
        </tr><tr>
            <td><code>THERMOMETER_EAR</code></td>
            <td><code>769</code></td>
            <td></td>
        </tr><tr>
            <td><code>HEART_RATE_SENSOR</code></td>
            <td><code>832</code></td>
            <td></td>
        </tr><tr>
            <td><code>HEART_RATE_SENSOR_BELT</code></td>
            <td><code>833</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLOOD_PRESSURE</code></td>
            <td><code>896</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLOOD_PRESSURE_ARM</code></td>
            <td><code>897</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLOOD_PRESSURE_WRIST</code></td>
            <td><code>898</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID</code></td>
            <td><code>960</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_KEYBOARD</code></td>
            <td><code>961</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_MOUSE</code></td>
            <td><code>962</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_JOYSTICK</code></td>
            <td><code>963</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_GAMEPAD</code></td>
            <td><code>964</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_DIGITIZER_TABLET</code></td>
            <td><code>965</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_CARD_READER</code></td>
            <td><code>966</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_DIGITAL_PEN</code></td>
            <td><code>967</code></td>
            <td></td>
        </tr><tr>
            <td><code>HID_BARCODE_SCANNER</code></td>
            <td><code>968</code></td>
            <td></td>
        </tr><tr>
            <td><code>GLUCOSE_METER</code></td>
            <td><code>1024</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNING_WALKING_SENSOR</code></td>
            <td><code>1088</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNING_WALKING_SENSOR_IN_SHOE</code></td>
            <td><code>1089</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNING_WALKING_SENSOR_ON_SHOE</code></td>
            <td><code>1090</code></td>
            <td></td>
        </tr><tr>
            <td><code>RUNNING_WALKING_SENSOR_ON_HIP</code></td>
            <td><code>1091</code></td>
            <td></td>
        </tr><tr>
            <td><code>CYCLING</code></td>
            <td><code>1152</code></td>
            <td></td>
        </tr><tr>
            <td><code>CYCLING_COMPUTER</code></td>
            <td><code>1153</code></td>
            <td></td>
        </tr><tr>
            <td><code>CYCLING_SPEED_SENSOR</code></td>
            <td><code>1154</code></td>
            <td></td>
        </tr><tr>
            <td><code>CYCLING_CADENCE_SENSOR</code></td>
            <td><code>1155</code></td>
            <td></td>
        </tr><tr>
            <td><code>CYCLING_POWER_SENSOR</code></td>
            <td><code>1156</code></td>
            <td></td>
        </tr><tr>
            <td><code>CYCLING_SPEED_AND_CADENCE_SENSOR</code></td>
            <td><code>1157</code></td>
            <td></td>
        </tr><tr>
            <td><code>PULSE_OXIMETER</code></td>
            <td><code>3136</code></td>
            <td></td>
        </tr><tr>
            <td><code>PULSE_OXIMETER_FINGERTIP</code></td>
            <td><code>3137</code></td>
            <td></td>
        </tr><tr>
            <td><code>PULSE_OXIMETER_WRIST</code></td>
            <td><code>3138</code></td>
            <td></td>
        </tr><tr>
            <td><code>WEIGHT_SCALE</code></td>
            <td><code>3200</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERSONAL_MOBILITY</code></td>
            <td><code>3264</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERSONAL_MOBILITY_WHEELCHAIR</code></td>
            <td><code>3265</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERSONAL_MOBILITY_SCOOTER</code></td>
            <td><code>3266</code></td>
            <td></td>
        </tr><tr>
            <td><code>GLUCOSE_MONITOR</code></td>
            <td><code>3328</code></td>
            <td></td>
        </tr><tr>
            <td><code>SPORTS_ACTIVITY</code></td>
            <td><code>5184</code></td>
            <td></td>
        </tr><tr>
            <td><code>SPORTS_ACTIVITY_LOCATION_DISPLAY</code></td>
            <td><code>5185</code></td>
            <td></td>
        </tr><tr>
            <td><code>SPORTS_ACTIVITY_LOCATION_AND_NAV_DISPLAY</code></td>
            <td><code>5186</code></td>
            <td></td>
        </tr><tr>
            <td><code>SPORTS_ACTIVITY_LOCATION_POD</code></td>
            <td><code>5187</code></td>
            <td></td>
        </tr><tr>
            <td><code>SPORTS_ACTIVITY_LOCATION_AND_NAV_POD</code></td>
            <td><code>5188</code></td>
            <td></td>
        </tr></table>

### TechnologyType {#TechnologyType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/remote_device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/remote_device.fidl#70)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LOW_ENERGY</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CLASSIC</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DUAL_MODE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### PairingOptions {#PairingOptions}


*Defined in [fuchsia.bluetooth.control/pairing_options.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_options.fidl#20)*

<p>Parameters that give a caller more fine-grained control over the pairing process. All of the
fields of this table are optional and pairing can still succeed if none of them are set.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>le_security_level</code></td>
            <td>
                <code><a class='link' href='#PairingSecurityLevel'>PairingSecurityLevel</a></code>
            </td>
            <td><p>Only relevant for LE. If present, determines the Security Manager security level to pair
with. If not present, defaults to PairingSecurityLevel.AUTHENTICATED.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>non_bondable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If not present or false, the pairing will default to bondable mode. Otherwise, setting this
parameter to true will initiate a non-bondable pairing.</p>
<p>TODO(fxb/42403): Only implemented for LE transport. Support this for BR/EDR.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>transport</code></td>
            <td>
                <code><a class='link' href='#TechnologyType'>TechnologyType</a></code>
            </td>
            <td><p>If transport is LOW_ENERGY or CLASSIC, pairing will be performed over the transport
corresponding to the specified technology, which must already be connected. If transport
is not present or DUAL_MODE, the pairing will be performed over whichever transport is
connected, and defaults to LE for dual-mode connections.</p>
</td>
        </tr></table>











