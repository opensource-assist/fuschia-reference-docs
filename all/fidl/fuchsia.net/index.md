Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net


## **PROTOCOLS**

## Connectivity {:#Connectivity}
*Defined in [fuchsia.net/connectivity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/connectivity.fidl#8)*


### OnNetworkReachable {:#OnNetworkReachable}

 This is triggered on a state change in network reachability. Clients
 should expect that network requests will succeed when `reachable` is
 true.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reachable</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## NameLookup {:#NameLookup}
*Defined in [fuchsia.net/namelookup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#41)*


### LookupIp {:#LookupIp}

 Look up a list of IP addresses by hostname.

 If `hostname` is an Internationalized Domain Name, it must be encoded as per RFC 3490.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hostname</code></td>
            <td>
                <code>string[255]</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#LookupIpOptions'>LookupIpOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#NameLookup_LookupIp_Result'>NameLookup_LookupIp_Result</a></code>
            </td>
        </tr></table>

### LookupHostname {:#LookupHostname}

 Look up a hostname by IP address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#NameLookup_LookupHostname_Result'>NameLookup_LookupHostname_Result</a></code>
            </td>
        </tr></table>

## SocketProvider {:#SocketProvider}
*Defined in [fuchsia.net/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/socket.fidl#48)*

 SocketProvider implements the POSIX sockets API.

### GetAddrInfo {:#GetAddrInfo}

 Retrieves information about the address of a node and/or service. The number of valid
 results in `res` is given by the `count` return value.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node</code></td>
            <td>
                <code>string[256]?</code>
            </td>
        </tr><tr>
            <td><code>service</code></td>
            <td>
                <code>string[256]?</code>
            </td>
        </tr><tr>
            <td><code>hints</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#AddrInfoHints'>AddrInfoHints</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#AddrInfoStatus'>AddrInfoStatus</a></code>
            </td>
        </tr><tr>
            <td><code>nres</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>res</code></td>
            <td>
                <code>[4]</code>
            </td>
        </tr></table>



## **STRUCTS**

### NameLookup_LookupIp_Response {:#NameLookup_LookupIp_Response}
*Defined in [fuchsia.net/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#3)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#IpAddressInfo'>IpAddressInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NameLookup_LookupHostname_Response {:#NameLookup_LookupHostname_Response}
*Defined in [fuchsia.net/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>hostname</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### IpAddressInfo {:#IpAddressInfo}
*Defined in [fuchsia.net/namelookup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ipv4_addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/index.html#Ipv4Address'>Ipv4Address</a>&gt;</code>
            </td>
            <td> All of the IPv4 addresses for the requested hostname.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipv6_addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/index.html#Ipv6Address'>Ipv6Address</a>&gt;</code>
            </td>
            <td> All of the IPv6 addresses for the requested hostname.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>canonical_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td> The canonical name of the requested hostname (usually the DNS CNAME record, if one exists).
</td>
            <td>No default</td>
        </tr>
</table>

### Ipv4Address {:#Ipv4Address}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#9)*



 Ipv4Address is expressed in network byte order, so the most significant byte
 ("127" in the address "127.0.0.1") will be at index 0.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>uint8[4]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Ipv6Address {:#Ipv6Address}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#15)*



 Ipv6Address is expressed in network byte order, so the most significant byte
 ("ff" in the address "ff02::1") will be at index 0.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Endpoint {:#Endpoint}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#28)*



 Endpoint describes an IP address and port. The network protocol associated
 with the Endpoint will be known from context or communicated through
 additional structures.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td> The IP address of the endpoint.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> The port number of the endpoint.
</td>
            <td>No default</td>
        </tr>
</table>

### Subnet {:#Subnet}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#38)*



 Subnet describes an IP subnetwork, where all host IP addresses share the same most significant
 bits.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td> The Ipv4 or Ipv6 address. Only the `prefix_len` most significant bits may be set in `addr`;
 all bits in the host portion of the address must be zero.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>prefix_len</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td> The prefix length of the netmask. E.g. for 192.168.1.0/24, the prefix
 length is 24, corresponding to a netmask of 255.255.255.0.
 For Ipv4, prefix_len must be in the range [0, 32].
 For Ipv6, prefix_len must be in the range [0, 128].
</td>
            <td>No default</td>
        </tr>
</table>

### MacAddress {:#MacAddress}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#51)*



 A MAC address used to identify a network interface on the data link layer within the network.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>octets</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddrInfoHints {:#AddrInfoHints}
*Defined in [fuchsia.net/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/socket.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>family</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>sock_type</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddrStorage {:#AddrStorage}
*Defined in [fuchsia.net/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/socket.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>val</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>len</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddrInfo {:#AddrInfo}
*Defined in [fuchsia.net/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/socket.fidl#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>family</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>sock_type</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#AddrStorage'>AddrStorage</a></code>
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

### LookupError {:#LookupError}
Type: <code>uint32</code>

*Defined in [fuchsia.net/namelookup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#16)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRANSIENT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### AddrInfoStatus {:#AddrInfoStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.net/socket.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/socket.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ok</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>bad_flags</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>no_name</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>again</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>fail</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>no_data</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>buffer_overflow</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>system_error</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### NameLookup_LookupIp_Result {:#NameLookup_LookupIp_Result}
*Defined in [fuchsia.net/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#6)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#NameLookup_LookupIp_Response'>NameLookup_LookupIp_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#LookupError'>LookupError</a></code>
            </td>
            <td></td>
        </tr></table>

### NameLookup_LookupHostname_Result {:#NameLookup_LookupHostname_Result}
*Defined in [fuchsia.net/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#13)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#NameLookup_LookupHostname_Response'>NameLookup_LookupHostname_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#LookupError'>LookupError</a></code>
            </td>
            <td></td>
        </tr></table>

### IpAddress {:#IpAddress}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#20)*

 Represents an IP address that may be either v4 or v6.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>ipv4</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>ipv6</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html#Ipv6Address'>Ipv6Address</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**
### LookupIpOptions {:#LookupIpOptions}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>V4_ADDRS</td>
            <td>1</td>
            <td> If the lookup should return IPv4 addresses.
</td>
        </tr><tr>
            <td>V6_ADDRS</td>
            <td>2</td>
            <td> If the lookup should return IPv6 addresses.
</td>
        </tr><tr>
            <td>CNAME_LOOKUP</td>
            <td>4</td>
            <td> If the lookup should return a canonical_name, if one exists.
</td>
        </tr></table>



## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#38">MAX_HOSTNAME_SIZE</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    
</table>
