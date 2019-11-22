[TOC]

# fuchsia.wlan.device.service


## **PROTOCOLS**

## DeviceWatcher {#DeviceWatcher}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#68)*


### OnPhyAdded {#OnPhyAdded}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### OnPhyRemoved {#OnPhyRemoved}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### OnIfaceAdded {#OnIfaceAdded}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### OnIfaceRemoved {#OnIfaceRemoved}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

## DeviceService {#DeviceService}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#76)*


### ListPhys {#ListPhys}


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

### QueryPhy {#QueryPhy}


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

### ListIfaces {#ListIfaces}


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

### QueryIface {#QueryIface}


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

### CreateIface {#CreateIface}


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

### DestroyIface {#DestroyIface}


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

### GetClientSme {#GetClientSme}


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
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/'>fuchsia.wlan.sme</a>/<a class='link' href='../fuchsia.wlan.sme/#ClientSme'>ClientSme</a>&gt;</code>
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

### GetApSme {#GetApSme}


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
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/'>fuchsia.wlan.sme</a>/<a class='link' href='../fuchsia.wlan.sme/#ApSme'>ApSme</a>&gt;</code>
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

### GetMeshSme {#GetMeshSme}


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
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/'>fuchsia.wlan.sme</a>/<a class='link' href='../fuchsia.wlan.sme/#MeshSme'>MeshSme</a>&gt;</code>
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

### GetIfaceStats {#GetIfaceStats}


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
                <code><a class='link' href='../fuchsia.wlan.stats/'>fuchsia.wlan.stats</a>/<a class='link' href='../fuchsia.wlan.stats/#IfaceStats'>IfaceStats</a>?</code>
            </td>
        </tr></table>

### GetMinstrelList {#GetMinstrelList}


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
                <code><a class='link' href='../fuchsia.wlan.minstrel/'>fuchsia.wlan.minstrel</a>/<a class='link' href='../fuchsia.wlan.minstrel/#Peers'>Peers</a></code>
            </td>
        </tr></table>

### GetMinstrelStats {#GetMinstrelStats}


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
                <code><a class='link' href='../fuchsia.wlan.minstrel/'>fuchsia.wlan.minstrel</a>/<a class='link' href='../fuchsia.wlan.minstrel/#Peer'>Peer</a>?</code>
            </td>
        </tr></table>

### WatchDevices {#WatchDevices}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DeviceWatcher'>DeviceWatcher</a>&gt;</code>
            </td>
        </tr></table>



### SetCountry {#SetCountry}


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

### PhyListItem {#PhyListItem}
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

### ListPhysResponse {#ListPhysResponse}
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

### QueryPhyRequest {#QueryPhyRequest}
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

### QueryPhyResponse {#QueryPhyResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/#PhyInfo'>PhyInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### IfaceListItem {#IfaceListItem}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#29)*





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

### QueryIfaceResponse {#QueryIfaceResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#33)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/#MacRole'>MacRole</a></code>
            </td>
            <td><p>The role the iface is currently operating in, e.g., client role.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The iface's global ID.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Iface's PHY ID.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy_assigned_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Local ID assigned by this iface's PHY.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td><p>The iface's MAC.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ListIfacesResponse {#ListIfacesResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#46)*





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

### CreateIfaceRequest {#CreateIfaceRequest}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#50)*





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
                <code><a class='link' href='../fuchsia.wlan.device/'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/#MacRole'>MacRole</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateIfaceResponse {#CreateIfaceResponse}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#55)*





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

### DestroyIfaceRequest {#DestroyIfaceRequest}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#59)*





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

### SetCountryRequest {#SetCountryRequest}
*Defined in [fuchsia.wlan.device.service/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/service.fidl#63)*





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













