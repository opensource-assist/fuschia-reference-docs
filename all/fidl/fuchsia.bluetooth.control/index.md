Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.control


## **PROTOCOLS**

## Control {:#Control}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#56)*

 Primary Bluetooth control service to access bluetooth

### IsBluetoothAvailable {:#IsBluetoothAvailable}

 Returns whether or not Bluetooth is currently available on the system.

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

### SetPairingDelegate {:#SetPairingDelegate}

 Registers a delegate to handle pairing requests.
 Indicate the capability type of the PairingDelegate using `in` and `out`.
 If your input/output capability is variable, call this function when it
 changes to update.
 Setting a pairing delegate closes the previously assigned pairing Delegate.

 To disable pairing, set `delegate` to null.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>delegate</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#PairingDelegate'>PairingDelegate</a>?</code>
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

### GetAdapters {:#GetAdapters}

 Returns information about all local adapters that are known to the system.

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
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.control/index.html#AdapterInfo'>AdapterInfo</a>&gt;?</code>
            </td>
        </tr></table>

### SetActiveAdapter {:#SetActiveAdapter}

 Sets the local adapter with the given `identifier` to act as the backing
 adapter for all Bluetooth interfaces.

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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### GetActiveAdapterInfo {:#GetActiveAdapterInfo}

 Returns information on the current active adapter, if it exists.

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
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#AdapterInfo'>AdapterInfo</a>?</code>
            </td>
        </tr></table>

### RequestDiscovery {:#RequestDiscovery}

 If `discovery` is true, active discovery is requested.
 When requesting discovery, general discovery for BR/EDR and LE will be
 active and newly discovered devices will be reported via
 RemoteDeviceDelegate.OnDeviceUpdate().

 Discovery may be active when not reqested.
 If an error occurs when starting discovery, it is reflected in `status`.

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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### GetKnownRemoteDevices {:#GetKnownRemoteDevices}

 Retrieve the set of known remote devices.
 Note: These devices are not guaranteed to still be reachable.

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
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteDevice'>RemoteDevice</a>&gt;</code>
            </td>
        </tr></table>

### SetName {:#SetName}

 Sets the public Bluetooth name for this device, or resets to the default
 name if `name` is not present.

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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### SetDeviceClass {:#SetDeviceClass}

 Set the Device Class for the active Bluetooth adapter.
 Values are defined in https://www.bluetooth.com/specifications/assigned-numbers/baseband

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_class</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#DeviceClass'>DeviceClass</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### SetDiscoverable {:#SetDiscoverable}

 Set the discoverability of this device.

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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### Connect {:#Connect}

 Attempt to connect to the remote `device_id`.

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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### Disconnect {:#Disconnect}

 Disconnect a previously-connected device.
 Note: This does not remove a device bond, see Control::Forget.

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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### Forget {:#Forget}

 Forgets `device_id` completely, removing all bonding information.
 This will disconnect a device if it is connected.

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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### SetIOCapabilities {:#SetIOCapabilities}

 Set local IO Capabilities to use during pairing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#InputCapabilityType'>InputCapabilityType</a></code>
            </td>
        </tr><tr>
            <td><code>output</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#OutputCapabilityType'>OutputCapabilityType</a></code>
            </td>
        </tr></table>



### OnActiveAdapterChanged {:#OnActiveAdapterChanged}

 Sent when the active adapter has been updated. If `active_adapter` is
 null, then no adapter is currently active.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>adapter</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#AdapterInfo'>AdapterInfo</a>?</code>
            </td>
        </tr></table>

### OnAdapterUpdated {:#OnAdapterUpdated}

 Sent when an adapter has been updated.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>adapter</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#AdapterInfo'>AdapterInfo</a></code>
            </td>
        </tr></table>

### OnAdapterRemoved {:#OnAdapterRemoved}

 Sent when an adapter with the given `identifier` has been removed from
 the system.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### OnDeviceUpdated {:#OnDeviceUpdated}

 Sent when a peer is updated.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr></table>

### OnDeviceRemoved {:#OnDeviceRemoved}

 Sent when a peer is removed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

## PairingDelegate {:#PairingDelegate}
*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#55)*


