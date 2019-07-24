Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.gatt


## **PROTOCOLS**

## RemoteService {:#RemoteService}
*Defined in [fuchsia.bluetooth.gatt/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/client.fidl#9)*


### DiscoverCharacteristics {:#DiscoverCharacteristics}


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
        </tr><tr>
            <td><code>characteristics</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Characteristic'>Characteristic</a>&gt;</code>
            </td>
        </tr></table>

### ReadCharacteristic {:#ReadCharacteristic}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
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
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>

### ReadLongCharacteristic {:#ReadLongCharacteristic}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>max_bytes</code></td>
            <td>
                <code>uint16</code>
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
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;[512]</code>
            </td>
        </tr></table>

### WriteCharacteristic {:#WriteCharacteristic}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
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

### WriteLongCharacteristic {:#WriteLongCharacteristic}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;[512]</code>
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

### WriteCharacteristicWithoutResponse {:#WriteCharacteristicWithoutResponse}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



### ReadDescriptor {:#ReadDescriptor}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
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
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>

### ReadLongDescriptor {:#ReadLongDescriptor}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>max_bytes</code></td>
            <td>
                <code>uint16</code>
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
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>

### WriteDescriptor {:#WriteDescriptor}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
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

### WriteLongDescriptor {:#WriteLongDescriptor}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;[512]</code>
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

### NotifyCharacteristic {:#NotifyCharacteristic}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>enable</code></td>
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

### OnCharacteristicValueUpdated {:#OnCharacteristicValueUpdated}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>

## Client {:#Client}
*Defined in [fuchsia.bluetooth.gatt/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/client.fidl#131)*


### ListServices {:#ListServices}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>uuids</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
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
            <td><code>services</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ServiceInfo'>ServiceInfo</a>&gt;</code>
            </td>
        </tr></table>

### ConnectToService {:#ConnectToService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>service</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RemoteService'>RemoteService</a>&gt;</code>
            </td>
        </tr></table>



## LocalServiceDelegate {:#LocalServiceDelegate}
*Defined in [fuchsia.bluetooth.gatt/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/server.fidl#10)*


### OnCharacteristicConfiguration {:#OnCharacteristicConfiguration}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>characteristic_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>notify</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>indicate</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnReadValue {:#OnReadValue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
        </tr></table>

### OnWriteValue {:#OnWriteValue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
        </tr></table>

### OnWriteWithoutResponse {:#OnWriteWithoutResponse}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>



## LocalService {:#LocalService}
*Defined in [fuchsia.bluetooth.gatt/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/server.fidl#36)*


### RemoveService {:#RemoveService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### NotifyValue {:#NotifyValue}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>characteristic_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>confirm</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## Server {:#Server}
*Defined in [fuchsia.bluetooth.gatt/server.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/server.fidl#54)*


### PublishService {:#PublishService}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ServiceInfo'>ServiceInfo</a></code>
            </td>
        </tr><tr>
            <td><code>delegate</code></td>
            <td>
                <code><a class='link' href='#LocalServiceDelegate'>LocalServiceDelegate</a></code>
            </td>
        </tr><tr>
            <td><code>service</code></td>
            <td>
                <code>request&lt;<a class='link' href='#LocalService'>LocalService</a>&gt;</code>
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



## **STRUCTS**

### SecurityRequirements {:#SecurityRequirements}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#27)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>encryption_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>authentication_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>authorization_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AttributePermissions {:#AttributePermissions}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#41)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>read</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>write</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>update</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ServiceInfo {:#ServiceInfo}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#76)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>characteristics</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Characteristic'>Characteristic</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>includes</code></td>
            <td>
                <code>vector&lt;uint64&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Characteristic {:#Characteristic}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#96)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>permissions</code></td>
            <td>
                <code><a class='link' href='#AttributePermissions'>AttributePermissions</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Descriptor'>Descriptor</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Descriptor {:#Descriptor}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#120)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>permissions</code></td>
            <td>
                <code><a class='link' href='#AttributePermissions'>AttributePermissions</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ErrorCode {:#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_ERROR</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_OFFSET</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_VALUE_LENGTH</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_PERMITTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/constants.fidl#7">MAX_VALUE_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#65">kPropertyBroadcast</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#66">kPropertyRead</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#67">kPropertyWriteWithoutResponse</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#68">kPropertyWrite</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#69">kPropertyNotify</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#70">kPropertyIndicate</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#71">kPropertyAuthenticatedSignedWrites</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#72">kPropertyReliableWrite</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#73">kPropertyWritableAuxiliaries</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

