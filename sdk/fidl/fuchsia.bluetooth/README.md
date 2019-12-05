[TOC]

# fuchsia.bluetooth




## **STRUCTS**

### Address {#Address}
*Defined in [fuchsia.bluetooth/address.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/address.fidl#16)*



<p>Represents a 48-bit Bluetooth Device Address.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#AddressType'>AddressType</a></code>
            </td>
            <td><p>Type of the device address.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td><p>The device address bytes in little-endian order.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### DeviceClass {#DeviceClass}
*Defined in [fuchsia.bluetooth/device_class.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#14)*



<p>The &quot;Class of Device/Service&quot; is a variable-format field that defines the category of a
Bluetooth device. The bitfield is divided into segments called &quot;major service class&quot;,
&quot;major device class&quot;, and &quot;minor device class&quot;.</p>
<p>No assumptions about the specific functionality or characteristics of any application should be
based solely on its inclusion within a Major or Minor device class. For more information, see
https://www.bluetooth.com/specifications/assigned-numbers/baseband.</p>


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

### Id {#Id}
*Defined in [fuchsia.bluetooth/id.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/id.fidl#8)*



<p>Generic 64-bit identifier type.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PeerId {#PeerId}
*Defined in [fuchsia.bluetooth/id.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/id.fidl#13)*



<p>64-bit unique value used by the system to identify peer devices.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Bool {#Bool}
*Defined in [fuchsia.bluetooth/nullables.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/nullables.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Int8 {#Int8}
*Defined in [fuchsia.bluetooth/nullables.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/nullables.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UInt16 {#UInt16}
*Defined in [fuchsia.bluetooth/nullables.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/nullables.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Error {#Error}
*Defined in [fuchsia.bluetooth/status.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/status.fidl#26)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error_code</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol_error_code</code></td>
            <td>
                <code>uint32</code>
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
        </tr>
</table>

### Status {#Status}
*Defined in [fuchsia.bluetooth/status.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/status.fidl#43)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Uuid {#Uuid}
*Defined in [fuchsia.bluetooth/uuid.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/uuid.fidl#10)*



<p>Represents a Bluetooth UUID in its 128-bit canonical form. While the Bluetooth standard supports
16- and 32-bit short form UUIDs over the wire, the Fuchsia FIDL libraries require all UUIDs to
be represented in their canonical 128-bit form.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td><p>The UUID bytes in little-endian order.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### AddressType {#AddressType}
Type: <code>uint8</code>

*Defined in [fuchsia.bluetooth/address.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/address.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PUBLIC</code></td>
            <td><code>1</code></td>
            <td><p>LE public device address or <code>BR/EDR</code> <code>BD_ADDR</code>.</p>
</td>
        </tr><tr>
            <td><code>RANDOM</code></td>
            <td><code>2</code></td>
            <td><p>LE private or static random device address.</p>
</td>
        </tr></table>

### Appearance {#Appearance}
Type: <code>uint16</code>

*Defined in [fuchsia.bluetooth/appearance.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/appearance.fidl#11)*

<p>Possible values for the LE Appearance property which describes the external
appearance of a peer at a high level.
(See the Bluetooth assigned-numbers document:
https://www.bluetooth.com/specifications/gatt/viewer?attributeXmlFile=org.bluetooth.characteristic.gap.appearance.xml)</p>


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

### ConnectionRole {#ConnectionRole}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth/connection_role.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/connection_role.fidl#10)*

<p>Refers to the role of a Bluetooth device (local or peer) in a physical channel piconet. See
<a href="/src/connectivity/bluetooth/docs/vocabulary.md">Bluetooth Vocabulary Guide</a> for more
information.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LEADER</code></td>
            <td><code>1</code></td>
            <td><p>The role of the device that defines the piconet physical channel in BR/EDR or the
&quot;initiating&quot; device in LE.</p>
</td>
        </tr><tr>
            <td><code>FOLLOWER</code></td>
            <td><code>2</code></td>
            <td><p>The role of a device that synchronizes to the piconet physical channel in BR/EDR or the
&quot;advertising&quot; device in LE.</p>
</td>
        </tr></table>

### ErrorCode {#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth/status.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/status.fidl#10)*

<p>DEPRECATED. Do not use these types in new code. Prefer the &quot;error&quot; syntax, protocol-specific
enums and zx.status instead.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CANCELED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>IN_PROGRESS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIMED_OUT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLUETOOTH_NOT_AVAILABLE</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_STATE</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALREADY</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROTOCOL_ERROR</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#19">MAJOR_DEVICE_CLASS_MASK</a></td>
            <td>
                    <code>7936</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Constants for the major device class field. The major device class is defined by bits 12-8.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#21">MAJOR_DEVICE_CLASS_MISCELLANEOUS</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#22">MAJOR_DEVICE_CLASS_COMPUTER</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#23">MAJOR_DEVICE_CLASS_PHONE</a></td>
            <td>
                    <code>512</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#24">MAJOR_DEVICE_CLASS_LAN</a></td>
            <td>
                    <code>768</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#25">MAJOR_DEVICE_CLASS_AUDIO_VIDEO</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#26">MAJOR_DEVICE_CLASS_PERIPHERAL</a></td>
            <td>
                    <code>1280</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#27">MAJOR_DEVICE_CLASS_IMAGING</a></td>
            <td>
                    <code>1536</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#28">MAJOR_DEVICE_CLASS_WEARABLE</a></td>
            <td>
                    <code>1792</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#29">MAJOR_DEVICE_CLASS_TOY</a></td>
            <td>
                    <code>2048</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#30">MAJOR_DEVICE_CLASS_HEALTH</a></td>
            <td>
                    <code>2304</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth/device_class.fidl#31">MAJOR_DEVICE_CLASS_UNCATEGORIZED</a></td>
            <td>
                    <code>7936</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



