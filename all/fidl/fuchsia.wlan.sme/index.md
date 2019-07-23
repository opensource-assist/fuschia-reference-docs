Project: /_project.yaml
Book: /_book.yaml

# fuchsia.wlan.sme


## **PROTOCOLS**

## ScanTransaction {:#ScanTransaction}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#33)*


### OnResult {:#OnResult}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>aps</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.wlan.sme/index.html#EssInfo'>EssInfo</a>&gt;</code>
            </td>
        </tr></table>

### OnFinished {:#OnFinished}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnError {:#OnError}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#ScanError'>ScanError</a></code>
            </td>
        </tr></table>

## ConnectTransaction {:#ConnectTransaction}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#57)*


### OnFinished {:#OnFinished}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#ConnectResultCode'>ConnectResultCode</a></code>
            </td>
        </tr></table>

## ClientSme {:#ClientSme}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#100)*


### Scan {:#Scan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#ScanRequest'>ScanRequest</a></code>
            </td>
        </tr><tr>
            <td><code>txn</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/index.html#ScanTransaction'>ScanTransaction</a>&gt;</code>
            </td>
        </tr></table>



### Connect {:#Connect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#ConnectRequest'>ConnectRequest</a></code>
            </td>
        </tr><tr>
            <td><code>txn</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.wlan.sme/index.html#ConnectTransaction'>ConnectTransaction</a>&gt;?</code>
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
    </table>

### Status {:#Status}


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
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#ClientStatusResponse'>ClientStatusResponse</a></code>
            </td>
        </tr></table>

## ApSme {:#ApSme}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#125)*


### Start {:#Start}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#ApConfig'>ApConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#StartApResultCode'>StartApResultCode</a></code>
            </td>
        </tr></table>

### Stop {:#Stop}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## MeshSme {:#MeshSme}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#153)*


### Join {:#Join}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#MeshConfig'>MeshConfig</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#JoinMeshResultCode'>JoinMeshResultCode</a></code>
            </td>
        </tr></table>

### Leave {:#Leave}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#LeaveMeshResultCode'>LeaveMeshResultCode</a></code>
            </td>
        </tr></table>

### GetMeshPathTable {:#GetMeshPathTable}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#GetMeshPathTableResultCode'>GetMeshPathTableResultCode</a></code>
            </td>
        </tr><tr>
            <td><code>path</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.mesh/index.html'>fuchsia.wlan.mesh</a>/<a class='link' href='../fuchsia.wlan.mesh/index.html#MeshPathTable'>MeshPathTable</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### BssInfo {:#BssInfo}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#10)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bssid</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rx_dbm</code></td>
            <td>
                <code>int8</code>
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
        </tr><tr>
            <td><code>protected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>compatible</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EssInfo {:#EssInfo}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>best_bss</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#BssInfo'>BssInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ScanError {:#ScanError}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#ScanErrorCode'>ScanErrorCode</a></code>
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

### ScanRequest {:#ScanRequest}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#40)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>timeout</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scan_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#ScanType'>ScanType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RadioConfig {:#RadioConfig}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#62)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>override_phy</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#PHY'>PHY</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>override_cbw</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cbw</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#CBW'>CBW</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>override_primary_chan</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_chan</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Empty {:#Empty}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#72)*



 Empty struct used as credential value for open networks.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ConnectRequest {:#ConnectRequest}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#86)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>credential</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#Credential'>Credential</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>radio_cfg</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#RadioConfig'>RadioConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scan_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/index.html'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/index.html#ScanType'>ScanType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ClientStatusResponse {:#ClientStatusResponse}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#94)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>connected_to</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#BssInfo'>BssInfo</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>connecting_to_ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ApConfig {:#ApConfig}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#107)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>password</code></td>
            <td>
                <code>vector&lt;uint8&gt;[64]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>radio_cfg</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#RadioConfig'>RadioConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshConfig {:#MeshConfig}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#130)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mesh_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
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



## **ENUMS**

### ScanErrorCode {:#ScanErrorCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#23)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ConnectResultCode {:#ConnectResultCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#45)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CANCELED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_CREDENTIALS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### StartApResultCode {:#StartApResultCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#113)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALREADY_STARTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CANCELED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIMED_OUT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>PREVIOUS_START_IN_PROGRESS</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>DFS_UNSUPPORTED</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### JoinMeshResultCode {:#JoinMeshResultCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#135)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CANCELED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGUMENTS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>DFS_UNSUPPORTED</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### LeaveMeshResultCode {:#LeaveMeshResultCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#143)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### GetMeshPathTableResultCode {:#GetMeshPathTableResultCode}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#148)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>







## **XUNIONS**

### Credential {:#Credential}
*Defined in [fuchsia.wlan.sme/sme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/lib/wlan/fidl/sme.fidl#75)*

 Information required to connect to a protected network.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>none</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.sme/index.html#Empty'>Empty</a></code>
            </td>
            <td> The network does not use credentials (open networks).
</td>
        </tr><tr>
            <td><code>password</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> Plaintext password (handled as binary data).
</td>
        </tr><tr>
            <td><code>psk</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td> Hash representation of the network passphrase (handled as binary data).
</td>
        </tr></table>




