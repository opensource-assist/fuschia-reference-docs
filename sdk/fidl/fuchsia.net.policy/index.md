Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.policy


## **PROTOCOLS**

## BaseInterfaceController {:#BaseInterfaceController}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#42)*


### GetInterfaceInfo {:#GetInterfaceInfo}

 Retrieve info about an interface.

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
                <code><a class='link' href='#InterfaceInfo'>InterfaceInfo</a></code>
            </td>
        </tr></table>

### SetInterfaceStatus {:#SetInterfaceStatus}

 Set the administrative status for an interfance.
 If enabled, the interface starts processing packets.
 If disabled, the interface stops processing packets.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetDHCPClientStatus {:#SetDHCPClientStatus}

 Set DHCP client status for a specific interface.
 If enabled, the interface acquires a dynamic IP address through DHCP server.
 If disabled, the interface uses the assigned static IP address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### UpdateAddress {:#UpdateAddress}

 Add/Remove IP address for an interface.
 Remove only if IP address is an exact match.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addressDiff</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#InterfaceAddressDiff'>InterfaceAddressDiff</a></code>
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

### SetName {:#SetName}

 Set a name for an interface.

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

### OnChange {:#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#Events'>Events</a></code>
            </td>
        </tr></table>

## StandardInterfaceController {:#StandardInterfaceController}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#67)*

 Controller of physical and virtual interfaces.

### GetInterfaceInfo {:#GetInterfaceInfo}

 Retrieve info about an interface.

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
                <code><a class='link' href='#InterfaceInfo'>InterfaceInfo</a></code>
            </td>
        </tr></table>

### SetInterfaceStatus {:#SetInterfaceStatus}

 Set the administrative status for an interfance.
 If enabled, the interface starts processing packets.
 If disabled, the interface stops processing packets.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetDHCPClientStatus {:#SetDHCPClientStatus}

 Set DHCP client status for a specific interface.
 If enabled, the interface acquires a dynamic IP address through DHCP server.
 If disabled, the interface uses the assigned static IP address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### UpdateAddress {:#UpdateAddress}

 Add/Remove IP address for an interface.
 Remove only if IP address is an exact match.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addressDiff</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#InterfaceAddressDiff'>InterfaceAddressDiff</a></code>
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

### SetName {:#SetName}

 Set a name for an interface.

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

### OnChange {:#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#Events'>Events</a></code>
            </td>
        </tr></table>

## BridgeInterfaceController {:#BridgeInterfaceController}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#72)*

 Controller of  bridging interfaces.

### GetInterfaceInfo {:#GetInterfaceInfo}

 Retrieve info about an interface.

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
                <code><a class='link' href='#InterfaceInfo'>InterfaceInfo</a></code>
            </td>
        </tr></table>

### SetInterfaceStatus {:#SetInterfaceStatus}

 Set the administrative status for an interfance.
 If enabled, the interface starts processing packets.
 If disabled, the interface stops processing packets.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### SetDHCPClientStatus {:#SetDHCPClientStatus}

 Set DHCP client status for a specific interface.
 If enabled, the interface acquires a dynamic IP address through DHCP server.
 If disabled, the interface uses the assigned static IP address.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#AdministrativeStatus'>AdministrativeStatus</a></code>
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

### UpdateAddress {:#UpdateAddress}

 Add/Remove IP address for an interface.
 Remove only if IP address is an exact match.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>addressDiff</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#InterfaceAddressDiff'>InterfaceAddressDiff</a></code>
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

### SetName {:#SetName}

 Set a name for an interface.

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

### OnChange {:#OnChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>events</code></td>
            <td>
                <code><a class='link' href='#Events'>Events</a></code>
            </td>
        </tr></table>

## Observer {:#Observer}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#80)*


### ListInterfaces {:#ListInterfaces}

 Retrieve info of all the interfaces.

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
                <code>vector&lt;<a class='link' href='#InterfaceInfo'>InterfaceInfo</a>&gt;?</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### GetInterfaceInfo {:#GetInterfaceInfo}

 Retrieve info of a specific interface.

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
                <code><a class='link' href='#InterfaceInfo'>InterfaceInfo</a>?</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### OnChange {:#OnChange}




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

## BasePolicy {:#BasePolicy}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#91)*


### AddInterface {:#AddInterface}

 Add virtual interfaces.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/index.html'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/index.html#Device'>Device</a></code>
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

### CreateBridge {:#CreateBridge}

 Create bridging interface.

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

## PrivilegedPolicy {:#PrivilegedPolicy}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#109)*


### GetInterfaceController {:#GetInterfaceController}


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

### InterfaceInfo {:#InterfaceInfo}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Interface name.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#InterfaceProperties'>InterfaceProperties</a></code>
            </td>
            <td> All info of an interface except the interface name.
</td>
            <td>No default</td>
        </tr>
</table>

### InterfaceNameUpdate {:#InterfaceNameUpdate}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#20)*



 Event for interface name update.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The new name.
</td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### Events {:#Events}


*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#25)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#InterfaceStatus'>InterfaceStatus</a></code>
            </td>
            <td> InterfaceStatus event is triggered whenever an interface's status is changed.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>addressDiff</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net.stack/index.html'>fuchsia.net.stack</a>/<a class='link' href='../fuchsia.net.stack/index.html#InterfaceAddressDiff'>InterfaceAddressDiff</a></code>
            </td>
            <td> InterfaceAddressDiff event is triggered whenever the interface's addresses are changed.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>name</code></td>
            <td>
                <code><a class='link' href='#InterfaceNameUpdate'>InterfaceNameUpdate</a></code>
            </td>
            <td> InterfaceNameUpdate event is triggered whenever an interface's name is changed.
</td>
        </tr></table>



## **UNIONS**

### EthernetControllerRequest {:#EthernetControllerRequest}
*Defined in [fuchsia.net.policy/policy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.net.policy/policy.fidl#36)*


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







