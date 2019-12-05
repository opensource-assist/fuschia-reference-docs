[TOC]

# fuchsia.wlan.mlme


## **PROTOCOLS**

## MLME {#MLME}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#617)*


### StartScan {#StartScan}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#ScanRequest'>ScanRequest</a></code>
            </td>
        </tr></table>



### OnScanResult {#OnScanResult}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#ScanResult'>ScanResult</a></code>
            </td>
        </tr></table>

### OnScanEnd {#OnScanEnd}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>end</code></td>
            <td>
                <code><a class='link' href='#ScanEnd'>ScanEnd</a></code>
            </td>
        </tr></table>

### JoinReq {#JoinReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#JoinRequest'>JoinRequest</a></code>
            </td>
        </tr></table>



### JoinConf {#JoinConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#JoinConfirm'>JoinConfirm</a></code>
            </td>
        </tr></table>

### AuthenticateReq {#AuthenticateReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#AuthenticateRequest'>AuthenticateRequest</a></code>
            </td>
        </tr></table>



### AuthenticateConf {#AuthenticateConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#AuthenticateConfirm'>AuthenticateConfirm</a></code>
            </td>
        </tr></table>

### AuthenticateInd {#AuthenticateInd}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ind</code></td>
            <td>
                <code><a class='link' href='#AuthenticateIndication'>AuthenticateIndication</a></code>
            </td>
        </tr></table>

### AuthenticateResp {#AuthenticateResp}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#AuthenticateResponse'>AuthenticateResponse</a></code>
            </td>
        </tr></table>



### DeauthenticateReq {#DeauthenticateReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#DeauthenticateRequest'>DeauthenticateRequest</a></code>
            </td>
        </tr></table>



### DeauthenticateConf {#DeauthenticateConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#DeauthenticateConfirm'>DeauthenticateConfirm</a></code>
            </td>
        </tr></table>

### DeauthenticateInd {#DeauthenticateInd}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ind</code></td>
            <td>
                <code><a class='link' href='#DeauthenticateIndication'>DeauthenticateIndication</a></code>
            </td>
        </tr></table>

### AssociateReq {#AssociateReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#AssociateRequest'>AssociateRequest</a></code>
            </td>
        </tr></table>



### AssociateConf {#AssociateConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#AssociateConfirm'>AssociateConfirm</a></code>
            </td>
        </tr></table>

### AssociateInd {#AssociateInd}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ind</code></td>
            <td>
                <code><a class='link' href='#AssociateIndication'>AssociateIndication</a></code>
            </td>
        </tr></table>

### AssociateResp {#AssociateResp}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#AssociateResponse'>AssociateResponse</a></code>
            </td>
        </tr></table>



### DisassociateReq {#DisassociateReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#DisassociateRequest'>DisassociateRequest</a></code>
            </td>
        </tr></table>



### DisassociateConf {#DisassociateConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#DisassociateConfirm'>DisassociateConfirm</a></code>
            </td>
        </tr></table>

### DisassociateInd {#DisassociateInd}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ind</code></td>
            <td>
                <code><a class='link' href='#DisassociateIndication'>DisassociateIndication</a></code>
            </td>
        </tr></table>

### ResetReq {#ResetReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#ResetRequest'>ResetRequest</a></code>
            </td>
        </tr></table>



### StartReq {#StartReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#StartRequest'>StartRequest</a></code>
            </td>
        </tr></table>



### StartConf {#StartConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#StartConfirm'>StartConfirm</a></code>
            </td>
        </tr></table>

### StopReq {#StopReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#StopRequest'>StopRequest</a></code>
            </td>
        </tr></table>



### StopConf {#StopConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#StopConfirm'>StopConfirm</a></code>
            </td>
        </tr></table>

### SetKeysReq {#SetKeysReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#SetKeysRequest'>SetKeysRequest</a></code>
            </td>
        </tr></table>



