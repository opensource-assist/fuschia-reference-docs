Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.host


## **PROTOCOLS**

## Host {:#Host}
*Defined in [fuchsia.bluetooth.host/host.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/connectivity/bluetooth/fidl/host.fidl#14)*

 Interface for interacting with a Bluetooth host device (bt-host)

### RequestLowEnergyCentral {:#RequestLowEnergyCentral}

 The following methods fulfill a given interface request. bt-host device
 will start processing FIDL messages. If the request cannot be fulfilled,
 the bt-host device will close its end of the given channel.

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

 Shuts down the host, ending all active Bluetooth procedures:

 * All FIDL interface handles associated with this host are closed and all
   connections initiated via FIDL clients are severed.
 * All scan, discovery, and advertising procedures are stopped.
 * Bonded devices are cleared and removed from the auto-connect lists.
 * Auto-connected peripherals are disconnected.

 This effectively resets the host to its initial state and the host remains
 available for future requests.

 The Host will continue to send OnDeviceUpdated events as procedures get
 terminated.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetInfo {:#GetInfo}

 Returns information about the Bluetooth adapter managed by this host.

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

 Returns a list of all known connectable devices, included those that are
 currently connected and/or bonded. This list does not include
 non-connectable devices such as LE broadcasters.

 Notes:

 - When used in the GAP central role (BR/EDR or LE) the listed devices are
 obtained during discovery and connection procedures. While in the
 peripheral role, this will contain devices that have successfully initiated
 connections to this host.

 - This list contains connectable devices that are discovered or connected
 via other interfaces obtained using the interface request methods declared
 above.

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

 Sets the local name for this adapter.

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

 Sets the device class for this adapter.

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

 Initiates a general discovery procedure for BR/EDR and LE devices. On success, discovered
 devices will be reported via AdapterDelegate.OnDeviceDiscovered().

 On the LE transport, only general-discoverable and connectable peripherals will be reported.

 Discovery will continue until it is terminated via StopDiscovery() or if the proxy to the
 Adapter gets disconnected. If the device does not support BR/EDR, only LE
 discovery will be performed.

 An OnDeviceUpdated event will be sent when the discovery procedures are
 started.

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

 Terminates discovery if one was started via StartDiscovery(). The AdapterDelegate will stop
 receiving device discovery notifications.

 NOTE: If another client is performing discovery (e.g. via its own le.Central interface handle),
 then the system will continue performing device discovery even if this method results in
 success.

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

 Sets whether this host should be connectable.

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

 Sets whether this host should be discoverable.

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

 Establish a BR/EDR and/or LE connection to the remote device with identifier `device_id`:

   - If the device is known to support the BR/EDR transport then a logical link over that
     transport will be established to the device. If the connection attempt is successful,
     local services registered using "RequestProfile()" will be available to the peer.
     Traditional services discovered on the peer will be notified to local services
     asynchronously.

   - If the device is known to support the LE transport then a logical link over that
     transport will be established to the device. If the connection attempt is successful,
     GATT services in the local database (populated via RequestGattServer()) will become
     available to the peer. Similarly, remote GATT services that are discovered on the
     peer will become available to holders of a gatt.Client capability and to device drivers
     that can bind to the bt-gatt-svc class of devices.

 The result of the procedure will be communicated via `status`. If the remote device
 supports both BR/EDR and LE transports and a link cannot be established over both, then an
 error Status will be returned and neither transport will be connected.

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

 Enable or disable a passive LE background scan. When enabled, the bt-host
 device will continuously perform a passive LE scan in the background when
 no device discovery sessions are active and accept connection requests from
 bonded peripherals.

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

 Assigns the pairing delegate that will respond to authentication challenges using the given
 I/O capabilities. Setting a pairing delegate cancels any on-going pairing procedure started
 using a previous delegate. Pairing requests will be rejected if no PairingDelegate has been
 assigned.

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

 Adds existing bonded devices to the host. The host will be configured to automatically connect
 to these devices when they are in range and connectable. Future connections will be encrypted
 using the provided bonding data.

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

 Notifies when the adapter state changes.



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

 Events that are sent when a connectable device is added, updated, or
 removed as a result of connection and discovery procedures.



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

 Notifies when bonding data for a device has been updated.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.control/index.html'>fuchsia.bluetooth.control</a>/<a class='link' href='../fuchsia.bluetooth.control/index.html#BondingData'>BondingData</a></code>
            </td>
        </tr></table>