### OnPairingRequest {:#OnPairingRequest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr><tr>
            <td><code>method</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#PairingMethod'>PairingMethod</a></code>
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

### OnPairingComplete {:#OnPairingComplete}


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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>



### OnRemoteKeypress {:#OnRemoteKeypress}


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
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#PairingKeypressType'>PairingKeypressType</a></code>
            </td>
        </tr></table>



### OnLocalKeypress {:#OnLocalKeypress}




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
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#PairingKeypressType'>PairingKeypressType</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### SecurityProperties {:#SecurityProperties}
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

### RemoteKey {:#RemoteKey}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>security_properties</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#SecurityProperties'>SecurityProperties</a></code>
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

### LocalKey {:#LocalKey}
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

### LTK {:#LTK}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteKey'>RemoteKey</a></code>
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

### LEConnectionParameters {:#LEConnectionParameters}
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

### LEData {:#LEData}
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
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#AddressType'>AddressType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>connection_parameters</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#LEConnectionParameters'>LEConnectionParameters</a>?</code>
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
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#LTK'>LTK</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>irk</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteKey'>RemoteKey</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>csrk</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteKey'>RemoteKey</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BREDRData {:#BREDRData}
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
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#LTK'>LTK</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BondingData {:#BondingData}
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
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#LEData'>LEData</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bredr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#BREDRData'>BREDRData</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HostData {:#HostData}
*Defined in [fuchsia.bluetooth.control/bonding.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/bonding.fidl#108)*



 Represents persistent local host data.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>irk</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#LocalKey'>LocalKey</a>?</code>
            </td>
            <td> The local Identity Resolving Key used by a bt-host device to generate Resolvable Private
 Addresses when privacy is enabled.

 NOTE: This key is distributed to LE peers during pairing procedures. The client must take
 care to assign an IRK that consistent with the local bt-host identity.
</td>
            <td>No default</td>
        </tr>
</table>

### AdapterInfo {:#AdapterInfo}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#11)*



 Bluetooth controller and its associated host-subsystem state that is present
 on the current platform.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
            <td> UUID that uniquely identifies this adapter on the current system.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>technology</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#TechnologyType'>TechnologyType</a></code>
            </td>
            <td> The Bluetooth technologies that are supported by this adapter.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Public Bluetooth device address which can be displayed to the user.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#AdapterState'>AdapterState</a>?</code>
            </td>
            <td> The current adapter state. This field is only present when an AdapterInfo
 is obtained via the Control and ControlDelegate interfaces. If present,
 all optional members of `state` will also be present.
</td>
            <td>No default</td>
        </tr>
</table>

### AdapterState {:#AdapterState}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#29)*



 Contains static global information about a local Bluetooth adapter,
 including its current state.  Each adapter instance represents a physical


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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Bool'>Bool</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>discovering</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Bool'>Bool</a>?</code>
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

### DeviceClass {:#DeviceClass}
*Defined in [fuchsia.bluetooth.control/control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/control.fidl#50)*



 Device Class represents the Major and Minor Device Class and Service Class of an adapter
 Values are defined in https://www.bluetooth.com/specifications/assigned-numbers/baseband


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

### RemoteDevice {:#RemoteDevice}
*Defined in [fuchsia.bluetooth.control/remote_device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/remote_device.fidl#77)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>technology</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#TechnologyType'>TechnologyType</a></code>
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
            <td><code>appearance</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html#Appearance'>Appearance</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rssi</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Int8'>Int8</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_power</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Int8'>Int8</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>connected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bonded</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### AddressType {:#AddressType}
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

### InputCapabilityType {:#InputCapabilityType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#11)*



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

### OutputCapabilityType {:#OutputCapabilityType}
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

### PairingMethod {:#PairingMethod}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#24)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONSENT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PASSKEY_DISPLAY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PASSKEY_COMPARISON</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PASSKEY_ENTRY</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### PairingKeypressType {:#PairingKeypressType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/pairing_delegate.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/pairing_delegate.fidl#41)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DIGIT_ENTERED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DIGIT_ERASED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PASSKEY_CLEARED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PASSKEY_ENTERED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### Appearance {:#Appearance}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.control/remote_device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.control/remote_device.fidl#14)*



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

### TechnologyType {:#TechnologyType}
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










