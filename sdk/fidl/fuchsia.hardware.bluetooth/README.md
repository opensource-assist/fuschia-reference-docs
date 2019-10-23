[TOC]

# fuchsia.hardware.bluetooth


## **PROTOCOLS**

## Emulator {#Emulator}
*Defined in [fuchsia.hardware.bluetooth/emulator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-bluetooth/emulator.fidl#10)*

 Represents the bt-emulator device protocol. A bt-emulator device is used for configuring and
 publishing fake bt-hci devices.

### Open {#Open}

 Opens a fake controller management channel that speaks the
 "//sdk/fidl/fuchsia.bluetooth.test.HciEmulator" protocol.
 Only one channel to this protocol can be open on a given bt-hci-emulator
 device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## Hci {#Hci}
*Defined in [fuchsia.hardware.bluetooth/hci.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-bluetooth/hci.fidl#8)*


### OpenCommandChannel {#OpenCommandChannel}

 Opens a command/event channel on the provided handle. The zircon channel
 is closed in the event of an error opening the hci channel or if the hci
 channel is already associated with a handle to another zircon channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### OpenAclDataChannel {#OpenAclDataChannel}

 Opens a acl data channel on the provided handle. The zircon channel is
 closed in the event of an error opening the hci channel or if the hci
 channel is already associated with a handle to another zircon channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### OpenSnoopChannel {#OpenSnoopChannel}

 Opens a snoop channel on the provided handle. The zircon channel is
 closed in the event of an error opening the hci channel or if the hci
 channel is already associated with a handle to another zircon channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## Host {#Host}
*Defined in [fuchsia.hardware.bluetooth/host.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-bluetooth/host.fidl#8)*


### Open {#Open}

 Connects to the host driver on the provided handle. The zircon channel
 is closed in the event of an error connecting to the driver. This
 channel speaks the "/src/connectivity/bluetooth/fidl/fuchsia.bluetooth.host.Host"
 protocol.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>

















