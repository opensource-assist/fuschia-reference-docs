Project: /_project.yaml
Book: /_book.yaml

# fuchsia.net.stack


## **PROTOCOLS**

## Stack {:#Stack}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#130)*


### AddEthernetInterface {:#AddEthernetInterface}

 Add an Ethernet interface to the network stack. On success, returns the identifier assigned
 by the stack for use in subsequent calls.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>topological_path</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/index.html'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/index.html#Device'>Device</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### DelEthernetInterface {:#DelEthernetInterface}

 Remove an Ethernet interface from the network stack.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_DelEthernetInterface_Result'>Stack_DelEthernetInterface_Result</a></code>
            </td>
        </tr></table>

### ListInterfaces {:#ListInterfaces}

 List all the interfaces available in the network stack.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ifs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InterfaceInfo'>InterfaceInfo</a>&gt;</code>
            </td>
        </tr></table>

### GetInterfaceInfo {:#GetInterfaceInfo}

 Retrieve info about a specific interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
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
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a>?</code>
            </td>
        </tr></table>

### EnableInterface {:#EnableInterface}

 Enable the interface. Packets may be processed by the stack after this call is processed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_EnableInterface_Result'>Stack_EnableInterface_Result</a></code>
            </td>
        </tr></table>

### DisableInterface {:#DisableInterface}

 Disable the interface. The stack will no longer process packets after this call.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_DisableInterface_Result'>Stack_DisableInterface_Result</a></code>
            </td>
        </tr></table>

### AddInterfaceAddress {:#AddInterfaceAddress}

 Add an address to the interface. If the interface already has an address of a given type that
 does not allow duplicates, this method will return an error.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#InterfaceAddress'>InterfaceAddress</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_AddInterfaceAddress_Result'>Stack_AddInterfaceAddress_Result</a></code>
            </td>
        </tr></table>

### DelInterfaceAddress {:#DelInterfaceAddress}

 Remove the address from the interface. If the address is not assigned to the interface, an
 error is returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>addr</code></td>
            <td>
                <code><a class='link' href='#InterfaceAddress'>InterfaceAddress</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_DelInterfaceAddress_Result'>Stack_DelInterfaceAddress_Result</a></code>
            </td>
        </tr></table>

### GetForwardingTable {:#GetForwardingTable}

 List all the entries in the forwarding table for the network stack.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>table</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ForwardingEntry'>ForwardingEntry</a>&gt;</code>
            </td>
        </tr></table>

### AddForwardingEntry {:#AddForwardingEntry}

 Add a new entry to the forwarding table. If the table already contains an entry with the same
 subnet, an error is returned. The entry may be deleted using DelForwardingEntry first.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>entry</code></td>
            <td>
                <code><a class='link' href='#ForwardingEntry'>ForwardingEntry</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_AddForwardingEntry_Result'>Stack_AddForwardingEntry_Result</a></code>
            </td>
        </tr></table>

### DelForwardingEntry {:#DelForwardingEntry}

 Removes the forwarding entry with the given subnet. This will not affect any overlapping
 subnets (superset or subset) so the subnet must exactly match an entry in the forwarding
 table. If no entry for the subnet exists, an error is returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>subnet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#Subnet'>Subnet</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_DelForwardingEntry_Result'>Stack_DelForwardingEntry_Result</a></code>
            </td>
        </tr></table>

### EnablePacketFilter {:#EnablePacketFilter}

 Enable the packet filter on a specific interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_EnablePacketFilter_Result'>Stack_EnablePacketFilter_Result</a></code>
            </td>
        </tr></table>

### DisablePacketFilter {:#DisablePacketFilter}

 Disable the packet filter on a specific interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Stack_DisablePacketFilter_Result'>Stack_DisablePacketFilter_Result</a></code>
            </td>
        </tr></table>

