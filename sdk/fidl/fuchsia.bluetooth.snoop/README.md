[TOC]

# fuchsia.bluetooth.snoop


## **PROTOCOLS**

## Snoop {#Snoop}
*Defined in [fuchsia.bluetooth.snoop/snooper.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.snoop/snooper.fidl#48)*

 Interface to receive packets recorded as received or transmitted for a Bluetooth host.
 Packets are received by the client as datagrams through the fidl channel as `OnPacket`
 events.

### Start {#Start}

 Subscribe to receive packets from the server. Packets that have been recorded are sent
 first.

 If `follow` is true, the channel stays open and packets are sent to the client as
 the snoop server receives them. If `follow` is false, the channel is closed by the server
 when all recorded packets have been sent.

 A `host_device` name may be provided; if so, only events from that host are sent to the client.
 If `host_device` is absent, the client is sent events from all host devices.

 Errors:
   `Start` can only be called once per connection. After the first request, subsequent requests
   always return an error.
   `host_device` values that are not recognized by the server return an error.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>follow</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>host_device</code></td>
            <td>
                <code>string?</code>
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

### OnPacket {#OnPacket}

 An event containing a packet that the client has registered interest in receiving and the
 `host_device` which generated the packet.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>host_device</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#SnoopPacket'>SnoopPacket</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Timestamp {#Timestamp}
*Defined in [fuchsia.bluetooth.snoop/snooper.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.snoop/snooper.fidl#10)*



 Timestamp represents the number of seconds and nanoseconds since the Unix epoch.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>subsec_nanos</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Valid values for `subsec_nanos` can be greater than 10^9-1. Therefore the total
 seconds elapsed since the epoch is defined by the value of `seconds` plus
 `subsec_nanos` / 10^9 - the value of `seconds` alone may not be sufficient.

 It is invalid for the carry from `subsec_nanos` to overflow the `seconds` field.
 A client or server should reject such data as malformed.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>seconds</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SnoopPacket {#SnoopPacket}
*Defined in [fuchsia.bluetooth.snoop/snooper.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.snoop/snooper.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>is_received</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> true if this packet is sent from the controller to the host.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#PacketType'>PacketType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code><a class='link' href='#Timestamp'>Timestamp</a></code>
            </td>
            <td> Timestamp that the bt-snoop service received the packet from a snoop channel as measured
 by the host system.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>original_len</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Original length of the packet before truncation.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> Payload sent over the HCI.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PacketType {#PacketType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.snoop/snooper.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.snoop/snooper.fidl#22)*

 Messages coming through the Host Controller Interface can be one of three types.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CMD</code></td>
            <td><code>0</code></td>
            <td> Command sent from the host to the controller.
</td>
        </tr><tr>
            <td><code>EVENT</code></td>
            <td><code>1</code></td>
            <td> Event sent from the controller to the host.
</td>
        </tr><tr>
            <td><code>DATA</code></td>
            <td><code>2</code></td>
            <td> Data sent from the controller to the host.
</td>
        </tr></table>











