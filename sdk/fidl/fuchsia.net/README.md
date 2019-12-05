[TOC]

# fuchsia.net


## **PROTOCOLS**

## Connectivity {#Connectivity}
*Defined in [fuchsia.net/connectivity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/connectivity.fidl#8)*


### OnNetworkReachable {#OnNetworkReachable}

<p>This is triggered on a state change in network reachability. Clients
should expect that network requests will succeed when <code>reachable</code> is
true.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reachable</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## NameLookup {#NameLookup}
*Defined in [fuchsia.net/namelookup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#41)*


### LookupIp {#LookupIp}

<p>Look up a list of IP addresses by hostname.</p>
<p>If <code>hostname</code> is an Internationalized Domain Name, it must be encoded as per RFC 3490.</p>

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
                <code><a class='link' href='#LookupIpOptions'>LookupIpOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NameLookup_LookupIp_Result'>NameLookup_LookupIp_Result</a></code>
            </td>
        </tr></table>

### LookupHostname {#LookupHostname}

<p>Look up a hostname by IP address.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#IpAddress'>IpAddress</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NameLookup_LookupHostname_Result'>NameLookup_LookupHostname_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### NameLookup_LookupIp_Response {#NameLookup_LookupIp_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#IpAddressInfo'>IpAddressInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NameLookup_LookupHostname_Response {#NameLookup_LookupHostname_Response}
*generated*





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

### IpAddressInfo {#IpAddressInfo}
*Defined in [fuchsia.net/namelookup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ipv4_addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Ipv4Address'>Ipv4Address</a>&gt;[256]</code>
            </td>
            <td><p>All of the IPv4 addresses for the requested hostname.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ipv6_addrs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Ipv6Address'>Ipv6Address</a>&gt;[256]</code>
            </td>
            <td><p>All of the IPv6 addresses for the requested hostname.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>canonical_name</code></td>
            <td>
                <code>string[256]?</code>
            </td>
            <td><p>The canonical name of the requested hostname (usually the DNS CNAME record, if one exists).</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Ipv4Address {#Ipv4Address}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#9)*



<p>Ipv4Address is expressed in network byte order, so the most significant byte
(&quot;127&quot; in the address &quot;127.0.0.1&quot;) will be at index 0.</p>


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

### Ipv6Address {#Ipv6Address}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#15)*



<p>Ipv6Address is expressed in network byte order, so the most significant byte
(&quot;ff&quot; in the address &quot;ff02::1&quot;) will be at index 0.</p>


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

### Endpoint {#Endpoint}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#28)*



<p>Endpoint describes an IP address and port. The network protocol associated
with the Endpoint will be known from context or communicated through
additional structures.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#IpAddress'>IpAddress</a></code>
            </td>
            <td><p>The IP address of the endpoint.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The port number of the endpoint.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Subnet {#Subnet}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#38)*



<p>Subnet describes an IP subnetwork, where all host IP addresses share the same most significant
bits.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#IpAddress'>IpAddress</a></code>
            </td>
            <td><p>The Ipv4 or Ipv6 address. Only the <code>prefix_len</code> most significant bits may be set in <code>addr</code>;
all bits in the host portion of the address must be zero.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>prefix_len</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>The prefix length of the netmask. E.g. for 192.168.1.0/24, the prefix
length is 24, corresponding to a netmask of 255.255.255.0.
For Ipv4, prefix_len must be in the range [0, 32].
For Ipv6, prefix_len must be in the range [0, 128].</p>
</td>
            <td>No default</td>
        </tr>
</table>

### MacAddress {#MacAddress}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#51)*



<p>A MAC address used to identify a network interface on the data link layer within the network.</p>


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



## **ENUMS**

### LookupError {#LookupError}
Type: <code>uint32</code>

*Defined in [fuchsia.net/namelookup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#16)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>1</code></td>
            <td><p>No result was found for this query.</p>
</td>
        </tr><tr>
            <td><code>TRANSIENT</code></td>
            <td><code>2</code></td>
            <td><p>The lookup failed, but may succeed at a later time. For instance, the
network or DNS server may be unreachable.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ARGS</code></td>
            <td><code>3</code></td>
            <td><p>The lookup failed due to an invalid argument (for instance, the hostname was not encoded
correctly, or was too long).</p>
</td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>4</code></td>
            <td><p>The lookup failed due to an internal error.</p>
</td>
        </tr></table>





## **UNIONS**

### NameLookup_LookupIp_Result {#NameLookup_LookupIp_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#NameLookup_LookupIp_Response'>NameLookup_LookupIp_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#LookupError'>LookupError</a></code>
            </td>
            <td></td>
        </tr></table>

### NameLookup_LookupHostname_Result {#NameLookup_LookupHostname_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#NameLookup_LookupHostname_Response'>NameLookup_LookupHostname_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#LookupError'>LookupError</a></code>
            </td>
            <td></td>
        </tr></table>

### IpAddress {#IpAddress}
*Defined in [fuchsia.net/net.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/net.fidl#20)*

<p>Represents an IP address that may be either v4 or v6.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>ipv4</code></td>
            <td>
                <code><a class='link' href='#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>ipv6</code></td>
            <td>
                <code><a class='link' href='#Ipv6Address'>Ipv6Address</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**

### LookupIpOptions {#LookupIpOptions}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>V4_ADDRS</td>
            <td>1</td>
            <td><p>If the lookup should return IPv4 addresses.</p>
</td>
        </tr><tr>
            <td>V6_ADDRS</td>
            <td>2</td>
            <td><p>If the lookup should return IPv6 addresses.</p>
</td>
        </tr><tr>
            <td>CNAME_LOOKUP</td>
            <td>4</td>
            <td><p>If the lookup should return a canonical_name, if one exists.</p>
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net/namelookup.fidl#38">MAX_HOSTNAME_SIZE</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    
</table>



