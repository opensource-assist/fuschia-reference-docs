[TOC]

# fuchsia.wlan.stats




## **STRUCTS**

### Counter {#Counter}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint64</code>
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
        </tr>
</table>

### PacketCounter {#PacketCounter}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>in</code></td>
            <td>
                <code><a class='link' href='#Counter'>Counter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code><a class='link' href='#Counter'>Counter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>drop</code></td>
            <td>
                <code><a class='link' href='#Counter'>Counter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>in_bytes</code></td>
            <td>
                <code><a class='link' href='#Counter'>Counter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>out_bytes</code></td>
            <td>
                <code><a class='link' href='#Counter'>Counter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>drop_bytes</code></td>
            <td>
                <code><a class='link' href='#Counter'>Counter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DispatcherStats {#DispatcherStats}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#22)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>any_packet</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mgmt_frame</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ctrl_frame</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data_frame</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RssiStats {#RssiStats}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#34)*



<p>RssiStats count the occurrence of the RSSIs.
RSSI value r's occurrence is counted in the bin[-r],
where r is defined in [-128, 0] in dBm.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>hist</code></td>
            <td>
                <code>vector&lt;uint64&gt;[129]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ClientMlmeStats {#ClientMlmeStats}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#39)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>svc_msg</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data_frame</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mgmt_frame</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tx_frame</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rx_frame</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>assoc_data_rssi</code></td>
            <td>
                <code><a class='link' href='#RssiStats'>RssiStats</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>beacon_rssi</code></td>
            <td>
                <code><a class='link' href='#RssiStats'>RssiStats</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ApMlmeStats {#ApMlmeStats}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#49)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>not_used</code></td>
            <td>
                <code><a class='link' href='#PacketCounter'>PacketCounter</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### IfaceStats {#IfaceStats}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#60)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dispatcher_stats</code></td>
            <td>
                <code><a class='link' href='#DispatcherStats'>DispatcherStats</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mlme_stats</code></td>
            <td>
                <code><a class='link' href='#MlmeStats'>MlmeStats</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### MlmeStats {#MlmeStats}
*Defined in [fuchsia.wlan.stats/wlan_stats.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#55)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>client_mlme_stats</code></td>
            <td>
                <code><a class='link' href='#ClientMlmeStats'>ClientMlmeStats</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>ap_mlme_stats</code></td>
            <td>
                <code><a class='link' href='#ApMlmeStats'>ApMlmeStats</a></code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.stats/wlan_stats.fidl#29">RSSI_BINS</a></td>
            <td>
                    <code>129</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    
</table>



