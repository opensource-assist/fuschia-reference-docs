[TOC]

# fuchsia.wlan.tap


## **PROTOCOLS**

## WlantapCtl {#WlantapCtl}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#21)*

<p>Instruct the wlantap-ctl device to creates a fake wlantap-phy device based on the
<code>WlantapPhyConfig</code> passed in. The newly created wlantap-phy device will use the channel to
allow a <code>WlantapPhy</code> client to observe and control its behavior.</p>

### CreatePhy {#CreatePhy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#WlantapPhyConfig'>WlantapPhyConfig</a></code>
            </td>
        </tr><tr>
            <td><code>proxy</code></td>
            <td>
                <code>request&lt;<a class='link' href='#WlantapPhy'>WlantapPhy</a>&gt;</code>
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

## WlantapPhy {#WlantapPhy}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#112)*

<p>Allow the test program to observe and control the behavior of the wlantap-phy device.
A wlantap-phy device is a special vendor device and its driver (Fuchsia being the vendor)
used for testing purpose.
Implements a subset of |wlanmac_ifc_t| and |wlanmac_protocol_ops_t| in
//garnet/lib/wlan/protocol/include/wlan/protocol/mac.h
Implements a subset of |WlanphyImpl| protocol in
//zircon/system/banjo/ddk.protocol.wlanphyimpl/wlanphy-impl.banjo</p>

### Rx {#Rx}

<p>The device &quot;receives&quot; a frame &quot;over the air&quot; and pass it up to driver.</p>

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
                <code><a class='link' href='#WlanRxInfo'>WlanRxInfo</a></code>
            </td>
        </tr></table>



### Status {#Status}

<p>The device report its status to the driver. (Not used).</p>

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



### ReportTxStatus {#ReportTxStatus}

<p>For rate selection (Minstrel), the device's last frame transmission is a success/failure,
with a certain number of retries.</p>

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
                <code><a class='link' href='#WlanTxStatus'>WlanTxStatus</a></code>
            </td>
        </tr></table>



### Tx {#Tx}

<p>The device is to send a frame &quot;over the air&quot;.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='#TxArgs'>TxArgs</a></code>
            </td>
        </tr></table>

### WlanmacStart {#WlanmacStart}

<p>The device created by its parent device (wlantap-phy: wlanphy) is
detected and being connected by wlanstack/wlancfg.
The device is to enter the &quot;running&quot; state.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='#WlanmacStartArgs'>WlanmacStartArgs</a></code>
            </td>
        </tr></table>

### SetChannel {#SetChannel}

<p>The device is to switch to the specified channel.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='#SetChannelArgs'>SetChannelArgs</a></code>
            </td>
        </tr></table>

### ConfigureBss {#ConfigureBss}

<p>AP: The device is to use args.config as a template for beacon frames.
Client: The device is to be configured with this BSS as it peer.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='#ConfigureBssArgs'>ConfigureBssArgs</a></code>
            </td>
        </tr></table>

### SetKey {#SetKey}

<p>The device is to install the keys (often coming from RSN, exceptions apply).</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='#SetKeyArgs'>SetKeyArgs</a></code>
            </td>
        </tr></table>

### SetCountry {#SetCountry}

<p>The device is to change its radio and power settings to conform to the regulation of the
specified country.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>args</code></td>
            <td>
                <code><a class='link' href='#SetCountryArgs'>SetCountryArgs</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### WlantapPhyConfig {#WlantapPhyConfig}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#12)*



<p>Describes the capabilities of the fake wlantap-phy device to be created.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>phy_info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.device/'>fuchsia.wlan.device</a>/<a class='link' href='../fuchsia.wlan.device/#PhyInfo'>PhyInfo</a></code>
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

### WlanRxInfo {#WlanRxInfo}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#28)*



<p>Information pertaining to incoming packets. One WlanRxInfo is associated with each packet.
You are encouraged to use the default value in //src/connectivity/wlan/testing/hw-sim/src/lib.rs
See wlan_rx_info_t for details about each field.</p>


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
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#WlanChan'>WlanChan</a></code>
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

### WlanTxInfo {#WlanTxInfo}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#43)*



<p>Instruction from generic WLAN driver on how to send a packet. One WlanTxInfo per packet.
These values are populated by the wlantap driver and should not be specified manually.
See wlan_tx_info_t for details about each field.</p>


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

### WlanTxPacket {#WlanTxPacket}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#54)*



<p>An outgoing packet that is to be &quot;sent&quot; by the wlantap device. |data| contains the packet
in its wire format.</p>


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
                <code><a class='link' href='#WlanTxInfo'>WlanTxInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanBssConfig {#WlanBssConfig}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#62)*



<p>BSS that is to be configured, or &quot;remembered&quot;, by the wlantap device.
These values are populated by the wlantap driver and should not be specified manually.
See wlan_bss_config_t for details about each field.</p>


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

### WlanKeyConfig {#WlanKeyConfig}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#71)*



<p>Configuration pertaining to security keys, often used by RSN and other secure authentication.
These values are populated by the wlantap driver and should not be specified manually.
See wlan_key_config_t for details about each field.</p>


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

### WlanTxStatusEntry {#WlanTxStatusEntry}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#84)*



<p>One entry in a WlanTxStatus report, 1 report can contain up to 8 entries (see below).
These values are populated by the wlantap driver and should not be specified manually.
See wlan_tx_status_entry_t for details about each field.</p>


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

### WlanTxStatus {#WlanTxStatus}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#92)*



<p>TX status report used by Minstrel rate selection algorithm. One report per packet.
You are encouraged to use the default value in //src/connectivity/wlan/testing/hw-sim/src/lib.rs
See wlan_tx_status_t for details about each field.</p>


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

### SetCountryArgs {#SetCountryArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#101)*



<p>Country code the device is to switch to.
These values are populated by the wlantap driver and should not be specified manually.
See also phy.fidl SetCountryRequest/Response.</p>


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

### TxArgs {#TxArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#152)*





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
                <code><a class='link' href='#WlanTxPacket'>WlanTxPacket</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetChannelArgs {#SetChannelArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#157)*





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
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#WlanChan'>WlanChan</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ConfigureBssArgs {#ConfigureBssArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#162)*





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
                <code><a class='link' href='#WlanBssConfig'>WlanBssConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetKeyArgs {#SetKeyArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#167)*





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
                <code><a class='link' href='#WlanKeyConfig'>WlanKeyConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanmacStartArgs {#WlanmacStartArgs}
*Defined in [fuchsia.wlan.tap/wlantap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/wlantap.fidl#172)*





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















