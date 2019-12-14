[TOC]

# fuchsia.router.config


## **PROTOCOLS**

## RouterAdmin {#RouterAdmin}
*Defined in [fuchsia.router.config/services.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/services.fidl#22)*

<p>RouterAdmin provides APIs for administering the router.</p>

### CreateWan {#CreateWan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>vlan</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>ports</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### CreateLan {#CreateLan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>vlan</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>ports</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### RemoveWan {#RemoveWan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### RemoveLan {#RemoveLan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetWanProperties {#SetWanProperties}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#WanProperties'>WanProperties</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetLanProperties {#SetLanProperties}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#LanProperties'>LanProperties</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetDhcpAddressPool {#SetDhcpAddressPool}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr><tr>
            <td><code>pool</code></td>
            <td>
                <code><a class='link' href='#AddressPool'>AddressPool</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetDhcpServerOptions {#SetDhcpServerOptions}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#DhcpServerOptions'>DhcpServerOptions</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetDhcpReservation {#SetDhcpReservation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr><tr>
            <td><code>reservation</code></td>
            <td>
                <code><a class='link' href='#DhcpReservation'>DhcpReservation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reservation_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteDhcpReservation {#DeleteDhcpReservation}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reservation_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetSystemConfig {#SetSystemConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#SystemConfig'>SystemConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetDnsResolver {#SetDnsResolver}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#DnsResolverConfig'>DnsResolverConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetDnsForwarder {#SetDnsForwarder}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#DnsForwarderConfig'>DnsForwarderConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### AddDnsEntry {#AddDnsEntry}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entry</code></td>
            <td>
                <code><a class='link' href='#DnsForwarderEntry'>DnsForwarderEntry</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entry_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteDnsEntry {#DeleteDnsEntry}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entry_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetRoute {#SetRoute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>route</code></td>
            <td>
                <code><a class='link' href='#Route'>Route</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteRoute {#DeleteRoute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>route_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### UpdateRouteMetric {#UpdateRouteMetric}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>route_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
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
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetSecurityFeatures {#SetSecurityFeatures}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>features</code></td>
            <td>
                <code><a class='link' href='#SecurityFeatures'>SecurityFeatures</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetPortForward {#SetPortForward}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#PortForwardingRule'>PortForwardingRule</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeletePortForward {#DeletePortForward}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetPortTrigger {#SetPortTrigger}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#PortTriggerRule'>PortTriggerRule</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeletePortTrigger {#DeletePortTrigger}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetFilter {#SetFilter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#FilterRule'>FilterRule</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteFilter {#DeleteFilter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetIpv6PinHole {#SetIpv6PinHole}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#Ipv6PinHoleRule'>Ipv6PinHoleRule</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteIpv6PinHole {#DeleteIpv6PinHole}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### SetDmzHost {#SetDmzHost}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#DmzHost'>DmzHost</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteDmzHost {#DeleteDmzHost}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### CreateWlanNetwork {#CreateWlanNetwork}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>network</code></td>
            <td>
                <code><a class='link' href='#WlanNetwork'>WlanNetwork</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteWlanNetwork {#DeleteWlanNetwork}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>network_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

## RouterSystem {#RouterSystem}
*Defined in [fuchsia.router.config/services.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/services.fidl#82)*

<p>RouterSystem provides APIs for managing features that are considered crytical for the system.
For example, setting filter rules that come into effect on startup.</p>

### SetAcl {#SetAcl}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#SystemAcl'>SystemAcl</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>acl_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### DeleteAcl {#DeleteAcl}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>acl_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetAcl {#GetAcl}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>acl_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>acl</code></td>
            <td>
                <code><a class='link' href='#SystemAcl'>SystemAcl</a></code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetAcls {#GetAcls}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

## RouterState {#RouterState}
*Defined in [fuchsia.router.config/services.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/services.fidl#91)*

<p>RouterState provide APIs for querying the router state.</p>

### GetWan {#GetWan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wan_lif</code></td>
            <td>
                <code><a class='link' href='#Lif'>Lif</a></code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetWans {#GetWans}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wans</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Lif'>Lif</a>&gt;</code>
            </td>
        </tr></table>

### GetWanPorts {#GetWanPorts}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetLan {#GetLan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_lif</code></td>
            <td>
                <code><a class='link' href='#Lif'>Lif</a></code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetLans {#GetLans}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lans</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Lif'>Lif</a>&gt;</code>
            </td>
        </tr></table>

### GetLanPorts {#GetLanPorts}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetPort {#GetPort}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port</code></td>
            <td>
                <code><a class='link' href='#Port'>Port</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetPorts {#GetPorts}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ports</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Port'>Port</a>&gt;</code>
            </td>
        </tr></table>

### GetWlanNetworks {#GetWlanNetworks}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>networks</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#WlanNetwork'>WlanNetwork</a>&gt;</code>
            </td>
        </tr></table>

### GetWanProperties {#GetWanProperties}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#WanProperties'>WanProperties</a></code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetLanProperties {#GetLanProperties}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#LanProperties'>LanProperties</a></code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetDhcpConfig {#GetDhcpConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>lan_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dhcp_config</code></td>
            <td>
                <code><a class='link' href='#DhcpServerConfig'>DhcpServerConfig</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetDnsResolver {#GetDnsResolver}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dns_resolver</code></td>
            <td>
                <code><a class='link' href='#DnsResolverConfig'>DnsResolverConfig</a></code>
            </td>
        </tr></table>

### GetDnsForwarder {#GetDnsForwarder}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>dns_forwarder</code></td>
            <td>
                <code><a class='link' href='#DnsForwarder'>DnsForwarder</a></code>
            </td>
        </tr></table>

### GetRoutes {#GetRoutes}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>routes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Route'>Route</a>&gt;</code>
            </td>
        </tr></table>

### GetRoute {#GetRoute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>route_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>route</code></td>
            <td>
                <code><a class='link' href='#Route'>Route</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetSecurityFeatures {#GetSecurityFeatures}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>features</code></td>
            <td>
                <code><a class='link' href='#SecurityFeatures'>SecurityFeatures</a></code>
            </td>
        </tr></table>

### GetPortForward {#GetPortForward}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#PortForwardingRule'>PortForwardingRule</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetPortTrigger {#GetPortTrigger}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#PortTriggerRule'>PortTriggerRule</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetFilter {#GetFilter}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#FilterRule'>FilterRule</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetIpv6PinHole {#GetIpv6PinHole}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#Ipv6PinHoleRule'>Ipv6PinHoleRule</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetDmzHost {#GetDmzHost}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rule</code></td>
            <td>
                <code><a class='link' href='#DmzHost'>DmzHost</a>?</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### GetPortForwards {#GetPortForwards}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port_forward_rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortForwardingRule'>PortForwardingRule</a>&gt;</code>
            </td>
        </tr></table>

### GetPortTriggers {#GetPortTriggers}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port_trigger_rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortTriggerRule'>PortTriggerRule</a>&gt;</code>
            </td>
        </tr></table>

### GetFilters {#GetFilters}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>port_filter_rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FilterRule'>FilterRule</a>&gt;</code>
            </td>
        </tr></table>

### GetIpv6PinHoles {#GetIpv6PinHoles}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pinhole_rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Ipv6PinHoleRule'>Ipv6PinHoleRule</a>&gt;</code>
            </td>
        </tr></table>

### GetDevice {#GetDevice}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#Device'>Device</a></code>
            </td>
        </tr></table>

### GetSystemConfig {#GetSystemConfig}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#SystemConfig'>SystemConfig</a></code>
            </td>
        </tr></table>

### GetRadios {#GetRadios}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>radios</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Radio'>Radio</a>&gt;</code>
            </td>
        </tr></table>

### OnChange {#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Event'>Event</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### Id {#Id}
*Defined in [fuchsia.router.config/common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/common.fidl#9)*



<p>Represents a unique identifier for each element at specific version.
eg. LIF, rules, reservations, clients, etc.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>uuid</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td><p>Time-independent unique identifier of the element.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>version</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Represents a specific config at a point in time in the global config
database. Incremented monotonically at each change.
For any new change requested by the client, this must match the latest
value in the database, otherwise the change will be rejected.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### DnsSearch {#DnsSearch}
*Defined in [fuchsia.router.config/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/dns.fidl#9)*



<p>DnsSearch is the device DNS search configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>servers</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a>&gt;</code>
            </td>
            <td><p>List of DNS servers to consult.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>domain_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td><p>Domain to add to non fully qualified domain names.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### DnsResolverConfig {#DnsResolverConfig}
*Defined in [fuchsia.router.config/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/dns.fidl#28)*



<p>DnsResolverConfig is the device DNS Resolver configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>search</code></td>
            <td>
                <code><a class='link' href='#DnsSearch'>DnsSearch</a></code>
            </td>
            <td><p>DNS search configuration.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>policy</code></td>
            <td>
                <code><a class='link' href='#DnsPolicy'>DnsPolicy</a></code>
            </td>
            <td><p>DNS configuration merge policy.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### DnsForwarderConfig {#DnsForwarderConfig}
*Defined in [fuchsia.router.config/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/dns.fidl#37)*



<p>DNSForwarderConfig is the device DNS Forwarder configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>search</code></td>
            <td>
                <code><a class='link' href='#DnsSearch'>DnsSearch</a></code>
            </td>
            <td><p>Upstream DNS server.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### DnsForwarderEntry {#DnsForwarderEntry}
*Defined in [fuchsia.router.config/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/dns.fidl#44)*



<p>DNSForwarder entry is a name - address mapping.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>names</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DnsForwarder {#DnsForwarder}
*Defined in [fuchsia.router.config/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/dns.fidl#51)*



<p>DNSForwarder the device DNS Forwarder configuration.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#DnsForwarderConfig'>DnsForwarderConfig</a></code>
            </td>
            <td><p>Forwarder configuration.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>resolver</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DnsForwarderEntry'>DnsForwarderEntry</a>&gt;</code>
            </td>
            <td><p>Local Names.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>interfaces</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Id'>Id</a>&gt;</code>
            </td>
            <td><p>Interfaces where the DNS forwarder is enabled.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### AddressPool {#AddressPool}
*Defined in [fuchsia.router.config/lan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/lan.fidl#20)*



<p>Range of addresses in the interface subnet available for DHCP assignment.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>from</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>to</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DhcpReservation {#DhcpReservation}
*Defined in [fuchsia.router.config/lan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/lan.fidl#41)*



<p>DhcpReservation hold a mac to address DHCP association.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
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
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#MacAddress'>MacAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DhcpServerConfig {#DhcpServerConfig}
*Defined in [fuchsia.router.config/lan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/lan.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>options</code></td>
            <td>
                <code><a class='link' href='#DhcpServerOptions'>DhcpServerOptions</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pool</code></td>
            <td>
                <code><a class='link' href='#AddressPool'>AddressPool</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>reservations</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DhcpReservation'>DhcpReservation</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Route {#Route}
*Defined in [fuchsia.router.config/route.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/route.fidl#15)*



<p>Route hold a routeing table entry.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
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
            <td><code>subnet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Subnet'>Subnet</a></code>
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
            <td><code>gateway</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>if_id</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Port {#Port}
*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#69)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PortRange {#PortRange}
*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>from</code></td>
            <td>
                <code><a class='link' href='#port'>port</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>to</code></td>
            <td>
                <code><a class='link' href='#port'>port</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FilterRule {#FilterRule}
*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#57)*



<p>Filter rule is applied on the LAN side; it allows blocking traffic from LAN to WAN.
Normally, all traffic from LAN to WAN is allowed. By applying filter rules, it is possible to
selectively block traffic from LAN devices to services on the WAN side.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#FilterAction'>FilterAction</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>selector</code></td>
            <td>
                <code><a class='link' href='#FlowSelector'>FlowSelector</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PortForwardingRule {#PortForwardingRule}
*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#66)*



<p>Port Forwarding allows remote (WAN) devices to connect to a service hosted on a LAN device.
It forwards all WAN packets (or only those from the optional source_address), destined to any of
the incoming ports, to the target address and port. Target address must be on one of the LANs.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>source_address</code></td>
            <td>
                <code><a class='link' href='#CidrAddress'>CidrAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>destination_ports</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortRange'>PortRange</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>target_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>target_port</code></td>
            <td>
                <code><a class='link' href='#port'>port</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#Protocol'>Protocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PortTriggerRule {#PortTriggerRule}
*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#88)*



<p>Port Triggering provides similar functionality to Port Forwarding. The difference is that it is
the target device that enables the port forwarding functionality.
The target device is not known in advance, and port forwarding is disabled. The first local
device to send traffic to the trigger port becomes the target device, and enables port
forwarding. WAN traffic comming to any of the incoming ports will be forwarded to the trigger
port on the target device.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>incoming_ports</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortRange'>PortRange</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#Protocol'>Protocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>trigger_port</code></td>
            <td>
                <code><a class='link' href='#port'>port</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Ipv6PinHoleRule {#Ipv6PinHoleRule}
*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#100)*



<p>IPv6 firewall pinholes create a hole in the IPv6 firewall.
It will allow traffic from source_address, destined to the indicated ports to pass
from WAN to LAN.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nickname</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>source_address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv6Address'>Ipv6Address</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ports</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortRange'>PortRange</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#Protocol'>Protocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DmzHost {#DmzHost}
*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#110)*



<p>DmzHost is a LAN host that receives all incoming tcp/udp packets that do not match any other rule.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>wan_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>lan_addr</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Error {#Error}
*Defined in [fuchsia.router.config/services.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/services.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='#ErrorCode'>ErrorCode</a></code>
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

### Channel {#Channel}
*Defined in [fuchsia.router.config/wireless.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wireless.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ch</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ChannelNumber'>ChannelNumber</a>&gt;[2]</code>
            </td>
            <td><p>[0] is primary channel, [1] (if provided) is secondary for HT/VHT.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='#ChannelWidth'>ChannelWidth</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Radio {#Radio}
*Defined in [fuchsia.router.config/wireless.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wireless.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code><a class='link' href='#Channel'>Channel</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanNetwork {#WlanNetwork}
*Defined in [fuchsia.router.config/wireless.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wireless.fidl#39)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
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
            <td><code>psk</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>radio_phys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Id'>Id</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enable_band_steering</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Regulatory {#Regulatory}
*Defined in [fuchsia.router.config/wireless.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wireless.fidl#47)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>county_code</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### DnsPolicy {#DnsPolicy}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/dns.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/dns.fidl#17)*

<p>DnsPolicy is the DNS merge policy to use.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_SET</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>STATIC</code></td>
            <td><code>1</code></td>
            <td><p>Can not be replaced by dynamically learned DNS configuration, will overwrite existing configuration.</p>
</td>
        </tr><tr>
            <td><code>REPLACEABLE</code></td>
            <td><code>2</code></td>
            <td><p>Can be replaced by dynamically learned DNS configuration, will not overwrite existing configuration.</p>
</td>
        </tr><tr>
            <td><code>MERGE</code></td>
            <td><code>3</code></td>
            <td><p>Will merge with existing configuration.</p>
</td>
        </tr></table>

### LifType {#LifType}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#49)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WAN</code></td>
            <td><code>1</code></td>
            <td><p>WAN interfaces, by default, will not be allowed to start a DHCP server.
The default is interface up, DHCP client enabled. IPv6 SLAAC.</p>
</td>
        </tr><tr>
            <td><code>LAN</code></td>
            <td><code>2</code></td>
            <td><p>LAN interface by default is up with the ports are up and bridged together, until an IP is statically
configured. A DHCP server can be started or not.</p>
</td>
        </tr><tr>
            <td><code>LAG</code></td>
            <td><code>3</code></td>
            <td><p>LAG interface is a Link aggregation interface.</p>
</td>
        </tr></table>

### Protocol {#Protocol}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#33)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BOTH</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>TCP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UDP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### FilterAction {#FilterAction}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#39)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DROP</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALLOW</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### AclAction {#AclAction}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#118)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PERMIT</code></td>
            <td><code>1</code></td>
            <td><p>Allows traffic to pass.</p>
</td>
        </tr><tr>
            <td><code>DENY</code></td>
            <td><code>2</code></td>
            <td><p>Blocks traffic, dropping the packets.</p>
</td>
        </tr><tr>
            <td><code>REDIRECT</code></td>
            <td><code>3</code></td>
            <td><p>Redirects packets to the destination port.</p>
</td>
        </tr></table>

### AclType {#AclType}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#127)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INGRESS</code></td>
            <td><code>1</code></td>
            <td><p>Ingress ACL is applied on the ingress port, before packet enters the forwarding path.</p>
</td>
        </tr><tr>
            <td><code>EGRESS</code></td>
            <td><code>2</code></td>
            <td><p>Egress ACL is applied on the egress port, after packet has passed the forwarding path.</p>
</td>
        </tr></table>

### ErrorCode {#ErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/services.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/services.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGS</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALREADY_EXISTS</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### WanConnection {#WanConnection}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DIRECT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PPPoE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PPTP</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>L2TP</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### WanAddressMethod {#WanAddressMethod}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#16)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>AUTOMATIC</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>MANUAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### WanIpV6ConnectionMode {#WanIpV6ConnectionMode}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#21)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STATIC</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PASSTHROUGH</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DELEGATION</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### ChannelWidth {#ChannelWidth}
Type: <code>uint32</code>

*Defined in [fuchsia.router.config/wireless.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wireless.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>AUTO</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WIDTH_20_MHZ</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>WIDTH_40_MHZ</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>WIDTH_80_MHZ</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>WIDTH_160_MHZ</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### LanProperties {#LanProperties}


*Defined in [fuchsia.router.config/lan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/lan.fidl#10)*

<p>LanProperties holds the configuration associated with a LAN interface.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address_v4</code></td>
            <td>
                <code><a class='link' href='#CidrAddress'>CidrAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>enable_dhcp_server</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>dhcp_config</code></td>
            <td>
                <code><a class='link' href='#DhcpServerConfig'>DhcpServerConfig</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>address_v6</code></td>
            <td>
                <code><a class='link' href='#CidrAddress'>CidrAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>enable_dns_forwarder</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>enable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### DhcpServerOptions {#DhcpServerOptions}


*Defined in [fuchsia.router.config/lan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/lan.fidl#26)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>lease_time_sec</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>default_gateway</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#Ipv4Address'>Ipv4Address</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>dns_server</code></td>
            <td>
                <code><a class='link' href='#DnsSearch'>DnsSearch</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>enable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### RoutingFeatures {#RoutingFeatures}


*Defined in [fuchsia.router.config/route.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/route.fidl#9)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>rip</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>ospf</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### Device {#Device}


*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#12)*

<p>Device is comprised of a device topology and the device features.
The device topology defines the WAN and LAN interfaces provisioned, indicating
which physical ports are part of an interface, as well as the parameters of the interface.
The device features define the device configuration, and the security and routing features
configured.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>version</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>topology</code></td>
            <td>
                <code><a class='link' href='#Topology'>Topology</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#DeviceConfig'>DeviceConfig</a></code>
            </td>
            <td></td>
        </tr></table>

### Topology {#Topology}


*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#26)*

<p>Topology allows indicating which ports are part of a LAN interface and which ports are part of a WAN interface.
All ports part of a given LAN or WAN are bridged among themselves and an Switch Virtual Interface (SVI)
is created for cpu to get packets (our current bridge).
Typical consumer routers have two LIFs, a WAN and a LAN. These are L3 LIFs, with one port
associated to the WAN side and 1 or more ports (including the WIFI one) associated to the LAN.
The LAN ports are bridged together.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>lifs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Lif'>Lif</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### Lif {#Lif}


*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#40)*

<p>A logical interface (LIF) is an abstraction that represents an L3 interface
(hence, you can assign an IP address to it, for example).
The relationship between logical interfaces and ports are as follows:</p>
<ul>
<li>A LIF can be associated with either a single physical port,
multiple ports (bridge (SVI) or Link aggregation),
or with no port at all (GRE interface, e.g.).</li>
<li>A single port can be associated with multiple LIFs (802.1q tagged port).</li>
<li>A LIF can change associations from one port to another
(in the case of a port failure, e.g.)</li>
</ul>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#LifType'>LifType</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>port_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>vlan</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#LifProperties'>LifProperties</a></code>
            </td>
            <td></td>
        </tr></table>

### SystemConfig {#SystemConfig}


*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#75)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>timezone</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>daylight_savings_time_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>leds_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>hostname</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### DeviceConfig {#DeviceConfig}


*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#83)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>system</code></td>
            <td>
                <code><a class='link' href='#SystemConfig'>SystemConfig</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>dns_resolver</code></td>
            <td>
                <code><a class='link' href='#DnsResolverConfig'>DnsResolverConfig</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>dns_forwarder</code></td>
            <td>
                <code><a class='link' href='#DnsForwarder'>DnsForwarder</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>routing_features</code></td>
            <td>
                <code><a class='link' href='#RoutingFeatures'>RoutingFeatures</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>routes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Route'>Route</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>security_features</code></td>
            <td>
                <code><a class='link' href='#SecurityFeatures'>SecurityFeatures</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>dmz_host</code></td>
            <td>
                <code><a class='link' href='#DmzHost'>DmzHost</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>port_trigger_rulesr</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortTriggerRule'>PortTriggerRule</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>9</td>
            <td><code>port_forwarding_rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortForwardingRule'>PortForwardingRule</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>10</td>
            <td><code>filtering_rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FilterRule'>FilterRule</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>11</td>
            <td><code>pin_hole_rules</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Ipv6PinHoleRule'>Ipv6PinHoleRule</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### SecurityFeatures {#SecurityFeatures}


*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#13)*

<p>Security features define the features enabled or disabled on the router.
For example, NAT, firewall, passthough for common protocols that need it.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>PPTP_PASSTHRU</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>L2TP_PASSTHRU</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>IPSEC_PASSTHRU</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>RTSP_PASSTHRU</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>H323_PASSTHRU</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>SIP_PASSTHRU</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>ALLOW_MULTICAST</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>NAT</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>9</td>
            <td><code>FIREWALL</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>10</td>
            <td><code>V6_FIREWALL</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>11</td>
            <td><code>UPNP</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>12</td>
            <td><code>DROP_ICMP_ECHO</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### FlowSelector {#FlowSelector}


*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#46)*

<p>FlowSelector is the set of packet selectors defining a traffic flow.
a not specified selector represents a match all.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>src_address</code></td>
            <td>
                <code><a class='link' href='#CidrAddress'>CidrAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>src_ports</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortRange'>PortRange</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>dst_address</code></td>
            <td>
                <code><a class='link' href='#CidrAddress'>CidrAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>dst_ports</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PortRange'>PortRange</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>protocol</code></td>
            <td>
                <code><a class='link' href='#Protocol'>Protocol</a></code>
            </td>
            <td></td>
        </tr></table>

### SystemAcl {#SystemAcl}


*Defined in [fuchsia.router.config/security.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#135)*

<p>SystemAcl describes an ACL installed at startup.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>selector</code></td>
            <td>
                <code><a class='link' href='#FlowSelector'>FlowSelector</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>ingress_port</code></td>
            <td>
                <code><a class='link' href='#port'>port</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>egress_port</code></td>
            <td>
                <code><a class='link' href='#port'>port</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>acl_type</code></td>
            <td>
                <code><a class='link' href='#AclType'>AclType</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>acl_action</code></td>
            <td>
                <code><a class='link' href='#AclAction'>AclAction</a></code>
            </td>
            <td></td>
        </tr></table>

### CidrAddress {#CidrAddress}


*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#31)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>address</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>prefix_length</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr></table>

### Credentials {#Credentials}


*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#36)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>user</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>password</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### Pppoe {#Pppoe}


*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#41)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>credentials</code></td>
            <td>
                <code><a class='link' href='#Credentials'>Credentials</a></code>
            </td>
            <td></td>
        </tr></table>

### Pptp {#Pptp}


*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#45)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>credentials</code></td>
            <td>
                <code><a class='link' href='#Credentials'>Credentials</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>server</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
        </tr></table>

### L2tp {#L2tp}


*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#50)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>credentials</code></td>
            <td>
                <code><a class='link' href='#Credentials'>Credentials</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>server</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
        </tr></table>

### WanProperties {#WanProperties}


*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#64)*

<p>WanProperties holds the configuration associated to a WAN interface.
It holds the type of upstream connection and authentication credentials for that connection,
the mechanism to use to obtain an IP address and control of the interface state.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>connection_type</code></td>
            <td>
                <code><a class='link' href='#WanConnection'>WanConnection</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>connection_parameters</code></td>
            <td>
                <code><a class='link' href='#ConnectionParameters'>ConnectionParameters</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>address_method</code></td>
            <td>
                <code><a class='link' href='#WanAddressMethod'>WanAddressMethod</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>address_v4</code></td>
            <td>
                <code><a class='link' href='#CidrAddress'>CidrAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>gateway_v4</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>connection_v6_mode</code></td>
            <td>
                <code><a class='link' href='#WanIpV6ConnectionMode'>WanIpV6ConnectionMode</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>address_v6</code></td>
            <td>
                <code><a class='link' href='#CidrAddress'>CidrAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>gateway_v6</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#IpAddress'>IpAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>9</td>
            <td><code>hostname</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>10</td>
            <td><code>clone_mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#MacAddress'>MacAddress</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>11</td>
            <td><code>mtu</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>12</td>
            <td><code>enable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>13</td>
            <td><code>metric</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### LifProperties {#LifProperties}
*Defined in [fuchsia.router.config/routercfg.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/routercfg.fidl#61)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>wan</code></td>
            <td>
                <code><a class='link' href='#WanProperties'>WanProperties</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>lan</code></td>
            <td>
                <code><a class='link' href='#LanProperties'>LanProperties</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### Event {#Event}
*Defined in [fuchsia.router.config/event.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/event.fidl#10)*

<p>Event defines the events the Router Manager will generate based on configuration state changes.
The event contains only the object that has changed; for example, if a new forwarding rule
is added the event only contains that route, not the full routing table.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>deleted_element</code></td>
            <td>
                <code><a class='link' href='#Id'>Id</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>lif</code></td>
            <td>
                <code><a class='link' href='#Lif'>Lif</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>port</code></td>
            <td>
                <code><a class='link' href='#Port'>Port</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>route</code></td>
            <td>
                <code><a class='link' href='#Route'>Route</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>security_features</code></td>
            <td>
                <code><a class='link' href='#SecurityFeatures'>SecurityFeatures</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>forwarding_rule</code></td>
            <td>
                <code><a class='link' href='#PortForwardingRule'>PortForwardingRule</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>trigger_rule</code></td>
            <td>
                <code><a class='link' href='#PortTriggerRule'>PortTriggerRule</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>filter_rule</code></td>
            <td>
                <code><a class='link' href='#FilterRule'>FilterRule</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>ipv6_pin_hole</code></td>
            <td>
                <code><a class='link' href='#Ipv6PinHoleRule'>Ipv6PinHoleRule</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dhz_host</code></td>
            <td>
                <code><a class='link' href='#DmzHost'>DmzHost</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dhcp_options</code></td>
            <td>
                <code><a class='link' href='#DhcpServerOptions'>DhcpServerOptions</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dhcp_reservation</code></td>
            <td>
                <code><a class='link' href='#DhcpReservation'>DhcpReservation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dns_resolver</code></td>
            <td>
                <code><a class='link' href='#DnsResolverConfig'>DnsResolverConfig</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dns_forwarder</code></td>
            <td>
                <code><a class='link' href='#DnsForwarder'>DnsForwarder</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>system_config</code></td>
            <td>
                <code><a class='link' href='#SystemConfig'>SystemConfig</a></code>
            </td>
            <td></td>
        </tr></table>

### ConnectionParameters {#ConnectionParameters}
*Defined in [fuchsia.router.config/wan.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wan.fidl#55)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>pppoe</code></td>
            <td>
                <code><a class='link' href='#Pppoe'>Pppoe</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>pptp</code></td>
            <td>
                <code><a class='link' href='#Pptp'>Pptp</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>l2tp</code></td>
            <td>
                <code><a class='link' href='#L2tp'>L2tp</a></code>
            </td>
            <td></td>
        </tr></table>

### ChannelNumber {#ChannelNumber}
*Defined in [fuchsia.router.config/wireless.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/wireless.fidl#20)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>number</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>auto_band</code></td>
            <td>
                <code><a class='link' href='#Band'>Band</a></code>
            </td>
            <td></td>
        </tr></table>



## **BITS**

### Band {#Band}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>BAND_2400_MHZ</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>BAND_5000_MHZ</td>
            <td>2</td>
            <td></td>
        </tr></table>





## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr id="port">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.router.config/security.fidl#9">port</a></td>
            <td>
                <code>uint16</code></td>
            <td></td>
        </tr></table>

