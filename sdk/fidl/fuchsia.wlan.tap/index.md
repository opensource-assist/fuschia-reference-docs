Project: /_project.yaml
Book: /_book.yaml

# fuchsia.wlan.tap


## **PROTOCOLS**

## WlantapCtl {:#WlantapCtl}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#21)*

 Instruct the wlantap-ctl device to creates a fake wlantap-phy device based on the
 `WlantapPhyConfig` passed in. The newly created wlantap-phy device will use the channel to
 allow a `WlantapPhy` client to observe and control its behavior

### CreatePhy {:#CreatePhy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlantapPhyConfig'>WlantapPhyConfig</a></code>
            </td>
        </tr><tr>
            <td><code>proxy</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.wlan.tap/index.html#WlantapPhy'>WlantapPhy</a>&gt;</code>
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

## WlantapPhy {:#WlantapPhy}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#89)*


### Rx {:#Rx}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlanRxInfo'>WlanRxInfo</a></code>
            </td>
        </tr></table>



### Status {:#Status}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>st</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### ReportTxStatus {:#ReportTxStatus}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>txs</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlanTxStatus'>WlanTxStatus</a></code>
            </td>
        </tr></table>



### Tx {:#Tx}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#TxArgs'>TxArgs</a></code>
            </td>
        </tr></table>

### SetChannel {:#SetChannel}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#SetChannelArgs'>SetChannelArgs</a></code>
            </td>
        </tr></table>

### ConfigureBss {:#ConfigureBss}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#ConfigureBssArgs'>ConfigureBssArgs</a></code>
            </td>
        </tr></table>

### SetKey {:#SetKey}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#SetKeyArgs'>SetKeyArgs</a></code>
            </td>
        </tr></table>

### WlanmacStart {:#WlanmacStart}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlanmacStartArgs'>WlanmacStartArgs</a></code>
            </td>
        </tr></table>

### SetCountry {:#SetCountry}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#SetCountryArgs'>SetCountryArgs</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### WlantapPhyConfig {:#WlantapPhyConfig}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#12)*



 Describes the capabilities of the fake wlantap-phy device to be created.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>phy_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/index.html'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/index.html#PhyInfo'>PhyInfo</a></code>
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
            <td><code>quiet</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanRxInfo {:#WlanRxInfo}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#26)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>rx_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>valid_fields</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>chan</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#WlanChan'>WlanChan</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mcs</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rssi_dbm</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rcpi_dbmh</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>snr_dbh</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanTxInfo {:#WlanTxInfo}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#39)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>tx_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>valid_fields</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_vector_idx</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cbw</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mcs</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanTxPacket {:#WlanTxPacket}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlanTxInfo'>WlanTxInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanBssConfig {:#WlanBssConfig}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#54)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bssid</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bss_type</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>remote</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanKeyConfig {:#WlanKeyConfig}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#61)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>protection</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cipher_oui</code></td>
            <td>
                <code>uint8[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cipher_type</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key_type</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>peer_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key_idx</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanTxStatusEntry {:#WlanTxStatusEntry}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#72)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>tx_vec_idx</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>attempts</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanTxStatus {:#WlanTxStatus}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#78)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_status_entries</code></td>
            <td>
                <code>[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCountryArgs {:#SetCountryArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#85)*





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

### TxArgs {:#TxArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#104)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlanTxPacket'>WlanTxPacket</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetChannelArgs {:#SetChannelArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#109)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>chan</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#WlanChan'>WlanChan</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ConfigureBssArgs {:#ConfigureBssArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#114)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlanBssConfig'>WlanBssConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetKeyArgs {:#SetKeyArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#119)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.tap/index.html#WlanKeyConfig'>WlanKeyConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanmacStartArgs {:#WlanmacStartArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#124)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>wlanmac_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













