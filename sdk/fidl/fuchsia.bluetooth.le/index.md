Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.le


## **PROTOCOLS**

## Central {:#Central}
*Defined in [fuchsia.bluetooth.le/central.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/central.fidl#11)*


### GetPeripherals {:#GetPeripherals}


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

### GetPeripheral {:#GetPeripheral}


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

### StartScan {:#StartScan}


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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### StopScan {:#StopScan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### ConnectPeripheral {:#ConnectPeripheral}


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
                <code>request&lt;<a class='link' href='../fuchsia.bluetooth.gatt/index.html'>fuchsia.bluetooth.gatt</a>/<a class='link' href='../fuchsia.bluetooth.gatt/index.html#Client'>Client</a>&gt;</code>
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

### DisconnectPeripheral {:#DisconnectPeripheral}


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

### OnScanStateChanged {:#OnScanStateChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scanning</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### OnDeviceDiscovered {:#OnDeviceDiscovered}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#RemoteDevice'>RemoteDevice</a></code>
            </td>
        </tr></table>

### OnPeripheralDisconnected {:#OnPeripheralDisconnected}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>

## Connection {:#Connection}
*Defined in [fuchsia.bluetooth.le/peer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peer.fidl#33)*

 Protocol that represents the connection to a peer. This can be used to interact with GATT
 services and establish L2CAP channels.

## AdvertisingHandle {:#AdvertisingHandle}
*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#75)*

 Capability that is valid for the duration of advertising. The caller can close the handle to
 stop advertising. If the system internally stops advertising for any reason, the handle will be
 closed to communicate this to the client.

## Peripheral {:#Peripheral}
*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#78)*


### StartAdvertising {:#StartAdvertising}

 Start advertising as a LE peripheral. An empty response is sent to indicate when advertising
 has successfully initiated. If advertising cannot be initiated, then the response will
 contain a <a class='link' href='#PeripheralError'>PeripheralError</a>.

 This method can get called any number of times and successive calls can be made to
 reconfigure the advertising parameters. However only the most recent
 <a class='link' href='#AdvertisingHandle'>AdvertisingHandle</a> will remain valid.

 An instance of <a class='link' href='#Peripheral'>Peripheral</a> can only have one active advertisement at
 a time. Clients must obtain multiple Peripheral instances for multiple simultaneous
 advertisements.

 If the client closes its end of the <a class='link' href='#AdvertisingHandle'>AdvertisingHandle</a> channel,
 advertising will be stopped. If the handle is closed before the request is fulfilled,
 advertising will be briefly enabled before it is terminated.

 + request `parameters` Parameters used while configuring the advertising instance.
 + request `handle` Handle that remains valid for the duration of this advertising session.
 * error Returns a <a class='link' href='#PeripheralError'>PeripheralError</a> if advertising cannot be
         initiated. In this case the `handle` will be closed.

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

### OnPeerConnected {:#OnPeerConnected}

 Event delivered when a remote LE central initiates a connection to this Peripheral when
 connectable advertising is enabled via
 <a class='link' href='#Peripheral.StartAdvertising'>Peripheral.StartAdvertising</a>.

 The returned <a class='link' href='#Connection'>Connection</a> handle can be used to interact with the
 peer. It also represents a peripheral's ownership over the connection: the client can drop
 the handle to request a disconnection. Similarly, the handle is closed by the system to
 indicate that the connection to the peer has been lost.

 + request `peer` Information about the central that initiated the connection.
 + request `handle` Represents the connection.



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

### StartAdvertisingDeprecated {:#StartAdvertisingDeprecated}


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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>advertisement_id</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

### StopAdvertisingDeprecated {:#StopAdvertisingDeprecated}


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
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Status'>Status</a></code>
            </td>
        </tr></table>

### OnCentralConnected {:#OnCentralConnected}




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

### OnCentralDisconnected {:#OnCentralDisconnected}




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

### ServiceData {:#ServiceData}
*Defined in [fuchsia.bluetooth.le/advertising_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/advertising_data.fidl#10)*



 Entry in the `service_data` field of a <a class='link' href='#AdvertisingData'>AdvertisingData</a>.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>uuid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Uuid'>Uuid</a></code>
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

### ManufacturerData {:#ManufacturerData}
*Defined in [fuchsia.bluetooth.le/advertising_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/advertising_data.fidl#16)*



 Entry in the `manufacturer_data` field of a <a class='link' href='#AdvertisingData'>AdvertisingData</a>.


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

### Peripheral_StartAdvertising_Response {:#Peripheral_StartAdvertising_Response}
*Defined in [fuchsia.bluetooth.le/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ServiceDataEntry {:#ServiceDataEntry}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#10)*





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

### ManufacturerSpecificDataEntry {:#ManufacturerSpecificDataEntry}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#16)*





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

### AdvertisingDataDeprecated {:#AdvertisingDataDeprecated}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_power_level</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Int8'>Int8</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>appearance</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#UInt16'>UInt16</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ServiceDataEntry'>ServiceDataEntry</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer_specific_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ManufacturerSpecificDataEntry'>ManufacturerSpecificDataEntry</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>solicited_service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uris</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RemoteDevice {:#RemoteDevice}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#54)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identifier</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
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
            <td><code>advertising_data</code></td>
            <td>
                <code><a class='link' href='#AdvertisingDataDeprecated'>AdvertisingDataDeprecated</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ScanFilter {:#ScanFilter}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#73)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>service_data_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer_identifier</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#UInt16'>UInt16</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>connectable</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Bool'>Bool</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name_substring</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_path_loss</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Int8'>Int8</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PeripheralError {:#PeripheralError}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ADVERTISING_DATA_TOO_LONG</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>SCAN_RESPONSE_DATA_TOO_LONG</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_PARAMETERS</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>

### AdvertisingModeHint {:#AdvertisingModeHint}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#33)*

 A client can indicate the transmission rate of advertising packets by specifying a mode. The
 mode provides a hint to the system when configuring the controller with advertising interval and
 window parameters.

 The mode affects how quickly a scanner or central is able to discover the peripheral; however it
 can have an adverse effect on power consumption. While the system will try to honor a client's
 request, it is not guaranteed to do so.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>VERY_FAST</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAST</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>SLOW</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### AdvertisingData {:#AdvertisingData}


*Defined in [fuchsia.bluetooth.le/advertising_data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/advertising_data.fidl#23)*

 Represents advertising and scan response data that are transmitted by a LE peripheral or
 broadcaster.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Long or short name of the device.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>appearance</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Appearance'>Appearance</a></code>
            </td>
            <td> The appearance of the device.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>tx_power_level</code></td>
            <td>
                <code>int8</code>
            </td>
            <td> The radio transmit power level reported by an advertising peer. This field is disallowed
 when used with the Peripheral API.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>service_uuids</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#Uuid'>Uuid</a>&gt;</code>
            </td>
            <td> Service UUIDs.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>service_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ServiceData'>ServiceData</a>&gt;</code>
            </td>
            <td> Service data entries.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>manufacturer_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ManufacturerData'>ManufacturerData</a>&gt;</code>
            </td>
            <td> Manufacturer-specific data entries.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>uris</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td> String representing a URI to be advertised, as defined in [IETF STD 66](https://tools.ietf.org/html/std66).
 Each entry should be a UTF-8 string including the scheme. For more information, see:
 - https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml for allowed schemes;
 - https://www.bluetooth.com/specifications/assigned-numbers/uri-scheme-name-string-mapping
   for code-points used by the system to compress the scheme to save space in the payload.
</td>
        </tr></table>

### Peer {:#Peer}


*Defined in [fuchsia.bluetooth.le/peer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peer.fidl#11)*

 Represents a Bluetooth Low Energy peer that may act in the broadcaster, peripheral, or central
 role. The peer's role depends on whether it is obtained from the Central or Peripheral protocol.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth/index.html'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/index.html#PeerId'>PeerId</a></code>
            </td>
            <td> Uniquely identifies this peer on the current system.

 This field is always present.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether or not this peer is connectable. Non-connectable peers are typically in the LE
 broadcaster role.

 This field is always present.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>rssi</code></td>
            <td>
                <code>int8</code>
            </td>
            <td> The last observed RSSI of this peer.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>advertising_data</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td> Advertising and scan response data broadcast by this peer. Present in broadcasters and
 peripherals.
</td>
        </tr></table>

### AdvertisingParameters {:#AdvertisingParameters}


*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#49)*

 Represents the parameters for configuring advertisements.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td> The fields that will be encoded in the data section of advertising packets.

 This field is required.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>scan_response</code></td>
            <td>
                <code><a class='link' href='#AdvertisingData'>AdvertisingData</a></code>
            </td>
            <td> The fields that are to be sent in a scan response packet. Clients may use this to send
 additional data that does not fit inside an advertising packet on platforms that do not
 support the advertising data length extensions.

 If present advertisements will be configured to be scannable.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>mode_hint</code></td>
            <td>
                <code><a class='link' href='#AdvertisingModeHint'>AdvertisingModeHint</a></code>
            </td>
            <td> The desired advertising frequency. See <a class='link' href='#AdvertisingModeHint'>AdvertisingModeHint</a>.
 Defaults to <a class='link' href='#AdvertisingModeHint.SLOW'>AdvertisingModeHint.SLOW</a> if not present.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>connectable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If present and true then the controller will broadcast connectable advertisements which
 allows remote LE centrals to initiate a connection to the Peripheral. If false or otherwise
 not present then the advertisements will be non-connectable.
</td>
        </tr></table>



## **UNIONS**

### Peripheral_StartAdvertising_Result {:#Peripheral_StartAdvertising_Result}
*Defined in [fuchsia.bluetooth.le/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#19)*


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







