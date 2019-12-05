[TOC]

# fuchsia.bluetooth.bredr


## **PROTOCOLS**

## Profile {#Profile}
*Defined in [fuchsia.bluetooth.bredr/profile.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/profile.fidl#25)*

<p>Profile provides Bluetooth services a way to register a service definition,
making that service discoverable by remote peers.  Registered services will receive
L2CAP connections made to the services advertised in the definition, and can open
connections to remote connected devices.  To discover possible connected
devices, devices should use <code>AddSearch</code> to search any remote devices.</p>

### AddService {#AddService}

<p>Register a service. This service will be registered and discoverable with
the Service Discovery Protocol server.
The <code>security_level</code> provided here will be required before a connection is
established.
If <code>devices</code> is true, connections to the service's channels will create a
device instead of producing an OnConnected event.
Returns <code>status</code> for success or error.
If successful, a unique <code>service_id</code> is returned to identify this service.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>definition</code></td>
            <td>
                <code><a class='link' href='#ServiceDefinition'>ServiceDefinition</a></code>
            </td>
        </tr><tr>
            <td><code>sec_level</code></td>
            <td>
                <code><a class='link' href='#SecurityLevel'>SecurityLevel</a></code>
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
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>service_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### AddSearch {#AddSearch}

<p>Register a search for services on remote devices.  An <code>OnServiceFound</code>
event will be produced each time a device is connected that has a service
matching <code>service_uuid</code> with the additional attributes in <code>attr_ids</code>.
The ProtocolDescriptor should be requested to obtain information to connect to a service.
If <code>attr_ids</code> is empty, all attributes will be requested.
See the SDP Specification (Core Spec 5.0, Vol 3, Part B, Section 5) and the
relevant profile specification documents.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_uuid</code></td>
            <td>
                <code><a class='link' href='#ServiceClassProfileIdentifier'>ServiceClassProfileIdentifier</a></code>
            </td>
        </tr><tr>
            <td><code>attr_ids</code></td>
            <td>
                <code>vector&lt;uint16&gt;</code>
            </td>
        </tr></table>



### RemoveService {#RemoveService}

<p>Removes a previously-registered service, disconnecting all clients.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### ConnectL2cap {#ConnectL2cap}

<p>Connect a channel to the connected remote device <code>peer_id</code> using the
protocol and channel listed. For L2CAP, dynamic PSMs can be specified.
See the defined PSMs in <code>service.fidl</code>
Returns the channel after it has been connected. <code>status</code> will indicate
an error if the channel could not be connected.</p>

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
                <code><a class='link' href='../fuchsia.bluetooth/'>fuchsia.bluetooth</a>/<a class='link' href='../fuchsia.bluetooth/#Status'>Status</a></code>
            </td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;socket&gt;?</code>
            </td>
        </tr></table>

### OnConnected {#OnConnected}

<p>Produced when a protocol channel is connected for this profile.
<code>channel</code> contains the channel connected to, and information about the
protocol is provided in <code>protocol</code>. All protocols supported internally will
be handled, for example an RFCOMM socket will be provided instead of an
L2CAP socket if the services protocol descriptor includes it.</p>



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
                <code><a class='link' href='#ProtocolDescriptor'>ProtocolDescriptor</a></code>
            </td>
        </tr></table>

### OnServiceFound {#OnServiceFound}

<p>Produced when a search this client added finds a matching service on a remote
device.  <code>peer_id</code> is the device the service was found on, and <code>profile</code> includes the
Profile Descriptor which matches the <code>service_uuid</code>
searched for, with the major and minor version reported by the remote device.
<code>attributes</code> contains all attributes retrieved from the remote device.  It may
include attributes not requested in the search.</p>



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
                <code><a class='link' href='#ProfileDescriptor'>ProfileDescriptor</a></code>
            </td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Attribute'>Attribute</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### DataElement {#DataElement}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#DataElementType'>DataElementType</a></code>
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
                <code><a class='link' href='#DataElementData'>DataElementData</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ProtocolDescriptor {#ProtocolDescriptor}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#75)*



<p>Identifies a communications protocol along with protocol-specific parameters.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#ProtocolIdentifier'>ProtocolIdentifier</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>params</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DataElement'>DataElement</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ProfileDescriptor {#ProfileDescriptor}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#138)*



<p>A description of a profile that this service conforms to.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>profile_id</code></td>
            <td>
                <code><a class='link' href='#ServiceClassProfileIdentifier'>ServiceClassProfileIdentifier</a></code>
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

### Information {#Information}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#145)*



<p>Human-readable information about a service. Strings are encoded in UTF-8.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>language</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>Language that is represented.  Must be two characters long and a valid
ICO 639:1988 identifier.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>Service name</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>A human-readable description</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>provider</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>The provider of this service (person or organization)</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Attribute {#Attribute}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#161)*



<p>A generic attribute, used for protocol information;</p>


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
                <code><a class='link' href='#DataElement'>DataElement</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ServiceDefinition {#ServiceDefinition}
*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#180)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>service_class_uuids</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>UUIDs of service classes that this service record conforms to.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol_descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProtocolDescriptor'>ProtocolDescriptor</a>&gt;</code>
            </td>
            <td><p>The protocols that can be used to gain access to this service, with their
protocol-specific identifiers.
This is ordered from lowest level to highest.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_protocol_descriptors</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td><p>Additional protocol descriptor lists, if the service requires more channels
in addition to the main service.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>profile_descriptors</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ProfileDescriptor'>ProfileDescriptor</a>&gt;</code>
            </td>
            <td><p>Bluetooth profiles that are supported by this service.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>information</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Information'>Information</a>&gt;</code>
            </td>
            <td><p>Human-readable service information, in one or more languages.
The first set of information is considered the primary language.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_attributes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Attribute'>Attribute</a>&gt;?</code>
            </td>
            <td><p>Additional attributes included in the Service Definition, for specific
services.
All of these attributes should have an Attribute ID above 0x0200.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### SecurityLevel {#SecurityLevel}
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

### DataElementType {#DataElementType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#8)*

<p>A building element in SDP.  Used for various low-level and custom parameters.</p>


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

### ProtocolIdentifier {#ProtocolIdentifier}
Type: <code>uint16</code>

*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#39)*

<p>Defined Protocol Identifiers for the Protocol Descriptor
We intentionally omit deprecated profile identifiers.
From Bluetooth Assigned Numbers:
https://www.bluetooth.com/specifications/assigned-numbers/service-discovery</p>


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

### ServiceClassProfileIdentifier {#ServiceClassProfileIdentifier}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.bredr/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#85)*

<p>Identifiers that are valid for Bluetooth Classes / Profiles
We intentionally omit classes and profile IDs that are unsupported, deprecated,
or reserved for use by Fuchsia Bluetooth.
From Bluetooth Assigned Numbers for SDP
https://www.bluetooth.com/specifications/assigned-numbers/service-discovery</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SerialPort</code></td>
            <td><code>4353</code></td>
            <td><p>ServiceDiscoveryService and BrowseGroupDescriptorService used by Fuchsia</p>
</td>
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
            <td><p>Headset Profile (HSP)</p>
</td>
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
            <td><p>Advanced Audio Distribution Profile (A2DP)</p>
</td>
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
            <td><p>Audio/Video Remote Control Profil (AVRCP)</p>
</td>
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
            <td><p>Personal Area Networking (PAN)</p>
</td>
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
            <td><p>Basic Printing and Basic Imaging Profiles omitted (unsupported)
Hands-Free Profile (HFP)</p>
</td>
        </tr><tr>
            <td><code>HandsfreeAudioGateway</code></td>
            <td><code>4383</code></td>
            <td></td>
        </tr><tr>
            <td><code>SIM_Access</code></td>
            <td><code>4397</code></td>
            <td><p>Human Interface Device and Hardcopy Cable Replacement Profile omitted (unsupported)</p>
</td>
        </tr><tr>
            <td><code>PhonebookPCE</code></td>
            <td><code>4398</code></td>
            <td><p>Phonebook Access Profile (PBAP)</p>
</td>
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
            <td><p>Message Access Profile (MAP)</p>
</td>
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
            <td><p>GNSS and 3DSP omitted (unsupported)
Multi-Profile Specification (MPS)</p>
</td>
        </tr><tr>
            <td><code>MPSClass</code></td>
            <td><code>4411</code></td>
            <td></td>
        </tr><tr>
            <td><code>VideoSource</code></td>
            <td><code>4867</code></td>
            <td><p>Calendar, Task, and Notes Profile omitted (unsupported)
Device ID used by Fuchsia
Video Distribution Profile (VDP)</p>
</td>
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
            <td><p>Health Device Profile (HDP)</p>
</td>
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

### DataElementData {#DataElementData}
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
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uuid</code></td>
            <td>
                <code>string</code>
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
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>sequence</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DataElement'>DataElement</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#59">kPSM_SDP</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>int64</code></td>
            <td><p>Defined PSMs from the Bluetooth Assigned Numbers
https://www.bluetooth.com/specifications/assigned-numbers/logical-link-control
Used in DataElementData for protocol parameters for L2CAP.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#60">kPSM_RFCOMM</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#61">kPSM_TCSBIN</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#62">kPSM_TCSBINCordless</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#63">kPSM_BNEP</a></td>
            <td>
                    <code>15</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#64">kPSM_HIDControl</a></td>
            <td>
                    <code>17</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#65">kPSM_HIDInterrupt</a></td>
            <td>
                    <code>19</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#66">kPSM_AVCTP</a></td>
            <td>
                    <code>23</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#67">kPSM_AVDTP</a></td>
            <td>
                    <code>25</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#68">kPSM_AVCTP_Browse</a></td>
            <td>
                    <code>27</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#69">kPSM_ATT</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#70">kPSM_3DSP</a></td>
            <td>
                    <code>33</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#71">kPSM_LE_IPSP</a></td>
            <td>
                    <code>35</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#72">kPSM_OTS</a></td>
            <td>
                    <code>37</code>
                </td>
                <td><code>int64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#168">ATTR_SERVICE_RECORD_HANDLE</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint16</code></td>
            <td><p>Universal attribute IDs.
From the Bluetooth Specification, Version 5, Vol 3, Part B</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#169">ATTR_SERVICE_CLASS_ID_LIST</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#170">ATTR_SERVICE_RECORD_STATE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#171">ATTR_SERVICE_ID</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#172">ATTR_PROTOCOL_DESCRIPTOR_LIST</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#173">ATTR_ADDITIONAL_PROTOCOL_DESCRIPTOR_LIST</a></td>
            <td>
                    <code>13</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#174">ATTR_BROWSE_GROUP_LIST</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#175">ATTR_LANGUAGE_BASE_ATTRIBUTE_ID_LIST</a></td>
            <td>
                    <code>6</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#176">ATTR_SERVICE_INFO_TIME_TO_LIVE</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#177">ATTR_SERVICE_AVAILABILITY</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.bredr/service.fidl#178">ATTR_BLUETOOTH_PROFILE_DESCRIPTOR_LIST</a></td>
            <td>
                    <code>9</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>



