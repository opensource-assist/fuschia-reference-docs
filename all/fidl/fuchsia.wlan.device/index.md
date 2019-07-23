Project: /_project.yaml
Book: /_book.yaml

# fuchsia.wlan.device


## **PROTOCOLS**

## Phy {:#Phy}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#109)*


### Query {:#Query}


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
                <code><a class='link' href='../fuchsia.wlan.device/index.html#QueryResponse'>QueryResponse</a></code>
            </td>
        </tr></table>

### CreateIface {:#CreateIface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#CreateIfaceRequest'>CreateIfaceRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#CreateIfaceResponse'>CreateIfaceResponse</a></code>
            </td>
        </tr></table>

### DestroyIface {:#DestroyIface}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#DestroyIfaceRequest'>DestroyIfaceRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#DestroyIfaceResponse'>DestroyIfaceResponse</a></code>
            </td>
        </tr></table>

### SetCountry {:#SetCountry}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#SetCountryRequest'>SetCountryRequest</a></code>
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

## Connector {:#Connector}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#120)*

 This protocol is used to connect to the real Phy protocol underlying this device.

### Connect {:#Connect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.wlan.device/index.html#Phy'>Phy</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### HtCapabilities {:#HtCapabilities}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ht_capability_info</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ampdu_params</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>supported_mcs_set</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_ext_capabilities</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_beamforming_capabilities</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>asel_capabilities</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VhtCapabilities {:#VhtCapabilities}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#40)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vht_capability_info</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>supported_vht_mcs_and_nss_set</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ChannelList {:#ChannelList}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#45)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>base_freq</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channels</code></td>
            <td>
                <code>vector&lt;uint8&gt;[200]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BandInfo {:#BandInfo}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#52)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>band_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#Band'>Band</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_caps</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.mlme/index.html'>fuchsia.wlan.mlme</a>/<a class='link' href='../fuchsia.wlan.mlme/index.html#HtCapabilities'>HtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vht_caps</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.mlme/index.html'>fuchsia.wlan.mlme</a>/<a class='link' href='../fuchsia.wlan.mlme/index.html#VhtCapabilities'>VhtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>basic_rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>supported_channels</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#ChannelList'>ChannelList</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PhyInfo {:#PhyInfo}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#60)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dev_path</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>hw_mac_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>supported_phys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.wlan.device/index.html#SupportedPhy'>SupportedPhy</a>&gt;[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>driver_features</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#DriverFeature'>DriverFeature</a>&gt;[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mac_roles</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.wlan.device/index.html#MacRole'>MacRole</a>&gt;[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>caps</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.wlan.device/index.html#Capability'>Capability</a>&gt;[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bands</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.wlan.device/index.html#BandInfo'>BandInfo</a>&gt;[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### QueryResponse {:#QueryResponse}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#79)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#PhyInfo'>PhyInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateIfaceRequest {:#CreateIfaceRequest}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#84)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html#MacRole'>MacRole</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>sme_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateIfaceResponse {:#CreateIfaceResponse}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#90)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>iface_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DestroyIfaceRequest {:#DestroyIfaceRequest}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#95)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DestroyIfaceResponse {:#DestroyIfaceResponse}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#99)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCountryRequest {:#SetCountryRequest}
*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#105)*



 The country code for a target WLAN PHY device.
 alpha2 is ISO 3166-1 code to indicate a country. eg. AF for Afghanistan.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>alpha2</code></td>
            <td>
                <code>uint8[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### SupportedPhy {:#SupportedPhy}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#10)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DSSS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CCK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>OFDM</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>HT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>VHT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### MacRole {:#MacRole}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#18)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CLIENT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>AP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### Capability {:#Capability}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.device/phy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/phy.fidl#24)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SHORT_PREAMBLE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>SPECTRUM_MGMT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SHORT_SLOT_TIME</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>RADIO_MSMT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>










