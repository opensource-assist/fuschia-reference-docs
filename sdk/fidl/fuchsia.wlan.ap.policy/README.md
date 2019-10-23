[TOC]

# fuchsia.wlan.ap.policy


## **PROTOCOLS**

## ApPolicy {#ApPolicy}
*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#11)*


### OpenControlChannels {#OpenControlChannels}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requests</code></td>
            <td>
                <code><a class='link' href='#Requests'>Requests</a></code>
            </td>
        </tr><tr>
            <td><code>updates</code></td>
            <td>
                <code>request&lt;<a class='link' href='#StateUpdates'>StateUpdates</a>&gt;</code>
            </td>
        </tr></table>



## Requests {#Requests}
*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#16)*


### StartAccessPoint {#StartAccessPoint}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#AccessPointParams'>AccessPointParams</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request_status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

### StopAccessPoint {#StopAccessPoint}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request_status</code></td>
            <td>
                <code><a class='link' href='#Status'>Status</a></code>
            </td>
        </tr></table>

## StateUpdates {#StateUpdates}
*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#22)*


### OnAccessPointStatusChange {#OnAccessPointStatusChange}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ap_state</code></td>
            <td>
                <code><a class='link' href='#ApState'>ApState</a></code>
            </td>
        </tr><tr>
            <td><code>previous_ap_state</code></td>
            <td>
                <code><a class='link' href='#ApState'>ApState</a></code>
            </td>
        </tr></table>

### OnAccessPointClientUpdate {#OnAccessPointClientUpdate}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ap_band</code></td>
            <td>
                <code><a class='link' href='#ApBand'>ApBand</a></code>
            </td>
        </tr><tr>
            <td><code>frequency</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>clients</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ApClient'>ApClient</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### Status {#Status}
*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#27)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#RequestStatus'>RequestStatus</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>message</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccessPointParams {#AccessPointParams}
*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#33)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>passphrase</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>band</code></td>
            <td>
                <code><a class='link' href='#ApBand'>ApBand</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ApClient {#ApClient}
*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#60)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mac</code></td>
            <td>
                <code><a class='link' href='../fuchsia.net/'>fuchsia.net</a>/<a class='link' href='../fuchsia.net/#MacAddress'>MacAddress</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ApBand {#ApBand}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#40)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BAND_ANY</code></td>
            <td><code>0</code></td>
            <td> allows the band to switch depending on device
 operating mode and environment
</td>
        </tr><tr>
            <td><code>BAND_2_4GHZ</code></td>
            <td><code>1</code></td>
            <td> restricted to 2.4ghz bands only
</td>
        </tr><tr>
            <td><code>BAND_5GHZ</code></td>
            <td><code>2</code></td>
            <td> restricted to 5ghz bands only
</td>
        </tr></table>

### ApState {#ApState}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.ap.policy/wlan_ap.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.ap/wlan_ap.fidl#51)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>STARTING</code></td>
            <td><code>0</code></td>
            <td> confirmation that the softap interface will attempt to be
 created (this can take seconds on some devices)
</td>
        </tr><tr>
            <td><code>UP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWN</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>











