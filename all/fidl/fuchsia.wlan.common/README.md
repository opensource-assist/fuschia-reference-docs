[TOC]

# fuchsia.wlan.common




## **STRUCTS**

### WlanChan {#WlanChan}
*Defined in [fuchsia.wlan.common/wlan_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.common/wlan_common.fidl#41)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>primary</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cbw</code></td>
            <td>
                <code><a class='link' href='#CBW'>CBW</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>secondary80</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### RequestStatus {#RequestStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.common/wlan_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.common/wlan_common.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ACKNOWLEDGED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>REJECTED_NOT_SUPPORTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>REJECTED_INCOMPATIBLE_MODE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>REJECTED_ALREADY_IN_USE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>REJECTED_DUPLICATE_REQUEST</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### PHY {#PHY}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.common/wlan_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.common/wlan_common.fidl#18)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>HR</code></td>
            <td><code>1</code></td>
            <td><p>IEEE 802.11b, used for DSSS, HR/DSSS, ERP-DSSS/CCK</p>
</td>
        </tr><tr>
            <td><code>ERP</code></td>
            <td><code>2</code></td>
            <td><p>IEEE 802.11a/g, used for ERP-OFDM</p>
</td>
        </tr><tr>
            <td><code>HT</code></td>
            <td><code>3</code></td>
            <td><p>IEEE 802.11n</p>
</td>
        </tr><tr>
            <td><code>VHT</code></td>
            <td><code>4</code></td>
            <td><p>IEEE 802.11ac</p>
</td>
        </tr><tr>
            <td><code>HEW</code></td>
            <td><code>5</code></td>
            <td><p>IEEE 802.11ax</p>
</td>
        </tr></table>

### CBW {#CBW}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.common/wlan_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.common/wlan_common.fidl#31)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CBW20</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CBW40</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CBW40BELOW</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CBW80</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>CBW160</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>CBW80P80</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### Band {#Band}
Type: <code>uint8</code>

*Defined in [fuchsia.wlan.common/wlan_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.common/wlan_common.fidl#47)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>WLAN_BAND_2GHZ</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WLAN_BAND_5GHZ</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>WLAN_BAND_COUNT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ScanType {#ScanType}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.common/wlan_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.common/wlan_common.fidl#55)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ACTIVE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PASSIVE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### DriverFeature {#DriverFeature}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.common/wlan_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.common/wlan_common.fidl#60)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SCAN_OFFLOAD</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>RATE_SELECTION</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYNTH</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>TX_STATUS_REPORT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>DFS</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>TEMP_DIRECT_SME_CHANNEL</code></td>
            <td><code>3141592</code></td>
            <td><p>Temporary feature flag for incrementally transitioning drivers to use
SME channel on iface creation.</p>
</td>
        </tr><tr>
            <td><code>TEMP_SOFTMAC</code></td>
            <td><code>2718281828</code></td>
            <td><p>Temporary feature flag for driver to indicate this iface a SoftMAC device.
TODO(41640): Remove this flag once FullMAC drivers no longer use SME.</p>
</td>
        </tr></table>













