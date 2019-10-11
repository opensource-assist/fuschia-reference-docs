Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.gatt


## **PROTOCOLS**

## RemoteService {:#RemoteService}
*Defined in [fuchsia.bluetooth.gatt/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/client.fidl#9)*


### DiscoverCharacteristics {:#DiscoverCharacteristics}

 Returns the characteristics and characteristic descriptors that belong to
 this service.

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

 Reads the value of the characteristic with `id` and returns it in the
 reply. If `status` indicates an error `value` will be empty.

 If the characteristic has a long value (i.e. larger than the current MTU)
 this method will return only the first (MTU - 1) bytes of the value. Use
 ReadLongCharacteristic() to read larger values or starting at a non-zero
 offset.

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

 Reads the complete value of a characteristic with the given `id`. This
 procedure should be used if the characteristic is known to have a value
 that can not be read in a single request.

 Returns up to `max_bytes` octets of the characteristic value starting at
 the given `offset`.

 This may return an error if:
   a. `max_bytes` is 0;
   b. The `offset` is invalid;
   c. The characteristic does not have a long value;
   d. The server does not support the long read procedure.

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

 Writes |value| to the characteristic with |id|. This operation may return
 an error if:
   a. The size of |value| exceeds the current MTU.
   b. The characteristic referred to by |id| does not have the 'write'
      property.

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

 Writes |value| to the characteristic with |id|, beginning at |offset|.
 This procedure should be used if the value to be written is too long to
 fit in a single request or needs to be written at an offset. This may
 return an error if:
   a. The |offset| is invalid;
   b. The server does not support the long write procedure.

 Long Writes require multiple messages to the remote service and take longer
 to execute than Short Writes. It is not recommended to send a short write
 while a long write is in process to the same id and data range. The order
 of the responses from this function signify the order in which the remote
 service received them, not necessarily the order in which it is called.

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

 Writes `value` to the characteristic with `id` without soliciting an
 acknowledgement from the peer. This method has no response and its delivery
 cannot be confirmed.

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

 Reads the value of the characteristic descriptor with `id` and returns it
 in the reply. If `status` indicates an error, `value` can be ignored.

 If the descriptor has a long value (i.e. larger than the current MTU)
 this method will return only the first (MTU - 1) bytes of the value. Use
 ReadLongDescriptor() to read larger values or starting at a non-zero
 offset.

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

 Reads the complete value of a characteristic descriptor with the given `id`.
 This procedure should be used if the descriptor is known to have a value
 that can not be read in a single request.

 Returns up to `max_bytes` octets of the characteristic value starting at
 the given `offset`.

 This may return an error if:
   a. `max_bytes` is 0;
   b. The `offset` is invalid;
   c. The server does not support the long read procedure.

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

 Writes |value| to the characteristic descriptor with |id|. This operation
 may return an error if:
   a. The size of |value| exceeds the current MTU.
   b. |id| refers to an internally reserved descriptor type (e.g. the Client
      Characteristic Configuration descriptor).

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

 Writes |value| to the characteristic descriptor with |id|, beginning at
 |offset|. This procedure should be used if the value to be written is too
 long to fit in a single request or needs to be written at an offset. This
 may return an error if:
   a. The |offset| is invalid;
   b. The server does not support the long write procedure.
   c. |id| refers to an internally reserved descriptor type (e.g. the Client
      Characteristic Configuration descriptor).

 Long Writes require multiple messages to the remote service and take longer
 to execute than Short Writes. It is not recommended to send a short write
 while a long write is in process to the same id and data range. The order
 of the responses from this function signify the order in which the remote
 service received them, not necessarily the order in which it is called.

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

 Subscribe or unsubscribe to notifications/indications from the characteristic with
 the given `id`. Notifications or indications will be enabled if `enable` is
 true or disabled if `enable` is false and they have been enabled for this
 client.

 Either notifications or indications will be enabled depending on
 characteristic properties. Indications will be preferred if they are
 supported.

 This operation fails if the characteristic does not have the "notify" or
 "indicate" property or does not contain a Client Characteristic
 Configuration descriptor.

 On success, the OnCharacteristicValueUpdated event will be sent whenever
 the peer sends a notification or indication. The local host will
 automically confirm indications.

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

 Events:
 Called when a characteristic value notification or indication is received.



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

 Enumerates services found on the peer that this Client represents. Results
 can be restricted by specifying a list of UUIDs in `uuids`. The returned
 ServiceInfo structures will contain only basic information about each
 service and the `characteristics` and `includes` fields will be null.

 To further interact with services, clients must obtain a RemoteService
 handle by calling ConnectToService().

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

 Connects the RemoteService with the given identifier.

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

 Interface for responding to requests on a local service.

### OnCharacteristicConfiguration {:#OnCharacteristicConfiguration}

 Notifies the delegate when a remote device with `peer_id` enables or
 disables notifications or indications on the characteristic with the given
 `characteristic_id`.

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

 Called when a remote device issues a request to read the value of the
 of the characteristic or descriptor with given identifier. The delegate
 must respond to the request by returning the characteristic value. If the
 read request resulted in an error it should be returned in `error_code`.
 On success, `error_code` should be set to NO_ERROR and a `value` should be
 provided.

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

 Called when a remote device issues a request to write the value of the
 characteristic or descriptor with the given identifier.

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

 Called when a remote device issues a request to write the value of the
 characteristic with the given identifier. This can be called on a
 characteristic with the WRITE_WITHOUT_RESPONSE property.

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

 Interface for communicating with a published service.

### RemoveService {:#RemoveService}

 Removes the service that this interface instance corresponds to. Does
 nothing if the service is already removed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### NotifyValue {:#NotifyValue}

 Sends a notification carrying the `value` of the characteristic with the
 given `characteristic_id` to the device with `peer_id`.

 If `confirm` is true, then this method sends an indication instead. If the
 peer fails to confirm the indication, the link between the peer and the
 local adapter will be closed.

 This method has no effect if the peer has not enabled notifications or
 indications on the requested characteristic.

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

 Publishes the given service so that it is available to all remote peers.
 A LocalServiceDelegate must be provided over which to receive service requests.

 The caller must assign distinct identifiers to the characteristics and
 descriptors listed in `info`. These identifiers will be used in requests
 sent to `delegate`.

 `service` can be used to interact with the pubished service. If this
 service cannot be published then the handle for `service` will be closed.

 Returns the success or failure status of the call and a unique identifier
 that can be used to unregister the service.

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

## RemoteService {:#RemoteService}
*Defined in [fuchsia.bluetooth.gatt/client.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/client.fidl#9)*


### DiscoverCharacteristics {:#DiscoverCharacteristics}

 Returns the characteristics and characteristic descriptors that belong to
 this service.

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

 Reads the value of the characteristic with `id` and returns it in the
 reply. If `status` indicates an error `value` will be empty.

 If the characteristic has a long value (i.e. larger than the current MTU)
 this method will return only the first (MTU - 1) bytes of the value. Use
 ReadLongCharacteristic() to read larger values or starting at a non-zero
 offset.

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

 Reads the complete value of a characteristic with the given `id`. This
 procedure should be used if the characteristic is known to have a value
 that can not be read in a single request.

 Returns up to `max_bytes` octets of the characteristic value starting at
 the given `offset`.

 This may return an error if:
   a. `max_bytes` is 0;
   b. The `offset` is invalid;
   c. The characteristic does not have a long value;
   d. The server does not support the long read procedure.

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

 Writes |value| to the characteristic with |id|. This operation may return
 an error if:
   a. The size of |value| exceeds the current MTU.
   b. The characteristic referred to by |id| does not have the 'write'
      property.

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

 Writes |value| to the characteristic with |id|, beginning at |offset|.
 This procedure should be used if the value to be written is too long to
 fit in a single request or needs to be written at an offset. This may
 return an error if:
   a. The |offset| is invalid;
   b. The server does not support the long write procedure.

 Long Writes require multiple messages to the remote service and take longer
 to execute than Short Writes. It is not recommended to send a short write
 while a long write is in process to the same id and data range. The order
 of the responses from this function signify the order in which the remote
 service received them, not necessarily the order in which it is called.

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

 Writes `value` to the characteristic with `id` without soliciting an
 acknowledgement from the peer. This method has no response and its delivery
 cannot be confirmed.

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

 Reads the value of the characteristic descriptor with `id` and returns it
 in the reply. If `status` indicates an error, `value` can be ignored.

 If the descriptor has a long value (i.e. larger than the current MTU)
 this method will return only the first (MTU - 1) bytes of the value. Use
 ReadLongDescriptor() to read larger values or starting at a non-zero
 offset.

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

 Reads the complete value of a characteristic descriptor with the given `id`.
 This procedure should be used if the descriptor is known to have a value
 that can not be read in a single request.

 Returns up to `max_bytes` octets of the characteristic value starting at
 the given `offset`.

 This may return an error if:
   a. `max_bytes` is 0;
   b. The `offset` is invalid;
   c. The server does not support the long read procedure.

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

 Writes |value| to the characteristic descriptor with |id|. This operation
 may return an error if:
   a. The size of |value| exceeds the current MTU.
   b. |id| refers to an internally reserved descriptor type (e.g. the Client
      Characteristic Configuration descriptor).

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

 Writes |value| to the characteristic descriptor with |id|, beginning at
 |offset|. This procedure should be used if the value to be written is too
 long to fit in a single request or needs to be written at an offset. This
 may return an error if:
   a. The |offset| is invalid;
   b. The server does not support the long write procedure.
   c. |id| refers to an internally reserved descriptor type (e.g. the Client
      Characteristic Configuration descriptor).

 Long Writes require multiple messages to the remote service and take longer
 to execute than Short Writes. It is not recommended to send a short write
 while a long write is in process to the same id and data range. The order
 of the responses from this function signify the order in which the remote
 service received them, not necessarily the order in which it is called.

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

 Subscribe or unsubscribe to notifications/indications from the characteristic with
 the given `id`. Notifications or indications will be enabled if `enable` is
 true or disabled if `enable` is false and they have been enabled for this
 client.

 Either notifications or indications will be enabled depending on
 characteristic properties. Indications will be preferred if they are
 supported.

 This operation fails if the characteristic does not have the "notify" or
 "indicate" property or does not contain a Client Characteristic
 Configuration descriptor.

 On success, the OnCharacteristicValueUpdated event will be sent whenever
 the peer sends a notification or indication. The local host will
 automically confirm indications.

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

 Events:
 Called when a characteristic value notification or indication is received.



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

 Enumerates services found on the peer that this Client represents. Results
 can be restricted by specifying a list of UUIDs in `uuids`. The returned
 ServiceInfo structures will contain only basic information about each
 service and the `characteristics` and `includes` fields will be null.

 To further interact with services, clients must obtain a RemoteService
 handle by calling ConnectToService().

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

 Connects the RemoteService with the given identifier.

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

 Interface for responding to requests on a local service.

### OnCharacteristicConfiguration {:#OnCharacteristicConfiguration}

 Notifies the delegate when a remote device with `peer_id` enables or
 disables notifications or indications on the characteristic with the given
 `characteristic_id`.

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

 Called when a remote device issues a request to read the value of the
 of the characteristic or descriptor with given identifier. The delegate
 must respond to the request by returning the characteristic value. If the
 read request resulted in an error it should be returned in `error_code`.
 On success, `error_code` should be set to NO_ERROR and a `value` should be
 provided.

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

 Called when a remote device issues a request to write the value of the
 characteristic or descriptor with the given identifier.

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

 Called when a remote device issues a request to write the value of the
 characteristic with the given identifier. This can be called on a
 characteristic with the WRITE_WITHOUT_RESPONSE property.

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

 Interface for communicating with a published service.

### RemoveService {:#RemoveService}

 Removes the service that this interface instance corresponds to. Does
 nothing if the service is already removed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### NotifyValue {:#NotifyValue}

 Sends a notification carrying the `value` of the characteristic with the
 given `characteristic_id` to the device with `peer_id`.

 If `confirm` is true, then this method sends an indication instead. If the
 peer fails to confirm the indication, the link between the peer and the
 local adapter will be closed.

 This method has no effect if the peer has not enabled notifications or
 indications on the requested characteristic.

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

 Publishes the given service so that it is available to all remote peers.
 A LocalServiceDelegate must be provided over which to receive service requests.

 The caller must assign distinct identifiers to the characteristics and
 descriptors listed in `info`. These identifiers will be used in requests
 sent to `delegate`.

 `service` can be used to interact with the pubished service. If this
 service cannot be published then the handle for `service` will be closed.

 Returns the success or failure status of the call and a unique identifier
 that can be used to unregister the service.

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



 Represents encryption, authentication, and authorization permissions that can
 be assigned to a specific access permission.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>encryption_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the physical link must be encrypted to access this attribute.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>authentication_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the physical link must be authenticated to access this
 attribute.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>authorization_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the client needs to be authorized before accessing this
 attribute.
</td>
            <td>No default</td>
        </tr>
</table>

### AttributePermissions {:#AttributePermissions}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#41)*



 Specifies the access permissions for a specific attribute value.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>read</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td> Specifies whether or not an attribute has the read permission. If null,
 then the attribute value cannot be read. Otherwise, it can be read only if
 the permissions specified in the Permissions struct are satisfied.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>write</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td> Specifies whether or not an attribute has the write permission. If null,
 then the attribute value cannot be written. Otherwise, it be written only
 if the permissions specified in the Permissions struct are satisfied.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>update</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td> Specifies the security requirements for a client to subscribe to
 notifications or indications on a characteristic. A characteristic's
 support for notifications or indiciations is specified using the NOTIFY and
 INDICATE characteristic properties. If a local characteristic has one of
 these properties then this field can not be null. Otherwise, this field
 must be left as null.

 This field is ignored for Descriptors.
</td>
            <td>No default</td>
        </tr>
</table>

### ServiceInfo {:#ServiceInfo}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#76)*



 Represents a local or remote GATT service.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Uniquely identifies this GATT service. This value will be ignored for local
 services. Remote services will always have an identifier.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates whether this is a primary or secondary service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The 128-bit UUID that identifies the type of this service. This is a string
 in the canonical 8-4-4-4-12 format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>characteristics</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Characteristic'>Characteristic</a>&gt;?</code>
            </td>
            <td> The characteristics of this service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>includes</code></td>
            <td>
                <code>vector&lt;uint64&gt;?</code>
            </td>
            <td> Ids of other services that are included by this service.
</td>
            <td>No default</td>
        </tr>
</table>

### Characteristic {:#Characteristic}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#96)*



 Represents a local or remote GATT characteristic.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Uniquely identifies this characteristic within a service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The 128-bit UUID that identifies the type of this characteristic. This is a
 string in the canonical 8-4-4-4-12 format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The characteristic properties bitfield. See kProperty* above for possible
 values.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>permissions</code></td>
            <td>
                <code><a class='link' href='#AttributePermissions'>AttributePermissions</a>?</code>
            </td>
            <td> The attribute permissions of this characteristic. For remote
 characteristics, this value will be null until the permissions are
 discovered via read and write requests.

 For local characteristics, this value is mandatory.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Descriptor'>Descriptor</a>&gt;?</code>
            </td>
            <td> The descriptors of this characteristic.
</td>
            <td>No default</td>
        </tr>
</table>

### Descriptor {:#Descriptor}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#120)*



 Represents a local or remote GATT characteristic descriptor.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Uniquely identifies this descriptor within the characteristic that it
 belongs to.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The 128-bit UUID that identifies the type of this descriptor. This is a
 string in the canonical 8-4-4-4-12 format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>permissions</code></td>
            <td>
                <code><a class='link' href='#AttributePermissions'>AttributePermissions</a>?</code>
            </td>
            <td> The attribute permissions of this descriptor. For remote
 descriptors, this value will be null until the permissions are
 discovered via read and write requests.

 For local descriptors, this value is mandatory.
</td>
            <td>No default</td>
        </tr>
</table>

### SecurityRequirements {:#SecurityRequirements}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#27)*



 Represents encryption, authentication, and authorization permissions that can
 be assigned to a specific access permission.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>encryption_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the physical link must be encrypted to access this attribute.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>authentication_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the physical link must be authenticated to access this
 attribute.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>authorization_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the client needs to be authorized before accessing this
 attribute.
</td>
            <td>No default</td>
        </tr>
</table>

### AttributePermissions {:#AttributePermissions}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#41)*



 Specifies the access permissions for a specific attribute value.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>read</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td> Specifies whether or not an attribute has the read permission. If null,
 then the attribute value cannot be read. Otherwise, it can be read only if
 the permissions specified in the Permissions struct are satisfied.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>write</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td> Specifies whether or not an attribute has the write permission. If null,
 then the attribute value cannot be written. Otherwise, it be written only
 if the permissions specified in the Permissions struct are satisfied.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>update</code></td>
            <td>
                <code><a class='link' href='#SecurityRequirements'>SecurityRequirements</a>?</code>
            </td>
            <td> Specifies the security requirements for a client to subscribe to
 notifications or indications on a characteristic. A characteristic's
 support for notifications or indiciations is specified using the NOTIFY and
 INDICATE characteristic properties. If a local characteristic has one of
 these properties then this field can not be null. Otherwise, this field
 must be left as null.

 This field is ignored for Descriptors.
</td>
            <td>No default</td>
        </tr>
</table>

### ServiceInfo {:#ServiceInfo}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#76)*



 Represents a local or remote GATT service.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Uniquely identifies this GATT service. This value will be ignored for local
 services. Remote services will always have an identifier.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Indicates whether this is a primary or secondary service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The 128-bit UUID that identifies the type of this service. This is a string
 in the canonical 8-4-4-4-12 format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>characteristics</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Characteristic'>Characteristic</a>&gt;?</code>
            </td>
            <td> The characteristics of this service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>includes</code></td>
            <td>
                <code>vector&lt;uint64&gt;?</code>
            </td>
            <td> Ids of other services that are included by this service.
</td>
            <td>No default</td>
        </tr>
</table>

### Characteristic {:#Characteristic}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#96)*



 Represents a local or remote GATT characteristic.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Uniquely identifies this characteristic within a service.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The 128-bit UUID that identifies the type of this characteristic. This is a
 string in the canonical 8-4-4-4-12 format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The characteristic properties bitfield. See kProperty* above for possible
 values.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>permissions</code></td>
            <td>
                <code><a class='link' href='#AttributePermissions'>AttributePermissions</a>?</code>
            </td>
            <td> The attribute permissions of this characteristic. For remote
 characteristics, this value will be null until the permissions are
 discovered via read and write requests.

 For local characteristics, this value is mandatory.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Descriptor'>Descriptor</a>&gt;?</code>
            </td>
            <td> The descriptors of this characteristic.
</td>
            <td>No default</td>
        </tr>
</table>

### Descriptor {:#Descriptor}
*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#120)*



 Represents a local or remote GATT characteristic descriptor.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Uniquely identifies this descriptor within the characteristic that it
 belongs to.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The 128-bit UUID that identifies the type of this descriptor. This is a
 string in the canonical 8-4-4-4-12 format.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>permissions</code></td>
            <td>
                <code><a class='link' href='#AttributePermissions'>AttributePermissions</a>?</code>
            </td>
            <td> The attribute permissions of this descriptor. For remote
 descriptors, this value will be null until the permissions are
 discovered via read and write requests.

 For local descriptors, this value is mandatory.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ErrorCode {:#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#9)*

 Codes that can be returned in the `protocol_error_code` field of a
 bluetooth.Error.


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

### ErrorCode {:#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.gatt/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#9)*

 Codes that can be returned in the `protocol_error_code` field of a
 bluetooth.Error.


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
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/constants.fidl#7">MAX_VALUE_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#65">kPropertyBroadcast</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Possible values for the characteristic properties bitfield. These specify the
 GATT procedures that are allowed for a particular characteristic.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#66">kPropertyRead</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#67">kPropertyWriteWithoutResponse</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#68">kPropertyWrite</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#69">kPropertyNotify</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#70">kPropertyIndicate</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#71">kPropertyAuthenticatedSignedWrites</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#72">kPropertyReliableWrite</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#73">kPropertyWritableAuxiliaries</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/constants.fidl#7">MAX_VALUE_LENGTH</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#65">kPropertyBroadcast</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Possible values for the characteristic properties bitfield. These specify the
 GATT procedures that are allowed for a particular characteristic.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#66">kPropertyRead</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#67">kPropertyWriteWithoutResponse</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#68">kPropertyWrite</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#69">kPropertyNotify</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#70">kPropertyIndicate</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#71">kPropertyAuthenticatedSignedWrites</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#72">kPropertyReliableWrite</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.gatt/types.fidl#73">kPropertyWritableAuxiliaries</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

