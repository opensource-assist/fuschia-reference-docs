Project: /_project.yaml
Book: /_book.yaml

# fuchsia.wlan.service


## **PROTOCOLS**

## Wlan {:#Wlan}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#81)*

 Stub interface; eventually to be replaced by something based on the 802.11
 SME / MSGCF.

### Scan {:#Scan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#ScanRequest'>ScanRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ScanResult'>ScanResult</a></code>
            </td>
        </tr></table>

### Connect {:#Connect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#ConnectConfig'>ConnectConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### Disconnect {:#Disconnect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### Status {:#Status}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#WlanStatus'>WlanStatus</a></code>
            </td>
        </tr></table>

### StartBss {:#StartBss}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>cfg</code></td>
            <td>
                <code><a class='link' href='#BssConfig'>BssConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### StopBss {:#StopBss}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
        </tr></table>

### Stats {:#Stats}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='#WlanStats'>WlanStats</a></code>
            </td>
        </tr></table>

### ClearSavedNetworks {:#ClearSavedNetworks}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### Error {:#Error}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='#ErrCode'>ErrCode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>description</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AP {:#AP}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>string</code>
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
            <td><code>is_secure</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_compatible</code></td>
            <td>
                <code>bool</code>
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

### ScanRequest {:#ScanRequest}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timeout</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ScanResult {:#ScanResult}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>aps</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AP'>AP</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ConnectConfig {:#ConnectConfig}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#42)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>passPhrase</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scanInterval</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bssid</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanStatus {:#WlanStatus}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#60)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>current_ap</code></td>
            <td>
                <code><a class='link' href='#AP'>AP</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BssConfig {:#BssConfig}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#66)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>beaconPeriod</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dtimPeriod</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channel</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WlanStats {:#WlanStats}
*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#73)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.stats/index.html'>fuchsia.wlan.stats</a>/<a class='link' href='../fuchsia.wlan.stats/index.html#IfaceStats'>IfaceStats</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ErrCode {:#ErrCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#10)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_FOUND</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGS</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### State {:#State}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.service/wlan_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.service/wlan_service.fidl#49)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BSS</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>QUERYING</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>SCANNING</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>JOINING</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTHENTICATING</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>ASSOCIATING</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>ASSOCIATED</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>