### EnableIpForwarding {:#EnableIpForwarding}

 Enable IP Forwarding.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### DisableIpForwarding {:#DisableIpForwarding}

 Disable IP Forwarding.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnInterfaceStatusChange {:#OnInterfaceStatusChange}

 A status change event is triggered whenever an interface's status changes.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#InterfaceStatusChange'>InterfaceStatusChange</a></code>
            </td>
        </tr></table>

## Log {:#Log}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#204)*


### SetLogLevel {:#SetLogLevel}

 Dynamically set a syslog level.
 See syslog/logger.go for level definition.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>level</code></td>
            <td>
                <code><a class='link' href='#LogLevelFilter'>LogLevelFilter</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Log_SetLogLevel_Result'>Log_SetLogLevel_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Stack_DelEthernetInterface_Response {:#Stack_DelEthernetInterface_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_EnableInterface_Response {:#Stack_EnableInterface_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_DisableInterface_Response {:#Stack_DisableInterface_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_AddInterfaceAddress_Response {:#Stack_AddInterfaceAddress_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_DelInterfaceAddress_Response {:#Stack_DelInterfaceAddress_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_AddForwardingEntry_Response {:#Stack_AddForwardingEntry_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_DelForwardingEntry_Response {:#Stack_DelForwardingEntry_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_EnablePacketFilter_Response {:#Stack_EnablePacketFilter_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Stack_DisablePacketFilter_Response {:#Stack_DisablePacketFilter_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Log_SetLogLevel_Response {:#Log_SetLogLevel_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### InterfaceAddress {:#InterfaceAddress}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ipAddress</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td> The IP address of the interface.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>prefixLen</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td> The length of the network portion of the interface IP address.
</td>
            <td>No default</td>
        </tr>
</table>

### InterfaceInfo {:#InterfaceInfo}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#45)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> An opaque identifier for the interface, assigned by the stack.
 This identifier will never be 0, and will not be reused even if the device is removed and
 subsequently re-added. It is not stable across netstack instances.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#InterfaceProperties'>InterfaceProperties</a></code>
            </td>
            <td> All info of an interface except the interface name.
</td>
            <td>No default</td>
        </tr>
</table>

### InterfaceProperties {:#InterfaceProperties}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#55)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td> Human friendly name of the interface. eg. eth001, wlanx35.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>topopath</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The topological path to the device, representing a stable identifier for the interface
 hardware.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>filepath</code></td>
            <td>
                <code>string</code>
            </td>
            <td> An unstable file path corresponding to the interface. Used in watching the creation
 and destruction of the interface, or in accessing the interface using netdump.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.hardware.ethernet/index.html'>fuchsia.hardware.ethernet</a>/<a class='link' href='../fuchsia.hardware.ethernet/index.html#MacAddress'>MacAddress</a>?</code>
            </td>
            <td> The MAC address of the interface, if available.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mtu</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The maximum transmission unit for the interface in bytes.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>features</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The features present on the interface, as a bitfield. Valid flags are
 fuchsia.hardware.ethernet.`INFO_FEATURE_*`.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>administrativeStatus</code></td>
            <td>
                <code><a class='link' href='#AdministrativeStatus'>AdministrativeStatus</a></code>
            </td>
            <td> The administrative status of the interface.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>physicalStatus</code></td>
            <td>
                <code><a class='link' href='#PhysicalStatus'>PhysicalStatus</a></code>
            </td>
            <td> The physical link status of the interface.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>addresses</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InterfaceAddress'>InterfaceAddress</a>&gt;</code>
            </td>
            <td> The list of addresses currently assigned to the interface.
</td>
            <td>No default</td>
        </tr>
</table>

### ForwardingEntry {:#ForwardingEntry}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#98)*



 An entry in the forwarding table for the network stack.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>subnet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#Subnet'>Subnet</a></code>
            </td>
            <td> The subnet is the key for the entry in the table.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>destination</code></td>
            <td>
                <code><a class='link' href='#ForwardingDestination'>ForwardingDestination</a></code>
            </td>
            <td> The destination that will receive the forwarded packet.
</td>
            <td>No default</td>
        </tr>
</table>

### InterfaceStatusChange {:#InterfaceStatusChange}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#106)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The opaque identifier of the device that had its status change.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#InterfaceStatus'>InterfaceStatus</a></code>
            </td>
            <td> The new status.
</td>
            <td>No default</td>
        </tr>
</table>

### Error {:#Error}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#125)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PresenceStatus {:#PresenceStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#10)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADDED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOVED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### PhysicalStatus {:#PhysicalStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DOWN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### AdministrativeStatus {:#AdministrativeStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#24)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DISABLED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENABLED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ErrorType {:#ErrorType}
Type: <code>uint32</code>

*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#114)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_STATE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIME_OUT</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALREADY_EXISTS</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>IO</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr></table>

### LogLevelFilter {:#LogLevelFilter}
Type: <code>int32</code>

*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#194)*

 Note LogLevelFilter and protocol Log is transient,
 and is planned to be deprecated by logger.fidl's LogLevelFilter.
 This definition is to support syslog/logger.go and Netstack2.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>TRACE</code></td>
            <td><code>-2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEBUG</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INFO</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WARN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FATAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Stack_DelEthernetInterface_Result {:#Stack_DelEthernetInterface_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_DelEthernetInterface_Response'>Stack_DelEthernetInterface_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_EnableInterface_Result {:#Stack_EnableInterface_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_EnableInterface_Response'>Stack_EnableInterface_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_DisableInterface_Result {:#Stack_DisableInterface_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_DisableInterface_Response'>Stack_DisableInterface_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_AddInterfaceAddress_Result {:#Stack_AddInterfaceAddress_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_AddInterfaceAddress_Response'>Stack_AddInterfaceAddress_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_DelInterfaceAddress_Result {:#Stack_DelInterfaceAddress_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_DelInterfaceAddress_Response'>Stack_DelInterfaceAddress_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_AddForwardingEntry_Result {:#Stack_AddForwardingEntry_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_AddForwardingEntry_Response'>Stack_AddForwardingEntry_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_DelForwardingEntry_Result {:#Stack_DelForwardingEntry_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_DelForwardingEntry_Response'>Stack_DelForwardingEntry_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_EnablePacketFilter_Result {:#Stack_EnablePacketFilter_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_EnablePacketFilter_Response'>Stack_EnablePacketFilter_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Stack_DisablePacketFilter_Result {:#Stack_DisablePacketFilter_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Stack_DisablePacketFilter_Response'>Stack_DisablePacketFilter_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### Log_SetLogLevel_Result {:#Log_SetLogLevel_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Log_SetLogLevel_Response'>Log_SetLogLevel_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorType'>ErrorType</a></code>
            </td>
            <td></td>
        </tr></table>

### InterfaceStatus {:#InterfaceStatus}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#31)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>presence</code></td>
            <td>
                <code><a class='link' href='#PresenceStatus'>PresenceStatus</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>physical</code></td>
            <td>
                <code><a class='link' href='#PhysicalStatus'>PhysicalStatus</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>administrative</code></td>
            <td>
                <code><a class='link' href='#AdministrativeStatus'>AdministrativeStatus</a></code>
            </td>
            <td></td>
        </tr></table>

### ForwardingDestination {:#ForwardingDestination}
*Defined in [fuchsia.net.stack/stack.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-net-stack/stack.fidl#89)*

 A ForwardingDestination represents either the device that should transmit a packet or the address
 of the next hop in the route.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>deviceId</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The opaque identifier of the device to which packets should be forwarded.
</td>
        </tr><tr>
            <td><code>nextHop</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/index.html'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/index.html#IpAddress'>IpAddress</a></code>
            </td>
            <td> The IP address of the next hop, used to look up the next forwarding entry.
</td>
        </tr></table>







