[TOC]

# fuchsia.bluetooth.snoop


## **PROTOCOLS**

## Snoop {#Snoop}
*Defined in [fuchsia.bluetooth.snoop/snooper.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.snoop/snooper.fidl#48)*

<p>Interface to receive packets recorded as received or transmitted for a Bluetooth host.
Packets are received by the client as datagrams through the fidl channel as <code>OnPacket</code>
events.</p>

### Start {#Start}

<p>Subscribe to receive packets from the server. Packets that have been recorded are sent
first.</p>
<p>If <code>follow</code> is true, the channel stays open and packets are sent to the client as
the snoop server receives them. If <code>follow</code> is false, the channel is closed by the server
when all recorded packets have been sent.</p>
<p>A <code>host_device</code> name may be provided; if so, only events from that host are sent to the client.
If <code>host_device</code> is absent, the client is sent events from all host devices.</p>
<p>Errors:
<code>Start</code> can only be called once per connection. After the first request, subsequent requests
always return an error.
<code>host_device</code> values that are not recognized by the server return an error.</p>

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

<p>An event containing a packet that the client has registered interest in receiving and the
<code>host_device</code> which generated the packet.</p>



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



<p>Timestamp represents the number of seconds and nanoseconds since the Unix epoch.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>subsec_nanos</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Valid values for <code>subsec_nanos</code> can be greater than 10^9-1. Therefore the total
seconds elapsed since the epoch is defined by the value of <code>seconds</code> plus
<code>subsec_nanos</code> / 10^9 - the value of <code>seconds</code> alone may not be sufficient.</p>
<p>It is invalid for the carry from <code>subsec_nanos</code> to overflow the <code>seconds</code> field.
A client or server should reject such data as malformed.</p>
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
            <td><p>true if this packet is sent from the controller to the host.</p>
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
            <td><p>Timestamp that the bt-snoop service received the packet from a snoop channel as measured
by the host system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>original_len</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Original length of the packet before truncation.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>Payload sent over the HCI.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PacketType {#PacketType}
Type: <code>uint32</code>

*Defined in [fuchsia.bluetooth.snoop/snooper.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.bluetooth.snoop/snooper.fidl#22)*

<p>Messages coming through the Host Controller Interface can be one of three types.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CMD</code></td>
            <td><code>0</code></td>
            <td><p>Command sent from the host to the controller.</p>
</td>
        </tr><tr>
            <td><code>EVENT</code></td>
            <td><code>1</code></td>
            <td><p>Event sent from the controller to the host.</p>
</td>
        </tr><tr>
            <td><code>DATA</code></td>
            <td><code>2</code></td>
            <td><p>Data sent from the controller to the host.</p>
</td>
        </tr></table>













