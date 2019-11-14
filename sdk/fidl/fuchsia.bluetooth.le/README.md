[TOC]

# fuchsia.bluetooth.le


## **PROTOCOLS**

## Central {#Central}
*Defined in [fuchsia.bluetooth.le/central.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/central.fidl#11)*


### GetPeripherals {#GetPeripherals}

<p>Returns the list of peripherals that are known to the system from previous scan, connection,
and/or bonding procedures. The results can be filtered based on service UUIDs that are known to
be present on the peripheral.</p>
<p>This method only returns peripherals (i.e. connectable devices).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peripherals</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RemoteDevice'>RemoteDevice</a>&gt;</code>
            </td>
        </tr></table>

### GetPeripheral {#GetPeripheral}

<p>Returns information about a single peripheral that is known to the system from previous scan,
connection, and/or bonding procedures based on its unique identifier. Returns null if
<code>identifier</code> is not recognized.</p>

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
            <td><code>peripheral</code></td>
            <td>
                <code><a class='link' href='#RemoteDevice'>RemoteDevice</a>?</code>
            </td>
        </tr></table>

### StartScan {#StartScan}

<p>Initiates a scan session for nearby peripherals and broadcasters. Discovered devices will be
reported via CentralDelegate.OnDeviceDiscovered(). If a scan session is already in progress,
<code>filter</code> will replace the existing session's filter.</p>
<p>If <code>filter</code> is null or empty (i.e. none of its fields has been populated) then the delegate
will be notified for all discoverable devices that are found. This is not recommended; clients
should generally filter results by at least one of <code>filter.service_uuids</code>,
<code>filter.service_data</code>, and/or <code>filter.manufacturer_identifier</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>filter</code></td>
            <td>
                <code><a class='link' href='#ScanFilter'>ScanFilter</a>?</code>
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

### StopScan {#StopScan}

<p>Terminate a previously started scan session.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ConnectPeripheral {#ConnectPeripheral}

<p>Creates a connection to the peripheral device with the given identifier.
Returns the status of the operation in <code>status</code>.</p>
<p>On success, <code>gatt_client</code> will be bound and can be used for GATT client
role procedures. On failure, <code>gatt_client</code> will be closed and <code>status</code> will
indicate an error.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>gatt_client</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.bluetooth.gatt/'>fuchsia.bluetooth.gatt</a>/<a class='link' href='../fuchsia.bluetooth.gatt/#Client'>Client</a>&gt;</code>
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

### DisconnectPeripheral {#DisconnectPeripheral}

<p>Disconnects this Central's connection to the peripheral with the given identifier.</p>

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

### OnScanStateChanged {#OnScanStateChanged}

<p>Called when the scan state changes, e.g. when a scan session terminates due to a call to
Central.StopScan() or another unexpected condition.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scanning</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### OnDeviceDiscovered {#OnDeviceDiscovered}

<p>Called for each peripheral/broadcaster that is discovered during a scan session. <code>rssi</code>
contains the received signal strength of the advertising packet that generated this event, if
available.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr></table>

### OnPeripheralDisconnected {#OnPeripheralDisconnected}

<p>Called when this Central's connection to a peripheral with the given identifier is terminated.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

## Connection {#Connection}
*Defined in [fuchsia.bluetooth.le/peer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peer.fidl#33)*

<p>Protocol that represents the connection to a peer. This can be used to interact with GATT
services and establish L2CAP channels.</p>

## AdvertisingHandle {#AdvertisingHandle}
*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#79)*

<p>Capability that is valid for the duration of advertising. The caller can close the handle to
stop advertising. If the system internally stops advertising for any reason, the handle will be
closed to communicate this to the client.</p>

## Peripheral {#Peripheral}
*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#83)*


### StartAdvertising {#StartAdvertising}

<p>Start advertising as a LE peripheral. An empty response is sent to indicate when advertising
has successfully initiated. If advertising cannot be initiated, then the response will
contain a <a class='link' href='#PeripheralError'>PeripheralError</a>.</p>
<p>This method can get called any number of times and successive calls can be made to
reconfigure the advertising parameters. However only the most recent
<a class='link' href='#AdvertisingHandle'>AdvertisingHandle</a> will remain valid.</p>
<p>An instance of <a class='link' href='#Peripheral'>Peripheral</a> can only have one active advertisement at
a time. Clients must obtain multiple Peripheral instances for multiple simultaneous
advertisements.</p>
<p>If the client closes its end of the <a class='link' href='#AdvertisingHandle'>AdvertisingHandle</a> channel,
advertising will be stopped. If the handle is closed before the request is fulfilled,
advertising will be briefly enabled before it is terminated.</p>
<ul>
<li>request <code>parameters</code> Parameters used while configuring the advertising instance.</li>
<li>request <code>handle</code> Handle that remains valid for the duration of this advertising session.</li>
</ul>
<ul>
<li>error Returns a <a class='link' href='#PeripheralError'>PeripheralError</a> if advertising cannot be
initiated. In this case the <code>handle</code> will be closed.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>parameters</code></td>
            <td>
                <code><a class='link' href='#AdvertisingParameters'>AdvertisingParameters</a></code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AdvertisingHandle'>AdvertisingHandle</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Peripheral_StartAdvertising_Result'>Peripheral_StartAdvertising_Result</a></code>
            </td>
        </tr></table>

### OnPeerConnected {#OnPeerConnected}

<p>Event delivered when a remote LE central initiates a connection to this Peripheral when
connectable advertising is enabled via
<a class='link' href='#Peripheral.StartAdvertising'>Peripheral.StartAdvertising</a>.</p>
<p>The returned <a class='link' href='#Connection'>Connection</a> handle can be used to interact with the
peer. It also represents a peripheral's ownership over the connection: the client can drop
the handle to request a disconnection. Similarly, the handle is closed by the system to
indicate that the connection to the peer has been lost.</p>
<ul>
<li>request <code>peer</code> Information about the central that initiated the connection.</li>
<li>request <code>handle</code> Represents the connection.</li>
</ul>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer</code></td>
            <td>
                <code><a class='link' href='#Peer'>Peer</a></code>
            </td>
        </tr><tr>
            <td><code>connection</code></td>
            <td>
                <code><a class='link' href='#Connection'>Connection</a></code>
            </td>
        </tr></table>

### StartAdvertisingDeprecated {#StartAdvertisingDeprecated}

<p>[[DEPRECATED]]</p>
<p>Starts sending advertisements based on the given parameters.
  - <code>advertising_data</code>: The advertising data that should be included in the payload.
  - <code>scan_result</code>: The scan result that will be returned when the advertisement is
                   scanned.  Setting this will mark the advertisement set as scannable.
  - <code>connectable</code>: when true, this advertisement will be marked as connectable.
NOTE: connections can be made to a GATT server even if this is not set.
  - <code>interval_ms</code>: The requested interval to advertise this set at in milliseconds.
                minimum 20, maximum 10,000,000 (almost 3 hours). A reasonable
default is 1 second (1000).
  - <code>anonymous</code>: if true, the address of this device will not be included</p>
<p>If the <code>tx_power_level</code> is set in either AdvertisingData, it will be replaced with
the actual TX Power level reported by the adapter, or included in the extended header
of the Advertising PDU to save advertising space.</p>
<p>If <code>scan_result</code> and <code>advertising_data</code> are both set, legacy advertising will be used,
which limits the size of the advertising data.</p>
<p>This request will fail if:
  - The <code>service_uuids</code> field of <code>advertising_data</code> contains a UUID that does not match
    a GATT service that was previously registered by this application;
  - If the provided advertising data cannot fit within the advertising payload MTU that
    is supported on the current platform and parameters.
  - If <code>anonymous</code> advertising is requested but the controller cannot support it.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>advertising_data</code></td>
            <td>
                <code><a class='link' href='#AdvertisingDataDeprecated'>AdvertisingDataDeprecated</a></code>
            </td>
        </tr><tr>
            <td><code>scan_result</code></td>
            <td>
                <code><a class='link' href='#AdvertisingDataDeprecated'>AdvertisingDataDeprecated</a>?</code>
            </td>
        </tr><tr>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>interval_ms</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>anonymous</code></td>
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
        </tr><tr>
            <td><code>advertisement_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### StopAdvertisingDeprecated {#StopAdvertisingDeprecated}

<p>[[DEPRECATED]]</p>
<p>Stop an advertising session that was previously started by this application.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>advertisement_id</code></td>
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

### OnCentralConnected {#OnCentralConnected}

<p>[[DEPRECATED]]</p>
<p>Called when a remote central device has connected to a connectable advertisement.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>advertisement_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>central</code></td>
            <td>
                <code><a class='link' href='#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr></table>

### OnCentralDisconnected {#OnCentralDisconnected}

<p>[[DEPRECATED]]</p>
<p>Called when a remote central previously connected to this application is disconnected.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## **STRUCTS**

### ServiceData {#ServiceData}
*Defined in [fuchsia.bluetooth.le/advertising_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/advertising_data.fidl#10)*



<p>Entry in the <code>service_data</code> field of a <a class='link' href='#AdvertisingData'>AdvertisingData</a>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>uuid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Uuid'>Uuid</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ManufacturerData {#ManufacturerData}
*Defined in [fuchsia.bluetooth.le/advertising_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/advertising_data.fidl#16)*



<p>Entry in the <code>manufacturer_data</code> field of a <a class='link' href='#AdvertisingData'>AdvertisingData</a>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>company_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Peripheral_StartAdvertising_Response {#Peripheral_StartAdvertising_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ServiceDataEntry {#ServiceDataEntry}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#10)*



<p>[[DEPRECATED]]</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>uuid</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ManufacturerSpecificDataEntry {#ManufacturerSpecificDataEntry}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#16)*



<p>[[DEPRECATED]]</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>company_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AdvertisingDataDeprecated {#AdvertisingDataDeprecated}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#23)*



<p>Represents advertising and scan response data advertised by a broadcaster or peripheral.
[[DEPRECATED]]</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>Name of the device.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_power_level</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Int8'>Int8</a>?</code>
            </td>
            <td><p>The radio transmission power level reported in the advertisement.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>appearance</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#UInt16'>UInt16</a>?</code>
            </td>
            <td><p>The appearance reported in the advertisemet.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>List of service UUIDs reported in the advertisement.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ServiceDataEntry'>ServiceDataEntry</a>&gt;?</code>
            </td>
            <td><p>Service data included in the advertisement.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer_specific_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ManufacturerSpecificDataEntry'>ManufacturerSpecificDataEntry</a>&gt;?</code>
            </td>
            <td><p>Manufacturer specific data entries.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>solicited_service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>Service UUIDs that were solicited in the advertisement. Peripherals can invite centrals that
expose certain services to connect to them using service solicitation.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>uris</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>URIs included in the advertising packet.
These are full URIs (they are encoded/decoded automatically)</p>
</td>
            <td>No default</td>
        </tr>
</table>

### RemoteDevice {#RemoteDevice}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#54)*



<p>Represents a remote Bluetooth Low Energy device. A RemoteDevice can represent a central,
broadcaster, or peripheral based on the API from which it was received.
[[DEPRECATED]]</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Identifier that uniquely identifies this device on the current system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not this device is connectable. Non-connectable devices are typically acting in the
LE broadcaster role.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rssi</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Int8'>Int8</a>?</code>
            </td>
            <td><p>The last known RSSI of this device, if known.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>advertising_data</code></td>
            <td>
                <code><a class='link' href='#AdvertisingDataDeprecated'>AdvertisingDataDeprecated</a>?</code>
            </td>
            <td><p>Advertising data broadcast by this device if this device is a broadcaster or peripheral.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ScanFilter {#ScanFilter}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#73)*



<p>Filter parameters for use during a scan. A discovered peripheral or broadcaster will be reported
to applications only if it satisfies all of the provided filter parameters. Null fields will be
ignored.
[[DEPRECATED]]</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>Filter based on advertised service UUIDs. A peripheral that advertises at least one of the
entries in <code>service_uuids</code> will satisfy this filter.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_data_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td><p>Filter based on service data containing one of the given UUIDs.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer_identifier</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#UInt16'>UInt16</a>?</code>
            </td>
            <td><p>Filter based on a company identifier present in the manufacturer data. If this filter parameter
is set, then the advertising payload must contain manufacturer specific data with the provided
company identifier to satisfy this filter.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>connectable</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Bool'>Bool</a>?</code>
            </td>
            <td><p>Filter based on whether or not a device is connectable. For example, a client that is only
interested in peripherals that it can connect to can set this to true. Similarly a client can
scan only for braodcasters by setting this to false.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name_substring</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>Filter results based on a portion of the advertised device name.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_path_loss</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Int8'>Int8</a>?</code>
            </td>
            <td><p>Filter results based on the path loss of the radio wave. A device that matches this filter must
satisfy the following:</p>
<ol>
<li>Radio transmission power level and received signal strength must be available for the path
loss calculation;</li>
<li>The calculated path loss value must be less than, or equal to, <code>max_path_loss</code>.</li>
</ol>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PeripheralError {#PeripheralError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>1</code></td>
            <td><p>The operation or parameters requested are not supported on the current hardware.</p>
</td>
        </tr><tr>
            <td><code>ADVERTISING_DATA_TOO_LONG</code></td>
            <td><code>2</code></td>
            <td><p>The provided advertising data exceeds the maximum allowed length when encoded.</p>
</td>
        </tr><tr>
            <td><code>SCAN_RESPONSE_DATA_TOO_LONG</code></td>
            <td><code>3</code></td>
            <td><p>The provided scan response data exceeds the maximum allowed length when encoded.</p>
</td>
        </tr><tr>
            <td><code>INVALID_PARAMETERS</code></td>
            <td><code>4</code></td>
            <td><p>The requested parameters are invalid.</p>
</td>
        </tr><tr>
            <td><code>ABORTED</code></td>
            <td><code>5</code></td>
            <td><p>The request to start advertising was aborted, for example by issuing a new request with new
parameters.</p>
</td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>6</code></td>
            <td><p>Advertising could not be initiated due to a hardware or system error.</p>
</td>
        </tr></table>

### AdvertisingModeHint {#AdvertisingModeHint}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#37)*

<p>A client can indicate the transmission rate of advertising packets by specifying a mode. The
mode provides a hint to the system when configuring the controller with advertising interval and
window parameters.</p>
<p>The mode affects how quickly a scanner or central is able to discover the peripheral; however it
can have an adverse effect on power consumption. While the system will try to honor a client's
request, it is not guaranteed to do so.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>VERY_FAST</code></td>
            <td><code>1</code></td>
            <td><p>Advertise with a very short interval and window for fast discovery at the cost of higher
power consumption. This corresponds to a 30-60ms interval on the 1M PHYs and 90-180ms on the
coded PHY.</p>
</td>
        </tr><tr>
            <td><code>FAST</code></td>
            <td><code>2</code></td>
            <td><p>Advertise with a short interval and window that uses less power than <code>VERY_FAST</code>.
This corresponds to a 100-150ms interval on the 1M PHYs and 300-450ms on the coded PHY.</p>
</td>
        </tr><tr>
            <td><code>SLOW</code></td>
            <td><code>3</code></td>
            <td><p>Advertise with a moderate interval and window. This corresponds to 1-1.2s on the 1M PHYs and 3s
on the coded PHY.</p>
</td>
        </tr></table>



## **TABLES**

### AdvertisingData {#AdvertisingData}


*Defined in [fuchsia.bluetooth.le/advertising_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/advertising_data.fidl#23)*

<p>Represents advertising and scan response data that are transmitted by a LE peripheral or
broadcaster.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Long or short name of the device.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>appearance</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Appearance'>Appearance</a></code>
            </td>
            <td><p>The appearance of the device.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>tx_power_level</code></td>
            <td>
                <code>int8</code>
            </td>
            <td><p>The radio transmit power level reported by an advertising peer. This field is disallowed
when used with the Peripheral API.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Uuid'>Uuid</a>&gt;</code>
            </td>
            <td><p>Service UUIDs.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>service_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ServiceData'>ServiceData</a>&gt;</code>
            </td>
            <td><p>Service data entries.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>manufacturer_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ManufacturerData'>ManufacturerData</a>&gt;</code>
            </td>
            <td><p>Manufacturer-specific data entries.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>uris</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>String representing a URI to be advertised, as defined in <a href="https://tools.ietf.org/html/std66">IETF STD 66</a>.
Each entry should be a UTF-8 string including the scheme. For more information, see:</p>
<ul>
<li>https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml for allowed schemes;</li>
<li>https://www.bluetooth.com/specifications/assigned-numbers/uri-scheme-name-string-mapping
for code-points used by the system to compress the scheme to save space in the payload.</li>
</ul>
</td>
        </tr></table>

### Peer {#Peer}


*Defined in [fuchsia.bluetooth.le/peer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peer.fidl#11)*

<p>Represents a Bluetooth Low Energy peer that may act in the broadcaster, peripheral, or central
role. The peer's role depends on whether it is obtained from the Central or Peripheral protocol.</p>


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
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether or not this peer is connectable. Non-connectable peers are typically in the LE
broadcaster role.</p>
<p>This field is always present.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>rssi</code></td>
            <td>
                <code>int8</code>
            </td>
            <td><p>The last observed RSSI of this peer.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>advertising_data</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td><p>Advertising and scan response data broadcast by this peer. Present in broadcasters and
peripherals.</p>
</td>
        </tr></table>

### AdvertisingParameters {#AdvertisingParameters}


*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#53)*

<p>Represents the parameters for configuring advertisements.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td><p>The fields that will be encoded in the data section of advertising packets.</p>
<p>This field is required.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>scan_response</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td><p>The fields that are to be sent in a scan response packet. Clients may use this to send
additional data that does not fit inside an advertising packet on platforms that do not
support the advertising data length extensions.</p>
<p>If present advertisements will be configured to be scannable.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>mode_hint</code></td>
            <td>
                <code><a class='link' href='#AdvertisingModeHint'>AdvertisingModeHint</a></code>
            </td>
            <td><p>The desired advertising frequency. See <a class='link' href='#AdvertisingModeHint'>AdvertisingModeHint</a>.
Defaults to <a class='link' href='#AdvertisingModeHint.SLOW'>AdvertisingModeHint.SLOW</a> if not present.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>If present and true then the controller will broadcast connectable advertisements which
allows remote LE centrals to initiate a connection to the Peripheral. If false or otherwise
not present then the advertisements will be non-connectable.</p>
</td>
        </tr></table>



## **UNIONS**

### Peripheral_StartAdvertising_Result {#Peripheral_StartAdvertising_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Peripheral_StartAdvertising_Response'>Peripheral_StartAdvertising_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#PeripheralError'>PeripheralError</a></code>
            </td>
            <td></td>
        </tr></table>







