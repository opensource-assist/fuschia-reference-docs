[TOC]

# fuchsia.net.policy


## **PROTOCOLS**

## BaseInterfaceController {#BaseInterfaceController}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#31)*


### GetInterfaceInfo {#GetInterfaceInfo}

<p>Retrieve info about an interface.</p>

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
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#InterfaceInfo'>InterfaceInfo</a></code>
            </td>
        </tr></table>

### SetInterfaceStatus {#SetInterfaceStatus}

<p>Set the administrative status for an interfance.
If enabled, the interface starts processing packets.
If disabled, the interface stops processing packets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetDHCPClientStatus {#SetDHCPClientStatus}

<p>Set DHCP client status for a specific interface.
If enabled, the interface acquires a dynamic IP address through DHCP server.
If disabled, the interface uses the assigned static IP address.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetName {#SetName}

<p>Set a name for an interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
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

### OnChange {#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#Events'>Events</a></code>
            </td>
        </tr></table>

## StandardInterfaceController {#StandardInterfaceController}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#52)*

<p>Controller of physical and virtual interfaces.</p>

### GetInterfaceInfo {#GetInterfaceInfo}

<p>Retrieve info about an interface.</p>

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
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#InterfaceInfo'>InterfaceInfo</a></code>
            </td>
        </tr></table>

### SetInterfaceStatus {#SetInterfaceStatus}

<p>Set the administrative status for an interfance.
If enabled, the interface starts processing packets.
If disabled, the interface stops processing packets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetDHCPClientStatus {#SetDHCPClientStatus}

<p>Set DHCP client status for a specific interface.
If enabled, the interface acquires a dynamic IP address through DHCP server.
If disabled, the interface uses the assigned static IP address.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetName {#SetName}

<p>Set a name for an interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
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

### OnChange {#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#Events'>Events</a></code>
            </td>
        </tr></table>

## BridgeInterfaceController {#BridgeInterfaceController}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#57)*

<p>Controller of  bridging interfaces.</p>

### GetInterfaceInfo {#GetInterfaceInfo}

<p>Retrieve info about an interface.</p>

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
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#InterfaceInfo'>InterfaceInfo</a></code>
            </td>
        </tr></table>

### SetInterfaceStatus {#SetInterfaceStatus}

<p>Set the administrative status for an interfance.
If enabled, the interface starts processing packets.
If disabled, the interface stops processing packets.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetDHCPClientStatus {#SetDHCPClientStatus}

<p>Set DHCP client status for a specific interface.
If enabled, the interface acquires a dynamic IP address through DHCP server.
If disabled, the interface uses the assigned static IP address.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetName {#SetName}

<p>Set a name for an interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
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

### OnChange {#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#Events'>Events</a></code>
            </td>
        </tr></table>

## Observer {#Observer}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#65)*


### ListInterfaces {#ListInterfaces}

<p>Retrieve info of all the interfaces.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>infos</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#InterfaceInfo'>InterfaceInfo</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetInterfaceInfo {#GetInterfaceInfo}

<p>Retrieve info of a specific interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#InterfaceInfo'>InterfaceInfo</a>?</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### OnChange {#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interface</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#Events'>Events</a></code>
            </td>
        </tr></table>

## BasePolicy {#BasePolicy}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#76)*


### AddInterface {#AddInterface}

<p>Add virtual interfaces.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/#Device'>Device</a></code>
            </td>
        </tr><tr>
            <td><code>interfaceCtl</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StandardInterfaceController'>StandardInterfaceController</a>&gt;</code>
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

### CreateBridge {#CreateBridge}

<p>Create bridging interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interfaces</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr><tr>
            <td><code>interfaceCtl</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BridgeInterfaceController'>BridgeInterfaceController</a>&gt;</code>
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

## PrivilegedPolicy {#PrivilegedPolicy}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#94)*


### GetInterfaceController {#GetInterfaceController}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>interface</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code><a class='link' href='#EthernetControllerRequest'>EthernetControllerRequest</a></code>
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

### InterfaceNameUpdate {#InterfaceNameUpdate}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#12)*



<p>Event for interface name update.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The new name.</p>
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### Events {#Events}


*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#17)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/#InterfaceStatus'>InterfaceStatus</a></code>
            </td>
            <td><p>InterfaceStatus event is triggered whenever an interface's status is changed.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>name</code></td>
            <td>
                <code><a class='link' href='#InterfaceNameUpdate'>InterfaceNameUpdate</a></code>
            </td>
            <td><p>InterfaceNameUpdate event is triggered whenever an interface's name is changed.</p>
</td>
        </tr></table>



## **UNIONS**

### EthernetControllerRequest {#EthernetControllerRequest}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#25)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>standard</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StandardInterfaceController'>StandardInterfaceController</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bridge</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BridgeInterfaceController'>BridgeInterfaceController</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>









