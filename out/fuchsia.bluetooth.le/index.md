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
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.le/index.html#RemoteDevice'>RemoteDevice</a>&gt;</code>
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
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#RemoteDevice'>RemoteDevice</a>?</code>
            </td>
        </tr></table>

### StartScan {:#StartScan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>filter</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#ScanFilter'>ScanFilter</a>?</code>
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
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#RemoteDevice'>RemoteDevice</a></code>
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

## Peripheral {:#Peripheral}
*Defined in [fuchsia.bluetooth.le/peripheral.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/peripheral.fidl#10)*


### StartAdvertising {:#StartAdvertising}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>advertising_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#AdvertisingData'>AdvertisingData</a></code>
            </td>
        </tr><tr>
            <td><code>scan_result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#AdvertisingData'>AdvertisingData</a>?</code>
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

### StartAdvertisingDeprecated {:#StartAdvertisingDeprecated}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>advertising_data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#AdvertisingDataDeprecated'>AdvertisingDataDeprecated</a></code>
            </td>
        </tr><tr>
            <td><code>scan_result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#AdvertisingDataDeprecated'>AdvertisingDataDeprecated</a>?</code>
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

### StopAdvertising {:#StopAdvertising}


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
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#RemoteDevice'>RemoteDevice</a></code>
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
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.le/index.html#ServiceDataEntry'>ServiceDataEntry</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer_specific_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.le/index.html#ManufacturerSpecificDataEntry'>ManufacturerSpecificDataEntry</a>&gt;?</code>
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

### AdvertisingData {:#AdvertisingData}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#53)*





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
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.le/index.html#ServiceDataEntry'>ServiceDataEntry</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>manufacturer_specific_data</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.le/index.html#ManufacturerSpecificDataEntry'>ManufacturerSpecificDataEntry</a>&gt;?</code>
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
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#84)*





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
                <code><a class='link' href='../fuchsia.bluetooth.le/index.html#AdvertisingDataDeprecated'>AdvertisingDataDeprecated</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ScanFilter {:#ScanFilter}
*Defined in [fuchsia.bluetooth.le/types_deprecated.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.le/types_deprecated.fidl#103)*





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













