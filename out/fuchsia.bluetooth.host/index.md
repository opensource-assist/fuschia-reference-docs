Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.host


## **PROTOCOLS**

## Host {:#Host}
*Defined in [fuchsia.bluetooth.host/host.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.host/host.fidl#16)*


### RequestLowEnergyCentral {:#RequestLowEnergyCentral}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>central</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.bluetooth.le/index.html'>fuchsia.bluetooth.le</a>/<a class='link' href='../fuchsia.bluetooth.le/index.html#Central'>Central</a>&gt;</code>
            </td>
        </tr></table>



### RequestLowEnergyPeripheral {:#RequestLowEnergyPeripheral}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peripheral</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.bluetooth.le/index.html'>fuchsia.bluetooth.le</a>/<a class='link' href='../fuchsia.bluetooth.le/index.html#Peripheral'>Peripheral</a>&gt;</code>
            </td>
        </tr></table>



### RequestGattServer {:#RequestGattServer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>server</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.bluetooth.gatt/index.html'>fuchsia.bluetooth.gatt</a>/<a class='link' href='../fuchsia.bluetooth.gatt/index.html#Server'>Server</a>&gt;</code>
            </td>
        </tr></table>



### RequestProfile {:#RequestProfile}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>profile</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html'>fuchsia.bluetooth.bredr</a>/<a class='link' href='../fuchsia.bluetooth.bredr/index.html#Profile'>Profile</a>&gt;</code>
            </td>
        </tr></table>



### Close {:#Close}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetInfo {:#GetInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#AdapterInfo'>AdapterInfo</a></code>
            </td>
        </tr></table>

### SetLocalData {:#SetLocalData}

 Assigns local data to this host.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>host_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#HostData'>HostData</a></code>
            </td>
        </tr></table>



### ListDevices {:#ListDevices}


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
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteDevice'>RemoteDevice</a>&gt;</code>
            </td>
        </tr></table>

### SetLocalName {:#SetLocalName}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>local_name</code></td>
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

### SetDeviceClass {:#SetDeviceClass}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_class</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#DeviceClass'>DeviceClass</a></code>
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

### StartDiscovery {:#StartDiscovery}


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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### StopDiscovery {:#StopDiscovery}


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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### SetConnectable {:#SetConnectable}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
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

### SetDiscoverable {:#SetDiscoverable}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
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

 Terminate all connections (BR/EDR or LE) to the remote peer with identifier `peer_id`.

 + request `peer_id` The identifier of the peer to disconnect.
 - response `status` Contains an error if either LE or BR/EDR transport fails to disconnect. Contains
                     success when both transports are successfully disconnected or if the peer is already
                     disconnected.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
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

 Deletes a peer from the Bluetooth host. If the peer is connected, it will be disconnected,
 then OnDeviceUpdated will be sent. OnDeviceRemoved will be sent. `device_id` will no longer
 refer to any peer, even if a device with the same address(es) is discovered again.

 Returns success after no peer exists that's identified by `device_id` (even if it didn't
 exist before Forget), failure if the peer specified by `device_id` could not be
 disconnected or deleted and still exists.

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

### EnableBackgroundScan {:#EnableBackgroundScan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### EnablePrivacy {:#EnablePrivacy}

 Enable or disable the LE privacy feature. When enabled, the bt-host device will use a private
 device address in all LE procedures. When disabled, the public identity address will be used
 instead (which is the default).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetPairingDelegate {:#SetPairingDelegate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#InputCapabilityType'>InputCapabilityType</a></code>
            </td>
        </tr><tr>
            <td><code>output</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#OutputCapabilityType'>OutputCapabilityType</a></code>
            </td>
        </tr><tr>
            <td><code>delegate</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#PairingDelegate'>PairingDelegate</a>?</code>
            </td>
        </tr></table>



### AddBondedDevices {:#AddBondedDevices}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>bonds</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#BondingData'>BondingData</a>&gt;</code>
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

### OnAdapterStateChanged {:#OnAdapterStateChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#AdapterState'>AdapterState</a></code>
            </td>
        </tr></table>

### OnDeviceUpdated {:#OnDeviceUpdated}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr></table>

### OnDeviceRemoved {:#OnDeviceRemoved}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

### OnNewBondingData {:#OnNewBondingData}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#BondingData'>BondingData</a></code>
            </td>
        </tr></table>















