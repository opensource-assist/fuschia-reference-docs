Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.dns


## **PROTOCOLS**

## DnsPolicy {:#DnsPolicy}
*Defined in [fuchsia.net.dns/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dns/dns.fidl#29)*

 This interface is used to interact with the policy layer of the fuchsia
 netstack implementation that is hosted in netcfg.  This interface is
 for use solely by privileged system components such as a 'system setting'
 user interface, and can be used to change system-wide DNS settings.

### SetDNSConfig {:#SetDNSConfig}

 Set the DNS servers' IP addresses.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#DNSConfig'>DNSConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#NetError'>NetError</a></code>
            </td>
        </tr></table>

### GetDNSConfig {:#GetDNSConfig}

 Get the DNS servers' IP addresses.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current</code></td>
            <td>
                <code><a class='link' href='#DNSConfig'>DNSConfig</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### NetError {:#NetError}
*Defined in [fuchsia.net.dns/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dns/dns.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DNSConfig {:#DNSConfig}
*Defined in [fuchsia.net.dns/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dns/dns.fidl#20)*



 Settings for the system-wide DNS behavior.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dns_servers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {:#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.net.dns/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.dns/dns.fidl#9)*



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
            <td><code>PARSE_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>











