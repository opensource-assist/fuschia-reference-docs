Project: /_project.yaml
Book: /_book.yaml

# fuchsia.bluetooth.bredr


## **PROTOCOLS**

## Profile {:#Profile}
*Defined in [fuchsia.bluetooth.bredr/profile.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/profile.fidl#25)*

 Profile provides Bluetooth services a way to register a service definition,
 making that service discoverable by remote peers.  Registered services will receive
 L2CAP connections made to the services advertised in the definition, and can open
 connections to remote connected devices.  To discover possible connected
 devices, devices should use `AddSearch` to search any remote devices.

### AddService {:#AddService}

 Register a service. This service will be registered and discoverable with
 the Service Discovery Protocol server.
 The `security_level` provided here will be required before a connection is
 established.
 If `devices` is true, connections to the service's channels will create a
 device instead of producing an OnConnected event.
 Returns `status` for success or error.
 If successful, a unique `service_id` is returned to identify this service.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>definition</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#ServiceDefinition'>ServiceDefinition</a></code>
            </td>
        </tr><tr>
            <td><code>sec_level</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#SecurityLevel'>SecurityLevel</a></code>
            </td>
        </tr><tr>
            <td><code>devices</code></td>
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
            <td><code>service_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### AddSearch {:#AddSearch}

 Register a search for services on remote devices.  An `OnServiceFound`
 event will be produced each time a device is connected that has a service
 matching `service_uuid` with the additional attributes in `attr_ids`.
 The ProtocolDescriptor should be requested to obtain information to connect to a service.
 If `attr_ids` is empty, all attributes will be requested.
 See the SDP Specification (Core Spec 5.0, Vol 3, Part B, Section 5) and the
 relevant profile specification documents.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_uuid</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#ServiceClassProfileIdentifier'>ServiceClassProfileIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>attr_ids</code></td>
            <td>
                <code>vector&lt;uint16&gt;</code>
            </td>
        </tr></table>



### RemoveService {:#RemoveService}

 Removes a previously-registered service, disconnecting all clients.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### ConnectL2cap {:#ConnectL2cap}

 Connect a channel to the connected remote device `peer_id` using the
 protocol and channel listed. For L2CAP, dynamic PSMs can be specified.
 See the defined PSMs in `service.fidl`
 Returns the channel after it has been connected. `status` will indicate
 an error if the channel could not be connected.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>psm</code></td>
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
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;socket&gt;?</code>
            </td>
        </tr></table>

### OnConnected {:#OnConnected}

 Produced when a protocol channel is connected for this profile.
 `channel` contains the channel connected to, and information about the
 protocol is provided in `protocol`. All protocols supported internally will
 be handled, for example an RFCOMM socket will be provided instead of an
 L2CAP socket if the services protocol descriptor includes it.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>service_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#ProtocolDescriptor'>ProtocolDescriptor</a></code>
            </td>
        </tr></table>

### OnServiceFound {:#OnServiceFound}

 Produced when a search this client added finds a matching service on a remote
 device.  `peer_id` is the device the service was found on, and `profile` includes the
 Profile Descriptor which matches the `service_uuid`
 searched for, with the major and minor version reported by the remote device.
 `attributes` contains all attributes retrieved from the remote device.  It may
 include attributes not requested in the search.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peer_id</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>profile</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#ProfileDescriptor'>ProfileDescriptor</a></code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html#Attribute'>Attribute</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### DataElement {:#DataElement}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#DataElementType'>DataElementType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#DataElementData'>DataElementData</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ProtocolDescriptor {:#ProtocolDescriptor}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#75)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#ProtocolIdentifier'>ProtocolIdentifier</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>params</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html#DataElement'>DataElement</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ProfileDescriptor {:#ProfileDescriptor}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#138)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>profile_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#ServiceClassProfileIdentifier'>ServiceClassProfileIdentifier</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>major_version</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>minor_version</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Information {:#Information}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#145)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>language</code></td>
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
            <td><code>description</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Attribute {:#Attribute}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#161)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='../fuchsia.bluetooth.bredr/index.html#DataElement'>DataElement</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ServiceDefinition {:#ServiceDefinition}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#180)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service_class_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol_descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html#ProtocolDescriptor'>ProtocolDescriptor</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_protocol_descriptors</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>profile_descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html#ProfileDescriptor'>ProfileDescriptor</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>information</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html#Information'>Information</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_attributes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html#Attribute'>Attribute</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### SecurityLevel {:#SecurityLevel}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.bredr/profile.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/profile.fidl#11)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENCRYPTION_OPTIONAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENCRYPTION_REQUIRED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>MITM_PROTECTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>HIGH_STRENGTH</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### DataElementType {:#DataElementType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#8)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOTHING</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSIGNED_INTEGER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SIGNED_INTEGER</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>UUID</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>STRING</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>BOOLEAN</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>SEQUENCE</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALTERNATIVE</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### ProtocolIdentifier {:#ProtocolIdentifier}
Type: <code>uint16</code>

*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#39)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SDP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>RFCOMM</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ATT</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>OBEX</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>BNEP</code></td>
            <td><code>15</code></td>
            <td></td>
        </tr><tr>
            <td><code>HIDP</code></td>
            <td><code>17</code></td>
            <td></td>
        </tr><tr>
            <td><code>HardcopyControlChannel</code></td>
            <td><code>18</code></td>
            <td></td>
        </tr><tr>
            <td><code>HardcopyDataChannel</code></td>
            <td><code>20</code></td>
            <td></td>
        </tr><tr>
            <td><code>HardcopyNotification</code></td>
            <td><code>22</code></td>
            <td></td>
        </tr><tr>
            <td><code>AVCTP</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr><tr>
            <td><code>AVDTP</code></td>
            <td><code>25</code></td>
            <td></td>
        </tr><tr>
            <td><code>MCAPControlChannel</code></td>
            <td><code>30</code></td>
            <td></td>
        </tr><tr>
            <td><code>MCAPDataChannel</code></td>
            <td><code>31</code></td>
            <td></td>
        </tr><tr>
            <td><code>L2CAP</code></td>
            <td><code>256</code></td>
            <td></td>
        </tr></table>

### ServiceClassProfileIdentifier {:#ServiceClassProfileIdentifier}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#85)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SerialPort</code></td>
            <td><code>4353</code></td>
            <td></td>
        </tr><tr>
            <td><code>DialupNetworking</code></td>
            <td><code>4355</code></td>
            <td></td>
        </tr><tr>
            <td><code>ObexObjectPush</code></td>
            <td><code>4357</code></td>
            <td></td>
        </tr><tr>
            <td><code>ObexFileTransfer</code></td>
            <td><code>4358</code></td>
            <td></td>
        </tr><tr>
            <td><code>Headset</code></td>
            <td><code>4360</code></td>
            <td></td>
        </tr><tr>
            <td><code>HeadsetAudioGateway</code></td>
            <td><code>4370</code></td>
            <td></td>
        </tr><tr>
            <td><code>HeadsetHS</code></td>
            <td><code>4401</code></td>
            <td></td>
        </tr><tr>
            <td><code>AudioSource</code></td>
            <td><code>4362</code></td>
            <td></td>
        </tr><tr>
            <td><code>AudioSink</code></td>
            <td><code>4363</code></td>
            <td></td>
        </tr><tr>
            <td><code>AdvancedAudioDistribution</code></td>
            <td><code>4365</code></td>
            <td></td>
        </tr><tr>
            <td><code>AVRemoteControlTarget</code></td>
            <td><code>4364</code></td>
            <td></td>
        </tr><tr>
            <td><code>AVRemoteControl</code></td>
            <td><code>4366</code></td>
            <td></td>
        </tr><tr>
            <td><code>AVRemoteControlController</code></td>
            <td><code>4367</code></td>
            <td></td>
        </tr><tr>
            <td><code>PANU</code></td>
            <td><code>4373</code></td>
            <td></td>
        </tr><tr>
            <td><code>NAP</code></td>
            <td><code>4374</code></td>
            <td></td>
        </tr><tr>
            <td><code>GN</code></td>
            <td><code>4375</code></td>
            <td></td>
        </tr><tr>
            <td><code>Handsfree</code></td>
            <td><code>4382</code></td>
            <td></td>
        </tr><tr>
            <td><code>HandsfreeAudioGateway</code></td>
            <td><code>4383</code></td>
            <td></td>
        </tr><tr>
            <td><code>SIM_Access</code></td>
            <td><code>4397</code></td>
            <td></td>
        </tr><tr>
            <td><code>PhonebookPCE</code></td>
            <td><code>4398</code></td>
            <td></td>
        </tr><tr>
            <td><code>PhonebookPSE</code></td>
            <td><code>4399</code></td>
            <td></td>
        </tr><tr>
            <td><code>Phonebook</code></td>
            <td><code>4400</code></td>
            <td></td>
        </tr><tr>
            <td><code>MessageAccessServer</code></td>
            <td><code>4402</code></td>
            <td></td>
        </tr><tr>
            <td><code>MessageNotificationServer</code></td>
            <td><code>4403</code></td>
            <td></td>
        </tr><tr>
            <td><code>MessageAccessProfile</code></td>
            <td><code>4404</code></td>
            <td></td>
        </tr><tr>
            <td><code>MPSProfile</code></td>
            <td><code>4410</code></td>
            <td></td>
        </tr><tr>
            <td><code>MPSClass</code></td>
            <td><code>4411</code></td>
            <td></td>
        </tr><tr>
            <td><code>VideoSource</code></td>
            <td><code>4867</code></td>
            <td></td>
        </tr><tr>
            <td><code>VideoSink</code></td>
            <td><code>4868</code></td>
            <td></td>
        </tr><tr>
            <td><code>VideoDistribution</code></td>
            <td><code>4869</code></td>
            <td></td>
        </tr><tr>
            <td><code>HDP</code></td>
            <td><code>5120</code></td>
            <td></td>
        </tr><tr>
            <td><code>HDPSource</code></td>
            <td><code>5121</code></td>
            <td></td>
        </tr><tr>
            <td><code>HDPSink</code></td>
            <td><code>5122</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### DataElementData {:#DataElementData}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#20)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>integer</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>str</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uuid</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>sequence</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.bluetooth.bredr/index.html#DataElement'>DataElement</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#59">kPSM_SDP</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#60">kPSM_RFCOMM</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#61">kPSM_TCSBIN</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#62">kPSM_TCSBINCordless</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#63">kPSM_BNEP</a></td>
            <td>
                    <code>15</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#64">kPSM_HIDControl</a></td>
            <td>
                    <code>17</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#65">kPSM_HIDInterrupt</a></td>
            <td>
                    <code>19</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#66">kPSM_AVCTP</a></td>
            <td>
                    <code>23</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#67">kPSM_AVDTP</a></td>
            <td>
                    <code>25</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#68">kPSM_AVCTP_Browse</a></td>
            <td>
                    <code>27</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#69">kPSM_ATT</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#70">kPSM_3DSP</a></td>
            <td>
                    <code>33</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#71">kPSM_LE_IPSP</a></td>
            <td>
                    <code>35</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#72">kPSM_OTS</a></td>
            <td>
                    <code>37</code>
                </td>
                <td><code>int64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#168">ATTR_SERVICE_RECORD_HANDLE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#169">ATTR_SERVICE_CLASS_ID_LIST</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#170">ATTR_SERVICE_RECORD_STATE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#171">ATTR_SERVICE_ID</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#172">ATTR_PROTOCOL_DESCRIPTOR_LIST</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#173">ATTR_ADDITIONAL_PROTOCOL_DESCRIPTOR_LIST</a></td>
            <td>
                    <code>13</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#174">ATTR_BROWSE_GROUP_LIST</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#175">ATTR_LANGUAGE_BASE_ATTRIBUTE_ID_LIST</a></td>
            <td>
                    <code>6</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#176">ATTR_SERVICE_INFO_TIME_TO_LIVE</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#177">ATTR_SERVICE_AVAILABILITY</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#178">ATTR_BLUETOOTH_PROFILE_DESCRIPTOR_LIST</a></td>
            <td>
                    <code>9</code>
                </td>
                <td><code>uint16</code></td>
        </tr>
    
</table>
