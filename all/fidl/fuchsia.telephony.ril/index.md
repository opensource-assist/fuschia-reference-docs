Project: /_project.yaml
Book: /_book.yaml

# fuchsia.telephony.ril


## **PROTOCOLS**

## NetworkConnection {:#NetworkConnection}
*Defined in [fuchsia.telephony.ril/ril.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.ril/ril.fidl#29)*


### Stop {:#Stop}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## Setup {:#Setup}
*Defined in [fuchsia.telephony.ril/ril.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.ril/ril.fidl#44)*

 The Standard Fuchsia RIL (FRIL)

### ConnectTransport {:#ConnectTransport}

 Hand a transport `channel` to the RIL service connecting it to the modem. Most
 modems will require this to be the first method called, since they are dependent
 on this. If a connection is already active, it will return false. If the channel
 is set successfully, it will return true.

 Called globaly per-modem, not per client connection.

 Implementation Detail: current services speak QMI but others will most likely speak other
 binary formats.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Setup_ConnectTransport_Result'>Setup_ConnectTransport_Result</a></code>
            </td>
        </tr></table>

## RadioInterfaceLayer {:#RadioInterfaceLayer}
*Defined in [fuchsia.telephony.ril/ril.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.ril/ril.fidl#59)*

 The Standard Fuchsia RIL (FRIL)

### GetDeviceIdentity {:#GetDeviceIdentity}

 Retrieve the identity of the modem (currently `imei` only).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_GetDeviceIdentity_Result'>RadioInterfaceLayer_GetDeviceIdentity_Result</a></code>
            </td>
        </tr></table>

### RadioPowerStatus {:#RadioPowerStatus}

 Power state of the radio. Currently on On or Off.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_RadioPowerStatus_Result'>RadioInterfaceLayer_RadioPowerStatus_Result</a></code>
            </td>
        </tr></table>

### StartNetwork {:#StartNetwork}

 Activate a network connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>apn</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_StartNetwork_Result'>RadioInterfaceLayer_StartNetwork_Result</a></code>
            </td>
        </tr></table>

### GetNetworkSettings {:#GetNetworkSettings}

 Network settings known to the modem.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_GetNetworkSettings_Result'>RadioInterfaceLayer_GetNetworkSettings_Result</a></code>
            </td>
        </tr></table>

### GetSignalStrength {:#GetSignalStrength}

 Signal Strength (dBm) for LTE networks (total received wideband power).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_GetSignalStrength_Result'>RadioInterfaceLayer_GetSignalStrength_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Setup_ConnectTransport_Response {:#Setup_ConnectTransport_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### RadioInterfaceLayer_GetDeviceIdentity_Response {:#RadioInterfaceLayer_GetDeviceIdentity_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>imei</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RadioInterfaceLayer_RadioPowerStatus_Response {:#RadioInterfaceLayer_RadioPowerStatus_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#RadioPowerState'>RadioPowerState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RadioInterfaceLayer_StartNetwork_Response {:#RadioInterfaceLayer_StartNetwork_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>conn</code></td>
            <td>
                <code><a class='link' href='#NetworkConnection'>NetworkConnection</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RadioInterfaceLayer_GetNetworkSettings_Response {:#RadioInterfaceLayer_GetNetworkSettings_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#NetworkSettings'>NetworkSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RadioInterfaceLayer_GetSignalStrength_Response {:#RadioInterfaceLayer_GetSignalStrength_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dbm</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NetworkSettings {:#NetworkSettings}
*Defined in [fuchsia.telephony.ril/ril.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.ril/ril.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ip_v4_addr</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ip_v4_subnet</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ip_v4_gateway</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ip_v4_dns</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mtu</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### RadioPowerState {:#RadioPowerState}
Type: <code>uint8</code>

*Defined in [fuchsia.telephony.ril/ril.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.ril/ril.fidl#8)*

 Power State of the radio


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OFF</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ON</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### RilError {:#RilError}
Type: <code>uint32</code>

*Defined in [fuchsia.telephony.ril/ril.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.telephony.ril/ril.fidl#15)*

 Errors that the Radio Interface Layer presents to modem
 management interfaces


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NO_RADIO</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NO_SIM</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED_NETWORK_TYPE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNKNOWN_ERROR</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRANSPORT_ERROR</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Setup_ConnectTransport_Result {:#Setup_ConnectTransport_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Setup_ConnectTransport_Response'>Setup_ConnectTransport_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#RilError'>RilError</a></code>
            </td>
            <td></td>
        </tr></table>

### RadioInterfaceLayer_GetDeviceIdentity_Result {:#RadioInterfaceLayer_GetDeviceIdentity_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_GetDeviceIdentity_Response'>RadioInterfaceLayer_GetDeviceIdentity_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#RilError'>RilError</a></code>
            </td>
            <td></td>
        </tr></table>

### RadioInterfaceLayer_RadioPowerStatus_Result {:#RadioInterfaceLayer_RadioPowerStatus_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_RadioPowerStatus_Response'>RadioInterfaceLayer_RadioPowerStatus_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#RilError'>RilError</a></code>
            </td>
            <td></td>
        </tr></table>

### RadioInterfaceLayer_StartNetwork_Result {:#RadioInterfaceLayer_StartNetwork_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_StartNetwork_Response'>RadioInterfaceLayer_StartNetwork_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#RilError'>RilError</a></code>
            </td>
            <td></td>
        </tr></table>

### RadioInterfaceLayer_GetNetworkSettings_Result {:#RadioInterfaceLayer_GetNetworkSettings_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_GetNetworkSettings_Response'>RadioInterfaceLayer_GetNetworkSettings_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#RilError'>RilError</a></code>
            </td>
            <td></td>
        </tr></table>

### RadioInterfaceLayer_GetSignalStrength_Result {:#RadioInterfaceLayer_GetSignalStrength_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#RadioInterfaceLayer_GetSignalStrength_Response'>RadioInterfaceLayer_GetSignalStrength_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#RilError'>RilError</a></code>
            </td>
            <td></td>
        </tr></table>







