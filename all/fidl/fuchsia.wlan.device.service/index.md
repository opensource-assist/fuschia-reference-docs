Project: /_project.yaml
Book: /_book.yaml

# fuchsia.wlan.device.service


## **PROTOCOLS**

## DeviceWatcher {:#DeviceWatcher}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#73)*


### OnPhyAdded {:#OnPhyAdded}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### OnPhyRemoved {:#OnPhyRemoved}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### OnIfaceAdded {:#OnIfaceAdded}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### OnIfaceRemoved {:#OnIfaceRemoved}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

## DeviceService {:#DeviceService}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#81)*


### ListPhys {:#ListPhys}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#ListPhysResponse'>ListPhysResponse</a></code>
            </td>
        </tr></table>

### QueryPhy {:#QueryPhy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#QueryPhyRequest'>QueryPhyRequest</a></code>
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
        </tr><tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#QueryPhyResponse'>QueryPhyResponse</a>?</code>
            </td>
        </tr></table>

### ListIfaces {:#ListIfaces}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#ListIfacesResponse'>ListIfacesResponse</a></code>
            </td>
        </tr></table>

### QueryIface {:#QueryIface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
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
        </tr><tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#QueryIfaceResponse'>QueryIfaceResponse</a>?</code>
            </td>
        </tr></table>

### CreateIface {:#CreateIface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#CreateIfaceRequest'>CreateIfaceRequest</a></code>
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
        </tr><tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#CreateIfaceResponse'>CreateIfaceResponse</a>?</code>
            </td>
        </tr></table>

### DestroyIface {:#DestroyIface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#DestroyIfaceRequest'>DestroyIfaceRequest</a></code>
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

### GetClientSme {:#GetClientSme}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>sme</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/index.html'>fuchsia.wlan.sme</a>/<a class='link' href='../fuchsia.wlan.sme/index.html#ClientSme'>ClientSme</a>&gt;</code>
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

### GetApSme {:#GetApSme}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>sme</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/index.html'>fuchsia.wlan.sme</a>/<a class='link' href='../fuchsia.wlan.sme/index.html#ApSme'>ApSme</a>&gt;</code>
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

### GetMeshSme {:#GetMeshSme}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>sme</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/index.html'>fuchsia.wlan.sme</a>/<a class='link' href='../fuchsia.wlan.sme/index.html#MeshSme'>MeshSme</a>&gt;</code>
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

### GetIfaceStats {:#GetIfaceStats}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
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
        </tr><tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.stats/index.html'>fuchsia.wlan.stats</a>/<a class='link' href='../fuchsia.wlan.stats/index.html#IfaceStats'>IfaceStats</a>?</code>
            </td>
        </tr></table>

### GetMinstrelList {:#GetMinstrelList}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
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
        </tr><tr>
            <td><code>peers</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.minstrel/index.html'>fuchsia.wlan.minstrel</a>/<a class='link' href='../fuchsia.wlan.minstrel/index.html#Peers'>Peers</a></code>
            </td>
        </tr></table>

### GetMinstrelStats {:#GetMinstrelStats}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>peer_addr</code></td>
            <td>
                <code>uint8[6]</code>
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
        </tr><tr>
            <td><code>peer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.minstrel/index.html'>fuchsia.wlan.minstrel</a>/<a class='link' href='../fuchsia.wlan.minstrel/index.html#Peer'>Peer</a>?</code>
            </td>
        </tr></table>

### WatchDevices {:#WatchDevices}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DeviceWatcher'>DeviceWatcher</a>&gt;</code>
            </td>
        </tr></table>



### SetCountry {:#SetCountry}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#SetCountryRequest'>SetCountryRequest</a></code>
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

### PhyListItem {:#PhyListItem}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
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

### ListPhysResponse {:#ListPhysResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#17)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>phys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PhyListItem'>PhyListItem</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### QueryPhyRequest {:#QueryPhyRequest}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#21)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### QueryPhyResponse {:#QueryPhyResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/index.html#PhyInfo'>PhyInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### IfaceListItem {:#IfaceListItem}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#29)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
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

### QueryIfaceResponse {:#QueryIfaceResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/index.html#MacRole'>MacRole</a></code>
            </td>
            <td> The role the iface is currently operating in, e.g., client role.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> The iface's global ID.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> Iface's PHY ID.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy_assigned_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td> Local ID assigned by this iface's PHY.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>dev_path</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The iface's device path.
 Note: This field is deprecated.
 Ifaces will soon have no device path.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td> The iface's MAC.
</td>
            <td>No default</td>
        </tr>
</table>

### ListIfacesResponse {:#ListIfacesResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#51)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ifaces</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#IfaceListItem'>IfaceListItem</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateIfaceRequest {:#CreateIfaceRequest}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#55)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/index.html#MacRole'>MacRole</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateIfaceResponse {:#CreateIfaceResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#60)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DestroyIfaceRequest {:#DestroyIfaceRequest}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#64)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCountryRequest {:#SetCountryRequest}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#68)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>alpha2</code></td>
            <td>
                <code>uint8[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













