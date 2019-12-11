[TOC]

# fuchsia.net.ppp


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.net.ppp/ppp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.ppp/ppp.fidl#35)*

<p>PPP device driver interface.</p>

### Rx {#Rx}

<p>Receive data.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#ProtocolType'>ProtocolType</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_Rx_Result'>Device_Rx_Result</a></code>
            </td>
        </tr></table>

### Tx {#Tx}

<p>Transmit data. When this call returns, it is guaranteed that the data has either been
written or that the write failed and the caller may attempt to retransmit.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#ProtocolType'>ProtocolType</a></code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_Tx_Result'>Device_Tx_Result</a></code>
            </td>
        </tr></table>

### GetInfo {#GetInfo}

<p>Obtain information about device configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#Info'>Info</a></code>
            </td>
        </tr></table>

### GetStatus {#GetStatus}

<p>Obtain status of a given protocol. If a protocol is <code>up</code>, <code>Rx</code> and <code>Tx</code> may be called with
the same protocol to send and receive PPP frames.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#ProtocolType'>ProtocolType</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>up</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### SetStatus {#SetStatus}

<p>Set status of a given protocol. If a protocol is <code>up</code>, <code>Rx</code> and <code>Tx</code> may be called with the
same protocol to send and receive PPP frames.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#ProtocolType'>ProtocolType</a></code>
            </td>
        </tr><tr>
            <td><code>up</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### Enable {#Enable}

<p>On up, obtain exclusive access to the serial port, and begin continuously reading all
protocol types. On down, stop reading and release access to the serial port. Errors only
occur when the device fails to obtain exclusive access to the serial port, in which case
the device remains in a down state. The device begins down when initialized, so <code>Enable</code>
must be called before the driver can send or receive data.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>up</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_Enable_Result'>Device_Enable_Result</a></code>
            </td>
        </tr></table>

## DeviceBootstrap {#DeviceBootstrap}
*Defined in [fuchsia.net.ppp/ppp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.ppp/ppp.fidl#62)*


### GetInstance {#GetInstance}

<p>Obtain a unique channel to be used with the driver. This is desirable to avoid blocking
other consumers of the device protocol, and should be removed when the DDK has a better
channel ownership model for drivers which implement protocols. All instances point to the
same underlying device; separate instances are only used to allow the driver to
concurrently reply to calls.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>instance</code></td>
            <td>
                <code><a class='link' href='#Device'>Device</a></code>
            </td>
        </tr></table>

## Ppp {#Ppp}
*Defined in [fuchsia.net.ppp/ppp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.ppp/ppp.fidl#73)*

<p>PPP service interface.</p>

### Open {#Open}

<p>Given an instance of the driver and options, attempt to open a PPP connection.
Uses the provided options to determine how to configure the link, and whether or not to
configure IPv4 or IPv6. If no error is returned, the connection is open and the driver
supports the requested protocols. Only one connection can be open at a time.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>instance</code></td>
            <td>
                <code><a class='link' href='#Device'>Device</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#ConnectionOptions'>ConnectionOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Ppp_Open_Result'>Ppp_Open_Result</a></code>
            </td>
        </tr></table>

### Close {#Close}

<p>If a connection is currently open, close it. Otherwise return an error.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Ppp_Close_Result'>Ppp_Close_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Device_Rx_Response {#Device_Rx_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Device_Tx_Response {#Device_Tx_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Device_Enable_Response {#Device_Enable_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Ppp_Open_Response {#Ppp_Open_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Ppp_Close_Response {#Ppp_Close_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Info {#Info}
*Defined in [fuchsia.net.ppp/ppp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.ppp/ppp.fidl#12)*



<p>Information about PPP device configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mtu</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ConnectionOptions {#ConnectionOptions}
*Defined in [fuchsia.net.ppp/ppp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.ppp/ppp.fidl#18)*



<p>Options for a PPP connection.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>magic_number</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Enable Link Control Protocol Magic Numbers for loopback detection.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipv4</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a>?</code>
            </td>
            <td><p>Enable IPv4 with the given IP address.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipv6</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv6Address'>Ipv6Address</a>?</code>
            </td>
            <td><p>Enable IPv6 with the given IPv6 address (used as an interface identifier).</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ProtocolType {#ProtocolType}
Type: <code>uint32</code>

*Defined in [fuchsia.net.ppp/ppp.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.ppp/ppp.fidl#28)*

<p>The type of protocol being transmitted or received.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONTROL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>IPV4</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>IPV6</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Device_Rx_Result {#Device_Rx_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_Rx_Response'>Device_Rx_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Device_Tx_Result {#Device_Tx_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_Tx_Response'>Device_Tx_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Device_Enable_Result {#Device_Enable_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_Enable_Response'>Device_Enable_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Ppp_Open_Result {#Ppp_Open_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Ppp_Open_Response'>Ppp_Open_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### Ppp_Close_Result {#Ppp_Close_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Ppp_Close_Response'>Ppp_Close_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>