### DeleteKeysReq {#DeleteKeysReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#DeleteKeysRequest'>DeleteKeysRequest</a></code>
            </td>
        </tr></table>



### EapolReq {#EapolReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#EapolRequest'>EapolRequest</a></code>
            </td>
        </tr></table>



### EapolConf {#EapolConf}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#EapolConfirm'>EapolConfirm</a></code>
            </td>
        </tr></table>

### IncomingMpOpenAction {#IncomingMpOpenAction}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#MeshPeeringOpenAction'>MeshPeeringOpenAction</a></code>
            </td>
        </tr></table>

### SendMpOpenAction {#SendMpOpenAction}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#MeshPeeringOpenAction'>MeshPeeringOpenAction</a></code>
            </td>
        </tr></table>



### IncomingMpConfirmAction {#IncomingMpConfirmAction}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#MeshPeeringConfirmAction'>MeshPeeringConfirmAction</a></code>
            </td>
        </tr></table>

### SendMpConfirmAction {#SendMpConfirmAction}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#MeshPeeringConfirmAction'>MeshPeeringConfirmAction</a></code>
            </td>
        </tr></table>



### MeshPeeringEstablished {#MeshPeeringEstablished}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>peering</code></td>
            <td>
                <code><a class='link' href='#MeshPeeringParams'>MeshPeeringParams</a></code>
            </td>
        </tr></table>



### GetMeshPathTableReq {#GetMeshPathTableReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#GetMeshPathTableRequest'>GetMeshPathTableRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.mesh/'>fuchsia.wlan.mesh</a>/<a class='link' href='../fuchsia.wlan.mesh/#MeshPathTable'>MeshPathTable</a></code>
            </td>
        </tr></table>

### SignalReport {#SignalReport}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ind</code></td>
            <td>
                <code><a class='link' href='#SignalReportIndication'>SignalReportIndication</a></code>
            </td>
        </tr></table>

### EapolInd {#EapolInd}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ind</code></td>
            <td>
                <code><a class='link' href='#EapolIndication'>EapolIndication</a></code>
            </td>
        </tr></table>

### SetControlledPort {#SetControlledPort}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#SetControlledPortRequest'>SetControlledPortRequest</a></code>
            </td>
        </tr></table>



### QueryDeviceInfo {#QueryDeviceInfo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#DeviceInfo'>DeviceInfo</a></code>
            </td>
        </tr></table>

### StatsQueryReq {#StatsQueryReq}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### StatsQueryResp {#StatsQueryResp}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#StatsQueryResponse'>StatsQueryResponse</a></code>
            </td>
        </tr></table>

### ListMinstrelPeers {#ListMinstrelPeers}


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
                <code><a class='link' href='#MinstrelListResponse'>MinstrelListResponse</a></code>
            </td>
        </tr></table>

### GetMinstrelStats {#GetMinstrelStats}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#MinstrelStatsRequest'>MinstrelStatsRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#MinstrelStatsResponse'>MinstrelStatsResponse</a></code>
            </td>
        </tr></table>

### StartCaptureFrames {#StartCaptureFrames}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#StartCaptureFramesRequest'>StartCaptureFramesRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resp</code></td>
            <td>
                <code><a class='link' href='#StartCaptureFramesResponse'>StartCaptureFramesResponse</a></code>
            </td>
        </tr></table>

### StopCaptureFrames {#StopCaptureFrames}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### RelayCapturedFrame {#RelayCapturedFrame}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#CapturedFrameResult'>CapturedFrameResult</a></code>
            </td>
        </tr></table>

### OnChannelSwitched {#OnChannelSwitched}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ChannelSwitchInfo'>ChannelSwitchInfo</a></code>
            </td>
        </tr></table>

## Connector {#Connector}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#722)*

<p>This protocol is used to connect to the interface's underlying MLME.</p>

### Connect {#Connect}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#MLME'>MLME</a>&gt;</code>
            </td>
        </tr></table>





