[TOC]

# fuchsia.setui


## **PROTOCOLS**

## SetUiService {#SetUiService}
*Defined in [fuchsia.setui/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/service.fidl#30)*

<p>The main interface for UIs to change system settings. Currently, the
settings are scoped to the device, but will eventually be scoped to the user
as is applicable.</p>

### Listen {#Listen}

<p>Begins listening to changes to a given settings object. This may cause the
SetUiService to connect to any applicable device services until all listeners
for a given type are closed.
The service will call the listener with the current state immediately on
initialization.
DEPRECATED: To be removed in favor of Watch</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settingType</code></td>
            <td>
                <code><a class='link' href='#SettingType'>SettingType</a></code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#SettingListener'>SettingListener</a></code>
            </td>
        </tr></table>



### Watch {#Watch}

<p>Returns immediately on first call. Subsequent calls will be delayed until
there is an updated value available.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settingType</code></td>
            <td>
                <code><a class='link' href='#SettingType'>SettingType</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>setting</code></td>
            <td>
                <code><a class='link' href='#SettingsObject'>SettingsObject</a></code>
            </td>
        </tr></table>

### Update {#Update}

<p>Sets the value of a given settings object. Returns once operation
has completed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#SettingsObject'>SettingsObject</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#UpdateResponse'>UpdateResponse</a></code>
            </td>
        </tr></table>

### Mutate {#Mutate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settingType</code></td>
            <td>
                <code><a class='link' href='#SettingType'>SettingType</a></code>
            </td>
        </tr><tr>
            <td><code>mutation</code></td>
            <td>
                <code><a class='link' href='#Mutation'>Mutation</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#MutationResponse'>MutationResponse</a></code>
            </td>
        </tr></table>

### InteractiveMutate {#InteractiveMutate}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settingType</code></td>
            <td>
                <code><a class='link' href='#SettingType'>SettingType</a></code>
            </td>
        </tr><tr>
            <td><code>mutation</code></td>
            <td>
                <code><a class='link' href='#Mutation'>Mutation</a></code>
            </td>
        </tr><tr>
            <td><code>mutation_handles</code></td>
            <td>
                <code><a class='link' href='#MutationHandles'>MutationHandles</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#MutationResponse'>MutationResponse</a></code>
            </td>
        </tr></table>

## SettingListener {#SettingListener}
*Defined in [fuchsia.setui/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/service.fidl#55)*

<p>DEPRECATED: To be removed in favor of Watch</p>

### Notify {#Notify}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>object</code></td>
            <td>
                <code><a class='link' href='#SettingsObject'>SettingsObject</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### StringMutation {#StringMutation}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#13)*



<p>Configuration for string mutations.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>operation</code></td>
            <td>
                <code><a class='link' href='#StringOperation'>StringOperation</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WirelessMutation {#WirelessMutation}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#37)*



<p>Configuration for wireless mutations.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>operation</code></td>
            <td>
                <code><a class='link' href='#WirelessOperation'>WirelessOperation</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>network_id</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>password</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TimeZoneMutation {#TimeZoneMutation}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#44)*



<p>Configuration for time zone mutation.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#TimeZoneInfo'>TimeZoneInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LocalesMutation {#LocalesMutation}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#49)*



<p>Mutation that replaces the existing list of locales with a new list.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>locales</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>See IntlSettings.locales for format.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### HourCycleMutation {#HourCycleMutation}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#55)*



<p>Mutation that changes the <code>HourCycle</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>hour_cycle</code></td>
            <td>
                <code><a class='link' href='#HourCycle'>HourCycle</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TemperatureUnitMutation {#TemperatureUnitMutation}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#60)*



<p>Mutation that changes the <code>TemperatureUnit</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AccountMutationHandles {#AccountMutationHandles}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#75)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SettingsObject {#SettingsObject}
*Defined in [fuchsia.setui/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/service.fidl#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>setting_type</code></td>
            <td>
                <code><a class='link' href='#SettingType'>SettingType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#SettingData'>SettingData</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UpdateResponse {#UpdateResponse}
*Defined in [fuchsia.setui/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/service.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>return_code</code></td>
            <td>
                <code><a class='link' href='#ReturnCode'>ReturnCode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MutationResponse {#MutationResponse}
*Defined in [fuchsia.setui/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/service.fidl#22)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>return_code</code></td>
            <td>
                <code><a class='link' href='#ReturnCode'>ReturnCode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TimeZoneInfo {#TimeZoneInfo}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>current</code></td>
            <td>
                <code><a class='link' href='#TimeZone'>TimeZone</a>?</code>
            </td>
            <td><p>The current time zone. Will be absent if no time zone is currently set.
To update the time zone, set this value.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>available</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TimeZone'>TimeZone</a>&gt;</code>
            </td>
            <td><p>An ordered list of the available time zones.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### TimeZone {#TimeZone}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#57)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The underlying ID value; shouldn't be displayed to the end user.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The user visible description of the time zone.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>region</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td><p>List of sample locations for which the time zone is valid.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### WirelessAccessPoint {#WirelessAccessPoint}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#114)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bssid</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td><p>The associated bssid.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>frequency</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rssi</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The connection strength of the access point. (read-only)</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#ConnectionStatus'>ConnectionStatus</a></code>
            </td>
            <td><p>The current connection state of the access point.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### WirelessNetwork {#WirelessNetwork}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#128)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>internal_id</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>The underlying ID value; shouldn't be displayed to the end user.
(internal / read-only)</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ssid</code></td>
            <td>
                <code>string</code>
            </td>
            <td><p>The published identifier for the access point. (read-only)</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>wpa_auth</code></td>
            <td>
                <code><a class='link' href='#WpaAuth'>WpaAuth</a></code>
            </td>
            <td><p>The auth configuration for the access point.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>wpa_cipher</code></td>
            <td>
                <code><a class='link' href='#WpaCipher'>WpaCipher</a></code>
            </td>
            <td><p>The cipher configuration for the access point.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>access_points</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#WirelessAccessPoint'>WirelessAccessPoint</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### WirelessState {#WirelessState}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#145)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>wireless_networks</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#WirelessNetwork'>WirelessNetwork</a>&gt;</code>
            </td>
            <td><p>The available access points to connect to.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ConnectedState {#ConnectedState}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#157)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reachability</code></td>
            <td>
                <code><a class='link' href='#Reachability'>Reachability</a></code>
            </td>
            <td><p>The current level of connection access.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### IntlSettings {#IntlSettings}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#176)*



<p>Collection of internationalization-related settings stored in Stash.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>locales</code></td>
            <td>
                <code>vector&lt;string&gt;[10]</code>
            </td>
            <td><p>An ordered list of the user's preferred locales, encoded as Unicode BCP-47 locale
identifiers <em>without extensions</em>.
Supports language-Script-REGION-variant.</p>
<p>Examples: &quot;fr&quot;, &quot;en-US&quot;, &quot;sr-Latn-BA&quot;, &quot;sl-nedis&quot;</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>hour_cycle</code></td>
            <td>
                <code><a class='link' href='#HourCycle'>HourCycle</a></code>
            </td>
            <td><p>The user's preferred hour cycle, 12 hours or 24 hours.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td><p>The user's preferred temperature unit.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### StringOperation {#StringOperation}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#8)*

<p>operations supported by string settings.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UPDATE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### AccountOperation {#AccountOperation}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#19)*

<p>Operations supported by account settings.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADD</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SET_LOGIN_OVERRIDE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### WirelessOperation {#WirelessOperation}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#31)*

<p>Operations supported by wireless settings.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONNECT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISCONNECT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ReturnCode {#ReturnCode}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/service.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### SettingType {#SettingType}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>TIME_ZONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONNECTIVITY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>WIRELESS</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTL</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ACCOUNT</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### LoginOverride {#LoginOverride}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#35)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTOLOGIN_GUEST</code></td>
            <td><code>1</code></td>
            <td><p>Do not require an account and login always as guest.</p>
</td>
        </tr><tr>
            <td><code>AUTH_PROVIDER</code></td>
            <td><code>2</code></td>
            <td><p>Requires a provisioned account through auth provider.</p>
</td>
        </tr></table>

### ConnectionStatus {#ConnectionStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#68)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISCONNECTED</code></td>
            <td><code>1</code></td>
            <td><p>The connection is at a resting disconnected state.</p>
</td>
        </tr><tr>
            <td><code>CONNECTING</code></td>
            <td><code>2</code></td>
            <td><p>The connection is being established.</p>
</td>
        </tr><tr>
            <td><code>CONNECTED</code></td>
            <td><code>3</code></td>
            <td><p>The connection is active.</p>
</td>
        </tr><tr>
            <td><code>DISCONNECTING</code></td>
            <td><code>4</code></td>
            <td><p>The connection is in the process of being disconnected.</p>
</td>
        </tr></table>

### WirelessSecurity {#WirelessSecurity}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#84)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSECURED</code></td>
            <td><code>1</code></td>
            <td><p>The network is open and requires no password.</p>
</td>
        </tr><tr>
            <td><code>SECURED</code></td>
            <td><code>2</code></td>
            <td><p>The network is protected by a password.</p>
</td>
        </tr></table>

### WpaAuth {#WpaAuth}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#94)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NONE_OPEN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>NONE_WEP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NONE_WEP_SHARED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>IEEE8021X</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>WPA_PSK</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>WPA_EAP</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>WPA2_PSK</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>WPA2_EAP</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr></table>

### WpaCipher {#WpaCipher}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#106)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>WEP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>TKIP</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>CCMP</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### Reachability {#Reachability}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#150)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WAN</code></td>
            <td><code>1</code></td>
            <td><p>we have access to the wide area network.</p>
</td>
        </tr></table>

### HourCycle {#HourCycle}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#162)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>H12</code></td>
            <td><code>0</code></td>
            <td><p>12-hour clock</p>
</td>
        </tr><tr>
            <td><code>H23</code></td>
            <td><code>1</code></td>
            <td><p>24-hour clock (from 0:00:00 to 23:59:59)</p>
</td>
        </tr></table>

### TemperatureUnit {#TemperatureUnit}
Type: <code>uint32</code>

*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#169)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CELSIUS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>FAHRENHEIT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### AccountMutation {#AccountMutation}


*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#25)*

<p>Configuration for account mutations.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>operation</code></td>
            <td>
                <code><a class='link' href='#AccountOperation'>AccountOperation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>login_override</code></td>
            <td>
                <code><a class='link' href='#LoginOverride'>LoginOverride</a></code>
            </td>
            <td></td>
        </tr></table>

### AccountSettings {#AccountSettings}


*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#43)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#LoginOverride'>LoginOverride</a></code>
            </td>
            <td><p>If set, indicates a login behavior specified at runtime.</p>
</td>
        </tr></table>



## **UNIONS**

### Mutation {#Mutation}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#65)*

<p>Container for setting mutations.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>account_mutation_value</code></td>
            <td>
                <code><a class='link' href='#AccountMutation'>AccountMutation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>string_mutation_value</code></td>
            <td>
                <code><a class='link' href='#StringMutation'>StringMutation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>wireless_mutation_value</code></td>
            <td>
                <code><a class='link' href='#WirelessMutation'>WirelessMutation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>time_zone_mutation_value</code></td>
            <td>
                <code><a class='link' href='#TimeZoneMutation'>TimeZoneMutation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>locales_mutation_value</code></td>
            <td>
                <code><a class='link' href='#LocalesMutation'>LocalesMutation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>hour_cycle_mutation_value</code></td>
            <td>
                <code><a class='link' href='#HourCycleMutation'>HourCycleMutation</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>temperature_unit_mutation_value</code></td>
            <td>
                <code><a class='link' href='#TemperatureUnitMutation'>TemperatureUnitMutation</a></code>
            </td>
            <td></td>
        </tr></table>

### MutationHandles {#MutationHandles}
*Defined in [fuchsia.setui/mutations.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/mutations.fidl#79)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>account_handles</code></td>
            <td>
                <code><a class='link' href='#AccountMutationHandles'>AccountMutationHandles</a></code>
            </td>
            <td></td>
        </tr></table>

### SettingData {#SettingData}
*Defined in [fuchsia.setui/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.setui/types.fidl#16)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>string_value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>time_zone_value</code></td>
            <td>
                <code><a class='link' href='#TimeZoneInfo'>TimeZoneInfo</a></code>
            </td>
            <td><p>The data returned by the time zone service for getting or setting
time zones.</p>
</td>
        </tr><tr>
            <td><code>connectivity</code></td>
            <td>
                <code><a class='link' href='#ConnectedState'>ConnectedState</a></code>
            </td>
            <td><p>The current connected state. (read-only)</p>
</td>
        </tr><tr>
            <td><code>wireless</code></td>
            <td>
                <code><a class='link' href='#WirelessState'>WirelessState</a></code>
            </td>
            <td><p>The wireless state (read-only).</p>
</td>
        </tr><tr>
            <td><code>intl</code></td>
            <td>
                <code><a class='link' href='#IntlSettings'>IntlSettings</a></code>
            </td>
            <td><p>Internationalization settings.</p>
</td>
        </tr><tr>
            <td><code>account</code></td>
            <td>
                <code><a class='link' href='#AccountSettings'>AccountSettings</a></code>
            </td>
            <td></td>
        </tr></table>









