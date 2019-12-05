[TOC]

# fuchsia.netstack


## **PROTOCOLS**

## Netstack {#Netstack}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#109)*


### GetPortForService {#GetPortForService}

<p>Finds the port number from a given service name and protocol. [service] can be a
number like &quot;42&quot;, or a service name like &quot;http&quot;. If [protocol] is UNSPECIFIED,
the service is checked for TCP first, then UDP.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#Protocol'>Protocol</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### GetAddress {#GetAddress}

<p>Finds the IP address for a given host name and port. This may issue network
requests via DNS to look up domain names. E.g.
GetAddress(&quot;example.com&quot;, 80) -&gt; [{142.42.42.1}]</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>address</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addresses</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SocketAddress'>SocketAddress</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#NetErr'>NetErr</a></code>
            </td>
        </tr></table>

### GetInterfaces {#GetInterfaces}

<p>Returns the list of registered network interfaces.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interfaces</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NetInterface'>NetInterface</a>&gt;</code>
            </td>
        </tr></table>

### GetInterfaces2 {#GetInterfaces2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interfaces</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NetInterface2'>NetInterface2</a>&gt;</code>
            </td>
        </tr></table>

### GetRouteTable {#GetRouteTable}

<p>Returns current route table.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rt</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RouteTableEntry'>RouteTableEntry</a>&gt;</code>
            </td>
        </tr></table>

### GetRouteTable2 {#GetRouteTable2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rt</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#RouteTableEntry2'>RouteTableEntry2</a>&gt;</code>
            </td>
        </tr></table>

### SetInterfaceStatus {#SetInterfaceStatus}

<p>Sets the status (up or down) for the interface with the given nicid.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetInterfaceAddress {#SetInterfaceAddress}

<p>Sets the address for the interface with the given nicid.
Masks off addr.PrefixLen bits from addr.Addr to set the subnet.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
        </tr><tr>
            <td><code>prefixLen</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NetErr'>NetErr</a></code>
            </td>
        </tr></table>

### RemoveInterfaceAddress {#RemoveInterfaceAddress}

<p>Removes the address for the interface with the given nicid.
Masks off addr.PrefixLen bits from addr.Addr to set the subnet.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
        </tr><tr>
            <td><code>prefixLen</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NetErr'>NetErr</a></code>
            </td>
        </tr></table>

### SetInterfaceMetric {#SetInterfaceMetric}

<p>Sets the route metric for the interface with the given nicid.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>metric</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NetErr'>NetErr</a></code>
            </td>
        </tr></table>

### BridgeInterfaces {#BridgeInterfaces}

<p>Creates a bridge and returns the newly created nicid or an
error if the creation fails.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nicids</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NetErr'>NetErr</a></code>
            </td>
        </tr><tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### AddEthernetDevice {#AddEthernetDevice}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>topological_path</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>interfaceConfig</code></td>
            <td>
                <code><a class='link' href='#InterfaceConfig'>InterfaceConfig</a></code>
            </td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/#Device'>Device</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetDhcpClient {#GetDhcpClient}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>client</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.net.dhcp/'>fuchsia.net.dhcp</a>/<a class='link' href='../fuchsia.net.dhcp/#Client'>Client</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Netstack_GetDhcpClient_Result'>Netstack_GetDhcpClient_Result</a></code>
            </td>
        </tr></table>

### StartRouteTableTransaction {#StartRouteTableTransaction}

<p>Begin a route transaction for atomically getting and setting the route
table.  Returns true if a transaction can be started.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>routeTableTransaction</code></td>
            <td>
                <code>request&lt;<a class='link' href='#RouteTableTransaction'>RouteTableTransaction</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### OnInterfacesChanged {#OnInterfacesChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interfaces</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#NetInterface'>NetInterface</a>&gt;</code>
            </td>
        </tr></table>

## ResolverAdmin {#ResolverAdmin}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#165)*


### SetNameServers {#SetNameServers}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>servers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a>&gt;</code>
            </td>
        </tr></table>



## RouteTableTransaction {#RouteTableTransaction}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#170)*


### AddRoute {#AddRoute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>r</code></td>
            <td>
                <code><a class='link' href='#RouteTableEntry2'>RouteTableEntry2</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### DelRoute {#DelRoute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>r</code></td>
            <td>
                <code><a class='link' href='#RouteTableEntry2'>RouteTableEntry2</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



## **STRUCTS**

### Netstack_GetDhcpClient_Response {#Netstack_GetDhcpClient_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### NetErr {#NetErr}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#27)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InterfaceConfig {#InterfaceConfig}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>filepath</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>An unstable file path corresponding to the interface. Used in watching the creation
and destruction of the interface, or in accessing the interface using netdump.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>metric</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ip_address_config</code></td>
            <td>
                <code><a class='link' href='#IpAddressConfig'>IpAddressConfig</a></code>
            </td>
            <td><p>Deprecated; to configure a network interface, use SetDhcpClientStatus
and SetInterfaceAddress instead.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### NetInterface {#NetInterface}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#51)*



<p>https://linux.die.net/man/7/netdevice</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>features</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>configuration</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>netmask</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>broadaddr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipv6addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Subnet'>Subnet</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>hwaddr</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NetInterface2 {#NetInterface2}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#67)*



<p>New version that includes a metric value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>features</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>configuration</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metric</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>netmask</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>broadaddr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipv6addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Subnet'>Subnet</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>hwaddr</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RouteTableEntry {#RouteTableEntry}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#85)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>destination</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>netmask</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>gateway</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RouteTableEntry2 {#RouteTableEntry2}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#95)*



<p>New version that includes a metric value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>destination</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>netmask</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>gateway</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nicid</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metric</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SocketAddress {#SocketAddress}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#103)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Protocol {#Protocol}
Type: <code>uint32</code>

*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#12)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>UDP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TCP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Status {#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#18)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DNS_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PARSE_ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>IPV4_ONLY</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_INTERFACE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Netstack_GetDhcpClient_Result {#Netstack_GetDhcpClient_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Netstack_GetDhcpClient_Response'>Netstack_GetDhcpClient_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### IpAddressConfig {#IpAddressConfig}
*Defined in [fuchsia.netstack/netstack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#45)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>static_ip</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Subnet'>Subnet</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dhcp</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#82">NetInterfaceFlagUp</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Flags for NetInterface.flags.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.netstack/netstack.fidl#83">NetInterfaceFlagDhcp</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