## **STRUCTS**

### ScanRequest {#ScanRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>txn_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bss_type</code></td>
            <td>
                <code><a class='link' href='#BSSTypes'>BSSTypes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
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
            <td><code>scan_type</code></td>
            <td>
                <code><a class='link' href='#ScanTypes'>ScanTypes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>probe_delay</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channel_list</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_channel_time</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_channel_time</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ssid_list</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HtCapabilities {#HtCapabilities}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#69)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>uint8[26]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HtOperation {#HtOperation}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#74)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>uint8[22]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VhtCapabilities {#VhtCapabilities}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#79)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>uint8[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VhtOperation {#VhtOperation}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#84)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>uint8[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BSSDescription {#BSSDescription}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#89)*





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
            <td><code>bss_type</code></td>
            <td>
                <code><a class='link' href='#BSSTypes'>BSSTypes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>beacon_period</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dtim_period</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cap</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>country</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rsne</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vendor_ies</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td><p>All vendor info elements present in the beacon frame. E.g. this may include a WPA1 IE.
This slice should be a valid chain of IEs including IE headers for each element.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rcpi_dbmh</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rsni_dbh</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_cap</code></td>
            <td>
                <code><a class='link' href='#HtCapabilities'>HtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_op</code></td>
            <td>
                <code><a class='link' href='#HtOperation'>HtOperation</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vht_cap</code></td>
            <td>
                <code><a class='link' href='#VhtCapabilities'>VhtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vht_op</code></td>
            <td>
                <code><a class='link' href='#VhtOperation'>VhtOperation</a>?</code>
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
            <td><code>rssi_dbm</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ScanResult {#ScanResult}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#133)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>txn_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bss</code></td>
            <td>
                <code><a class='link' href='#BSSDescription'>BSSDescription</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ScanEnd {#ScanEnd}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#138)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>txn_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>code</code></td>
            <td>
                <code><a class='link' href='#ScanResultCodes'>ScanResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### JoinRequest {#JoinRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#145)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>selected_bss</code></td>
            <td>
                <code><a class='link' href='#BSSDescription'>BSSDescription</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>join_failure_timeout</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nav_sync_delay</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>op_rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#PHY'>PHY</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cbw</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#CBW'>CBW</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### JoinConfirm {#JoinConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#171)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#JoinResultCodes'>JoinResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AuthenticateRequest {#AuthenticateRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#185)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_type</code></td>
            <td>
                <code><a class='link' href='#AuthenticationTypes'>AuthenticationTypes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_failure_timeout</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_content</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AuthenticateConfirm {#AuthenticateConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#206)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_type</code></td>
            <td>
                <code><a class='link' href='#AuthenticationTypes'>AuthenticationTypes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#AuthenticateResultCodes'>AuthenticateResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_content</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AuthenticateIndication {#AuthenticateIndication}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#217)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_type</code></td>
            <td>
                <code><a class='link' href='#AuthenticationTypes'>AuthenticationTypes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AuthenticateResponse {#AuthenticateResponse}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#226)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#AuthenticateResultCodes'>AuthenticateResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeauthenticateRequest {#DeauthenticateRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#304)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>reason_code</code></td>
            <td>
                <code><a class='link' href='#ReasonCode'>ReasonCode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeauthenticateConfirm {#DeauthenticateConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#313)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeauthenticateIndication {#DeauthenticateIndication}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#319)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>reason_code</code></td>
            <td>
                <code><a class='link' href='#ReasonCode'>ReasonCode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AssociateRequest {#AssociateRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#328)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cap_info</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_cap</code></td>
            <td>
                <code><a class='link' href='#HtCapabilities'>HtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vht_cap</code></td>
            <td>
                <code><a class='link' href='#VhtCapabilities'>VhtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rsne</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vendor_ies</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AssociateConfirm {#AssociateConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#355)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#AssociateResultCodes'>AssociateResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>association_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AssociateIndication {#AssociateIndication}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#365)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>listen_interval</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rsne</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AssociateResponse {#AssociateResponse}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#379)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#AssociateResultCodes'>AssociateResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>association_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DisassociateRequest {#DisassociateRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#393)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>reason_code</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DisassociateConfirm {#DisassociateConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#402)*





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

### DisassociateIndication {#DisassociateIndication}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#408)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>reason_code</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ResetRequest {#ResetRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#417)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>set_default_mib</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Country {#Country}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#431)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>alpha2</code></td>
            <td>
                <code>uint8[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>suffix</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StartRequest {#StartRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#439)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bss_type</code></td>
            <td>
                <code><a class='link' href='#BSSTypes'>BSSTypes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>beacon_period</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dtim_period</code></td>
            <td>
                <code>uint8</code>
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
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>country</code></td>
            <td>
                <code><a class='link' href='#Country'>Country</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mesh_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rsne</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phy</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#PHY'>PHY</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cbw</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#CBW'>CBW</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StartConfirm {#StartConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#491)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#StartResultCodes'>StartResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StopRequest {#StopRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#497)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StopConfirm {#StopConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#507)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#StopResultCodes'>StopResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetKeyDescriptor {#SetKeyDescriptor}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#520)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key_type</code></td>
            <td>
                <code><a class='link' href='#KeyType'>KeyType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rsc</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cipher_suite_oui</code></td>
            <td>
                <code>uint8[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cipher_suite_type</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetKeysRequest {#SetKeysRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#531)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>keylist</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SetKeyDescriptor'>SetKeyDescriptor</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeleteKeyDescriptor {#DeleteKeyDescriptor}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#537)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>key_type</code></td>
            <td>
                <code><a class='link' href='#KeyType'>KeyType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeleteKeysRequest {#DeleteKeysRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#543)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>keylist</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DeleteKeyDescriptor'>DeleteKeyDescriptor</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EapolRequest {#EapolRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#549)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>src_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EapolConfirm {#EapolConfirm}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#563)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>result_code</code></td>
            <td>
                <code><a class='link' href='#EapolResultCodes'>EapolResultCodes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshConfiguration {#MeshConfiguration}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#568)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>active_path_sel_proto_id</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>active_path_sel_metric_id</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>congest_ctrl_method_id</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>sync_method_id</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>auth_proto_id</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mesh_formation_info</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mesh_capability</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshPeeringCommon {#MeshPeeringCommon}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#579)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>protocol_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_link_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mesh_id</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mesh_config</code></td>
            <td>
                <code><a class='link' href='#MeshConfiguration'>MeshConfiguration</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_cap</code></td>
            <td>
                <code><a class='link' href='#HtCapabilities'>HtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_op</code></td>
            <td>
                <code><a class='link' href='#HtOperation'>HtOperation</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vht_cap</code></td>
            <td>
                <code><a class='link' href='#VhtCapabilities'>VhtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vht_op</code></td>
            <td>
                <code><a class='link' href='#VhtOperation'>VhtOperation</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshPeeringOpenAction {#MeshPeeringOpenAction}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#593)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>common</code></td>
            <td>
                <code><a class='link' href='#MeshPeeringCommon'>MeshPeeringCommon</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshPeeringConfirmAction {#MeshPeeringConfirmAction}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#598)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>common</code></td>
            <td>
                <code><a class='link' href='#MeshPeeringCommon'>MeshPeeringCommon</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>aid</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>peer_link_id</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshPeeringParams {#MeshPeeringParams}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#604)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>local_aid</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### GetMeshPathTableRequest {#GetMeshPathTableRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#611)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SignalReportIndication {#SignalReportIndication}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#17)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>rssi_dbm</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EapolIndication {#EapolIndication}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>src_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dst_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BandCapabilities {#BandCapabilities}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>band_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#Band'>Band</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rates</code></td>
            <td>
                <code>vector&lt;uint8&gt;[12]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>base_frequency</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channels</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>cap</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ht_cap</code></td>
            <td>
                <code><a class='link' href='#HtCapabilities'>HtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vht_cap</code></td>
            <td>
                <code><a class='link' href='#VhtCapabilities'>VhtCapabilities</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceInfo {#DeviceInfo}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mac_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='#MacRole'>MacRole</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bands</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#BandCapabilities'>BandCapabilities</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>driver_features</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.wlan.common/'>fuchsia.wlan.common</a>/<a class='link' href='../fuchsia.wlan.common/#DriverFeature'>DriverFeature</a>&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StatsQueryResponse {#StatsQueryResponse}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#57)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>stats</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.stats/'>fuchsia.wlan.stats</a>/<a class='link' href='../fuchsia.wlan.stats/#IfaceStats'>IfaceStats</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MinstrelListResponse {#MinstrelListResponse}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#61)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peers</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.minstrel/'>fuchsia.wlan.minstrel</a>/<a class='link' href='../fuchsia.wlan.minstrel/#Peers'>Peers</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MinstrelStatsRequest {#MinstrelStatsRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#65)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mac_addr</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MinstrelStatsResponse {#MinstrelStatsResponse}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#69)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.wlan.minstrel/'>fuchsia.wlan.minstrel</a>/<a class='link' href='../fuchsia.wlan.minstrel/#Peer'>Peer</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetControlledPortRequest {#SetControlledPortRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#75)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>peer_sta_address</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#ControlledPortState'>ControlledPortState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StartCaptureFramesRequest {#StartCaptureFramesRequest}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#109)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mgmt_frame_flags</code></td>
            <td>
                <code><a class='link' href='#MgmtFrameCaptureFlags'>MgmtFrameCaptureFlags</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StartCaptureFramesResponse {#StartCaptureFramesResponse}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#113)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>supported_mgmt_frames</code></td>
            <td>
                <code><a class='link' href='#MgmtFrameCaptureFlags'>MgmtFrameCaptureFlags</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CapturedFrameResult {#CapturedFrameResult}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#118)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>frame</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ChannelSwitchInfo {#ChannelSwitchInfo}
*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#125)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>new_channel</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### BSSTypes {#BSSTypes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INFRASTRUCTURE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PERSONAL</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INDEPENDENT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ANY_BSS</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### ScanTypes {#ScanTypes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#26)*



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

### ScanResultCodes {#ScanResultCodes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#126)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_ARGS</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### JoinResultCodes {#JoinResultCodes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#165)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>JOIN_FAILURE_TIMEOUT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### AuthenticationTypes {#AuthenticationTypes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#177)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OPEN_SYSTEM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SHARED_KEY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAST_BSS_TRANSITION</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>SAE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### AuthenticateResultCodes {#AuthenticateResultCodes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#196)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ANTI_CLOGGING_TOKEN_REQUIRED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>FINITE_CYCLIC_GROUP_NOT_SUPPORTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTHENTICATION_REJECTED</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTH_FAILURE_TIMEOUT</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### ReasonCode {#ReasonCode}
Type: <code>uint16</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#236)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED_REASON</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_AUTHENTICATION</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEAVING_NETWORK_DEAUTH</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INACTIVITY</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NO_MORE_STAS</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_CLASS2_FRAME</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_CLASS3_FRAME</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>LEAVING_NETWORK_DISASSOC</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_AUTHENTICATED</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNACCEPTABLE_POWER_CA</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNACCEPTABLE_SUPPORTED_CHANNELS</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr><tr>
            <td><code>BSS_TRANSITION_DISASSOC</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_ELEMENT</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr><tr>
            <td><code>MIC_FAILURE</code></td>
            <td><code>14</code></td>
            <td></td>
        </tr><tr>
            <td><code>FOURWAY_HANDSHAKE_TIMEOUT</code></td>
            <td><code>15</code></td>
            <td></td>
        </tr><tr>
            <td><code>GK_HANDSHAKE_TIMEOUT</code></td>
            <td><code>16</code></td>
            <td></td>
        </tr><tr>
            <td><code>HANDSHAKE_ELEMENT_MISMATCH</code></td>
            <td><code>17</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_GROUP_CIPHER</code></td>
            <td><code>18</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_PAIRWISE_CIPHER</code></td>
            <td><code>19</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_AKMP</code></td>
            <td><code>20</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED_RSNE_VERSION</code></td>
            <td><code>21</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_RSNE_CAPABILITIES</code></td>
            <td><code>22</code></td>
            <td></td>
        </tr><tr>
            <td><code>IEEE802_1_X_AUTH_FAILED</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_CIPHER_OUT_OF_POLICY</code></td>
            <td><code>24</code></td>
            <td></td>
        </tr><tr>
            <td><code>TDLS_PEER_UNREACHABLE</code></td>
            <td><code>25</code></td>
            <td></td>
        </tr><tr>
            <td><code>TDLS_UNSPECIFIED_REASON</code></td>
            <td><code>26</code></td>
            <td></td>
        </tr><tr>
            <td><code>SSP_REQUESTED_DISASSOC</code></td>
            <td><code>27</code></td>
            <td></td>
        </tr><tr>
            <td><code>NO_SSP_ROAMING_AGREEMENT</code></td>
            <td><code>28</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAD_CIPHER_OR_AKM</code></td>
            <td><code>29</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_AUTHORIZED_THIS_LOCATION</code></td>
            <td><code>30</code></td>
            <td></td>
        </tr><tr>
            <td><code>SERVICE_CHANGE_PRECLUDES_TS</code></td>
            <td><code>31</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSPECIFIED_QOS_REASON</code></td>
            <td><code>32</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_ENOUGH_BANDWIDTH</code></td>
            <td><code>33</code></td>
            <td></td>
        </tr><tr>
            <td><code>MISSING_ACKS</code></td>
            <td><code>34</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXCEEDED_TXOP</code></td>
            <td><code>35</code></td>
            <td></td>
        </tr><tr>
            <td><code>STA_LEAVING</code></td>
            <td><code>36</code></td>
            <td></td>
        </tr><tr>
            <td><code>END_TS_BA_DLS</code></td>
            <td><code>37</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_TS_BA</code></td>
            <td><code>38</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIMEOUT</code></td>
            <td><code>39</code></td>
            <td></td>
        </tr><tr>
            <td><code>PEERKEY_MISMATCH</code></td>
            <td><code>45</code></td>
            <td></td>
        </tr><tr>
            <td><code>PEER_INITIATED</code></td>
            <td><code>46</code></td>
            <td></td>
        </tr><tr>
            <td><code>AP_INITIATED</code></td>
            <td><code>47</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_FT_ACTION_FRAME_COUNT</code></td>
            <td><code>48</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_PMKID</code></td>
            <td><code>49</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_MDE</code></td>
            <td><code>50</code></td>
            <td></td>
        </tr><tr>
            <td><code>REASON_INVALID_FTE</code></td>
            <td><code>51</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_PEERING_CANCELED</code></td>
            <td><code>52</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_MAX_PEERS</code></td>
            <td><code>53</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_CONFIGURATION_POLICY_VIOLATION</code></td>
            <td><code>54</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_CLOSE_RCVD</code></td>
            <td><code>55</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_MAX_RETRIES</code></td>
            <td><code>56</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_CONFIRM_TIMEOUT</code></td>
            <td><code>57</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_INVALID_GTK</code></td>
            <td><code>58</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_INCONSISTENT_PARAMETERS</code></td>
            <td><code>59</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_INVALID_SECURITY_CAPABILITY</code></td>
            <td><code>60</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_PATH_ERROR_NO_PROXY_INFORMATION</code></td>
            <td><code>61</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_PATH_ERROR_NO_FORWARDING_INFORMATION</code></td>
            <td><code>62</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_PATH_ERROR_DESTINATION_UNREACHABLE</code></td>
            <td><code>63</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAC_ADDRESS_ALREADY_EXISTS_IN_MBSS</code></td>
            <td><code>64</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_CHANNEL_SWITCH_REGULATORY_REQUIREMENTS</code></td>
            <td><code>65</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH_CHANNEL_SWITCH_UNSPECIFIED</code></td>
            <td><code>66</code></td>
            <td></td>
        </tr></table>

### AssociateResultCodes {#AssociateResultCodes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#343)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED_REASON_UNSPECIFIED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED_NOT_AUTHENTICATED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED_CAPABILITIES_MISMATCH</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED_EXTERNAL_REASON</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED_AP_OUT_OF_MEMORY</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED_BASIC_RATES_MISMATCH</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>REJECTED_EMERGENCY_SERVICES_NOT_SUPPORTED</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>REFUSED_TEMPORARILY</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr></table>

### StartResultCodes {#StartResultCodes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#483)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BSS_ALREADY_STARTED_OR_JOINED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>RESET_REQUIRED_BEFORE_START</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_SUPPORTED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### StopResultCodes {#StopResultCodes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#501)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BSS_ALREADY_STOPPED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERNAL_ERROR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### KeyType {#KeyType}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#513)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>GROUP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PAIRWISE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>PEER_KEY</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>IGTK</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### EapolResultCodes {#EapolResultCodes}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#557)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUCCESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRANSMISSION_FAILURE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### MacRole {#MacRole}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#29)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CLIENT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>AP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>MESH</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### ControlledPortState {#ControlledPortState}
Type: <code>uint32</code>

*Defined in [fuchsia.wlan.mlme/wlan_mlme_ext.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme_ext.fidl#80)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CLOSED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>OPEN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>









## **BITS**

### MgmtFrameCaptureFlags {#MgmtFrameCaptureFlags}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>ASSOC_REQ</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>ASSOC_RESP</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>REASSOC_REQ</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>REASSOC_RESP</td>
            <td>8</td>
            <td></td>
        </tr><tr>
            <td>PROBE_REQ</td>
            <td>16</td>
            <td></td>
        </tr><tr>
            <td>PROBE_RESP</td>
            <td>32</td>
            <td></td>
        </tr><tr>
            <td>TIMING_AD</td>
            <td>64</td>
            <td></td>
        </tr><tr>
            <td>BEACON</td>
            <td>256</td>
            <td></td>
        </tr><tr>
            <td>ATIM</td>
            <td>512</td>
            <td></td>
        </tr><tr>
            <td>DISASSOC</td>
            <td>1024</td>
            <td></td>
        </tr><tr>
            <td>AUTH</td>
            <td>2048</td>
            <td></td>
        </tr><tr>
            <td>DEAUTH</td>
            <td>4096</td>
            <td></td>
        </tr><tr>
            <td>ACTION</td>
            <td>8192</td>
            <td></td>
        </tr><tr>
            <td>ACTION_NO_ACK</td>
            <td>16384</td>
            <td></td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#58">HT_CAP_LEN</a></td>
            <td>
                    <code>26</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#60">HT_OP_LEN</a></td>
            <td>
                    <code>22</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#62">VHT_CAP_LEN</a></td>
            <td>
                    <code>12</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#64">VHT_OP_LEN</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#66">RATES_MAX_LEN</a></td>
            <td>
                    <code>12</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#425">countryEnvironAll</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#426">countryEnvironOutdoor</a></td>
            <td>
                    <code>79</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#427">countryEnvironIndoor</a></td>
            <td>
                    <code>73</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#428">countryEnvironNonCountry</a></td>
            <td>
                    <code>88</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.wlan.mlme/wlan_mlme.fidl#55">CapabilityInfo</a></td>
            <td>
                <code>uint16</code></td>
            <td></td>
        </tr></table>

