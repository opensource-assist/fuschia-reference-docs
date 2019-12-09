[TOC]

# fuchsia.lowpan


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.lowpan/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/device.fidl#7)*


### Provision {#Provision}

<p>Provision the interface for the network
described by identity and credential. This
is similar to <code>Join</code>, except that (assuming
the identity and credential are valid) it
will always succeed, even if there are no
peers nearby.</p>
<p>This method returns immediately. You can be
notified when this process is complete by
adding a callback and handling the following:</p>
<ul>
<li><code>Listener::OnProvisionException</code>, which is called
to report errors.</li>
<li><code>Listener::OnStateChanged</code>, which will transition
to <code>State::ATTACHED</code> upon success.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#ProvisioningParams'>ProvisioningParams</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Device_Provision_Result'>Device_Provision_Result</a></code>
            </td>
        </tr></table>

### Leave {#Leave}

<p>Bring down the network interface and forget
all non-volatile details about the current network.</p>
<p>This method returns immediately. You can be notified
when this process is complete by adding a callback
and handling the following:</p>
<ul>
<li><code>Listener::OnStateChanged</code>, which will transition
to <code>State::OFFLINE</code>.</li>
<li><code>Listener::OnIdentityChanged</code>, which will be called
with an identity of <code>null</code>/<code>None</code>.</li>
</ul>
<p>If the interface was not previously provisioned,
calling this method does nothing.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Reset {#Reset}

<p>Resets this network interface, returning
all volatile state to default values. Any
information stored in non-volatile memory
is preserved. If the interface was attached
to a network, this method will cause the
interface to detach. In that case, once the
interface has finished initialization the
interface will attempt to reattach to the
previous network.</p>
<p>This method is the only way to clear <code>State::FAULT</code>.</p>
<p>This method returns immediately. You can be
notified when this process is complete by
adding a listener and handling the following:</p>
<ul>
<li><code>Listener::OnStateChanged</code>, which will
indicate various state changes after reset.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetEnabled {#SetEnabled}

<p>Enables or disables the interface.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### GetSupportedNetworkTypes {#GetSupportedNetworkTypes}

<p>Returns the types of networks supported by this interface.</p>

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
                <code><a class='link' href='#Device_GetSupportedNetworkTypes_Result'>Device_GetSupportedNetworkTypes_Result</a></code>
            </td>
        </tr></table>

### GetSupportedChannels {#GetSupportedChannels}

<p>Returns a vector of information about the
channels supported by this interface.</p>
<p>If the returned array is empty, this interface does not
support additional channel information.</p>

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
                <code><a class='link' href='#Device_GetSupportedChannels_Result'>Device_GetSupportedChannels_Result</a></code>
            </td>
        </tr></table>

### RegisterObserver {#RegisterObserver}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>observer</code></td>
            <td>
                <code><a class='link' href='#DeviceObserver'>DeviceObserver</a></code>
            </td>
        </tr></table>



## DeviceObserver {#DeviceObserver}
*Defined in [fuchsia.lowpan/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/device.fidl#79)*


### OnStateChanged {#OnStateChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='#State'>State</a></code>
            </td>
        </tr></table>



### OnRoleChanged {#OnRoleChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='#Role'>Role</a></code>
            </td>
        </tr></table>



### OnEnabledChanged {#OnEnabledChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>is_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnProvisionedChanged {#OnProvisionedChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>is_provisioned</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## DeviceExtra {#DeviceExtra}
*Defined in [fuchsia.lowpan/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/device.fidl#89)*


### Form {#Form}

<p>Forms a new network with the given network
information optional credential. Unspecified
fields in the network information will be
filled in with reasonable values. If the network
credential is unspecified, one will be generated
automatically.</p>
<p>Upon success, the interface will be up and
attached to the newly formed network.</p>
<p>This method returns immediately. You can be
notified when this process is complete by
adding a listener and handling the following:</p>
<ul>
<li><code>Listener::OnProvisionException</code>, which is called
to report errors.</li>
<li><code>Listener::OnStateChanged</code>, which will transition
to <code>State::ATTACHED</code> upon success.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#ProvisioningParams'>ProvisioningParams</a></code>
            </td>
        </tr><tr>
            <td><code>progress</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ProvisioningProgress'>ProvisioningProgress</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#DeviceExtra_Form_Result'>DeviceExtra_Form_Result</a></code>
            </td>
        </tr></table>

### Join {#Join}

<p>Attempts to join a pre-existing nearby network
with the given provisioning parameters.</p>
<p>Upon success, the interface will be up and
attached to the newly joined network.</p>
<p>This method returns immediately. You can be
notified when this process is complete by
adding a callback and handling the following:</p>
<ul>
<li><code>Listener::OnProvisionException</code>, which is called
to report errors.</li>
<li><code>Listener::OnStateChanged</code>, which will transition
to <code>State::ATTACHED</code> upon success.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>params</code></td>
            <td>
                <code><a class='link' href='#ProvisioningParams'>ProvisioningParams</a></code>
            </td>
        </tr><tr>
            <td><code>progress</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ProvisioningProgress'>ProvisioningProgress</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#DeviceExtra_Join_Result'>DeviceExtra_Join_Result</a></code>
            </td>
        </tr></table>

### GetCredential {#GetCredential}

<p>Fetches the current credential, if any.</p>

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
                <code><a class='link' href='#DeviceExtra_GetCredential_Result'>DeviceExtra_GetCredential_Result</a></code>
            </td>
        </tr></table>

### CreateNetworkScanner {#CreateNetworkScanner}

<p>Sets up a new <code>NetworkScanner</code> for this interface, which
is used to scan for nearby networks.</p>
<p>This will expose coarse location information.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scanner</code></td>
            <td>
                <code>request&lt;<a class='link' href='#NetworkScanner'>NetworkScanner</a>&gt;</code>
            </td>
        </tr></table>



### CreateEnergyScanner {#CreateEnergyScanner}

<p>Sets up a new <code>EnergyScanner</code> for this interface, which
is used to coarsely determine which channels might be
appropriate to use.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scanner</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EnergyScanner'>EnergyScanner</a>&gt;</code>
            </td>
        </tr></table>



### RegisterObserver {#RegisterObserver}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>observer</code></td>
            <td>
                <code><a class='link' href='#DeviceExtraObserver'>DeviceExtraObserver</a></code>
            </td>
        </tr></table>



## DeviceExtraObserver {#DeviceExtraObserver}
*Defined in [fuchsia.lowpan/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/device.fidl#150)*


### OnIdentityChanged {#OnIdentityChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identity</code></td>
            <td>
                <code><a class='link' href='#Identity'>Identity</a></code>
            </td>
        </tr></table>

## EnergyScanResultStream {#EnergyScanResultStream}
*Defined in [fuchsia.lowpan/energy_scanner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/energy_scanner.fidl#7)*


### Next {#Next}

<p>Called to fetch the next set of energy scan results.</p>
<p>The last set will have zero items. Once results for all
indicated channels have been returned, this channel will close.</p>

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
                <code><a class='link' href='#EnergyScanResultStream_Next_Result'>EnergyScanResultStream_Next_Result</a></code>
            </td>
        </tr></table>

## EnergyScanner {#EnergyScanner}
*Defined in [fuchsia.lowpan/energy_scanner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/energy_scanner.fidl#15)*


### SetChannels {#SetChannels}

<p>Sets which channels will be used for scanning.</p>
<p>If empty, all available channels will be scanned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel_indexes</code></td>
            <td>
                <code>vector&lt;uint16&gt;[100]</code>
            </td>
        </tr></table>



### GetChannels {#GetChannels}

<p>Gets the list of channels that will be scanned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel_indexes</code></td>
            <td>
                <code>vector&lt;uint16&gt;[100]</code>
            </td>
        </tr></table>

### SetChannelDuration {#SetChannelDuration}

<p>Changes the approximate dwell time per-channel for the
energy scan, measured in milliseconds.</p>
<p>Note that this duration is approximate and may
differ significantly. In some cases setting this
duration may not be supported, in which case the value
is ignored.</p>
<p>Setting a value outside of the supported range of
values for this device will result in the value being
clamped to the closest valid value, so setting a value of zero
would request the smallest energy scan duration the device
is capable of.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ms</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### StartScan {#StartScan}

<p>Starts a energy scan operation.</p>
<p>If this method is called while a scan is in progress,
the error <code>INTERFACE_BUSY</code> will be returned by the
first call to <code>stream.Next()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='#EnergyScanResultStream'>EnergyScanResultStream</a>&gt;</code>
            </td>
        </tr></table>



## BeaconInfoStream {#BeaconInfoStream}
*Defined in [fuchsia.lowpan/network_scanner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/network_scanner.fidl#7)*


### Next {#Next}

<p>Called to fetch the next set of received beacons.</p>
<p>The last set will have zero items. Once all received
beacons have been returned, this channel will close.</p>

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
                <code><a class='link' href='#BeaconInfoStream_Next_Result'>BeaconInfoStream_Next_Result</a></code>
            </td>
        </tr></table>

## NetworkScanner {#NetworkScanner}
*Defined in [fuchsia.lowpan/network_scanner.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/network_scanner.fidl#16)*

<p>Protocol for performing active network scans.</p>

### SetChannels {#SetChannels}

<p>Sets which channels will be used for scanning.</p>
<p>If empty, all available channels will be scanned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel_indexes</code></td>
            <td>
                <code>vector&lt;uint16&gt;[100]</code>
            </td>
        </tr></table>



### GetChannels {#GetChannels}

<p>Gets the list of channels that will be scanned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>channel_indexes</code></td>
            <td>
                <code>vector&lt;uint16&gt;[100]</code>
            </td>
        </tr></table>

### SetTxPower {#SetTxPower}

<p>Changes the transmit power (in dBm) to the
antenna for transmitting beacon requests.</p>
<p>Note that the actual transmit
power may differ in a way that is less than
the amount specified. Call <code>GetTxPower</code> to get
the actual transmit power.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>power</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### GetTxPower {#GetTxPower}

<p>Gets the transmit power (in dBm) that will be
used for transmitting beacon requests.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>tx_power</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### StartScan {#StartScan}

<p>Starts a network scan operation.</p>
<p>If this method is called while a scan is in progress,
the error <code>INTERFACE_BUSY</code> will be returned by the
first call to <code>stream.Next()</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BeaconInfoStream'>BeaconInfoStream</a>&gt;</code>
            </td>
        </tr></table>



## ProvisioningProgress {#ProvisioningProgress}
*Defined in [fuchsia.lowpan/provisioning_progress.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/provisioning_progress.fidl#7)*


### OnError {#OnError}

<p>Reports an error durring provisioning</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#ProvisionError'>ProvisionError</a></code>
            </td>
        </tr></table>

### OnSuccess {#OnSuccess}

<p>Indicates the success of the provisioning process.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>identity</code></td>
            <td>
                <code><a class='link' href='#Identity'>Identity</a></code>
            </td>
        </tr></table>

## LowpanLookup {#LowpanLookup}
*Defined in [fuchsia.lowpan/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/service.fidl#42)*


### Lookup {#Lookup}

<p>Looks up the LoWPAN device with the given interface name,
or the last device registered if no interface name is given.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]?</code>
            </td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Device'>Device</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#LowpanLookup_Lookup_Result'>LowpanLookup_Lookup_Result</a></code>
            </td>
        </tr></table>

### GetDevices {#GetDevices}

<p>Returns the list of all registered LoWPAN device interface names.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_names</code></td>
            <td>
                <code>vector&lt;string&gt;[8]</code>
            </td>
        </tr></table>

### OnDeviceAdded {#OnDeviceAdded}

<p>Called when a new LoWPAN device has been registered.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr></table>

### OnDeviceRemoved {#OnDeviceRemoved}

<p>Called when an existing LoWPAN device has been removed.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr></table>

## LowpanRegistry {#LowpanRegistry}
*Defined in [fuchsia.lowpan/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/service.fidl#58)*


### Register {#Register}

<p>Registers the given LoWPAN device with the LoWPAN Service
using the given interface name. If no interface name is given,
then the registry will pick one. The actual interface name
for the device is returned.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]?</code>
            </td>
        </tr><tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#Device'>Device</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#LowpanRegistry_Register_Result'>LowpanRegistry_Register_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### BeaconInfo {#BeaconInfo}
*Defined in [fuchsia.lowpan/beacon_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/beacon_info.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identity</code></td>
            <td>
                <code><a class='link' href='#Identity'>Identity</a></code>
            </td>
            <td><p>The identity of the network being advertised by
this beacon.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rssi</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>RSSI of the beacon, measured in dBm.
If unspecified, set to -128 (<code>RSSI_UNSPECIFIED</code>).</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>lqi</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td><p>Link Quality Index (LQI) of the beacon.</p>
<ul>
<li>A value of 0 (<code>LQI_UNSPECIFIED</code>) indicates that the LQI
was not set.</li>
<li>A value of 1 indicates the worst possible
quality where the decoded beacon is still valid.</li>
<li>A value of 255 indicates the best possible
quality that can be recognized by the radio
hardware.</li>
<li>Values 2-254 are intended to represent relative
quality levels evenly distributed between the
worst and best, with lower values always
indicating a worse quality than higher values.</li>
</ul>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>address</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16]</code>
            </td>
            <td><p>The MAC address associated with this beacon.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>vector&lt;int32&gt;[32]</code>
            </td>
            <td><p>A collection of integers representing any
flags associated with this beacon, like
<code>BEACON_INFO_FLAG_CAN_ASSIST</code>.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ChannelInfo {#ChannelInfo}
*Defined in [fuchsia.lowpan/channel_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/channel_info.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>string[16]</code>
            </td>
            <td><p>Human-readable identifier for channel.</p>
<p>For most network types, this is just
the string representation of the index.
However, some network types might have
non-integer ways of identifying specific
channels. This field allows the application
to display the name of the channel correctly
under such circumstances.</p>
<p>The allowed characters include:</p>
<ul>
<li>Dash (<code>-</code>), Underscore (<code>_</code>), Plus(<code>+</code>), Semicolon(<code>:</code>)</li>
<li>Numbers (<code>0</code>-<code>9</code>)</li>
<li>Letters (<code>a</code>-<code>z</code>, <code>A</code>-<code>Z</code>)</li>
</ul>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>index</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The index used by the interface to identify
this channel.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_transmit_power</code></td>
            <td>
                <code>int32</code>
            </td>
            <td><p>The maximum transmit power allowed on
this channel, in dBm.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>spectrum_center_frequency</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The center RF frequency of this channel, in Hz.</p>
<p>For example, 802.15.4 has the following values:</p>
<p>Channel | Center Frequency (Hz)
--------|----------------------
11      | 2,405,000,000
12      | 2,410,000,000
13      | 2,415,000,000
14      | 2,420,000,000
15      | 2,425,000,000
16      | 2,430,000,000
17      | 2,435,000,000
18      | 2,440,000,000
19      | 2,445,000,000
20      | 2,450,000,000
21      | 2,455,000,000
22      | 2,460,000,000
23      | 2,465,000,000
24      | 2,470,000,000
25      | 2,475,000,000
26      | 2,480,000,000</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>spectrum_bandwidth</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>The RF spectrum bandwidth used by this
channel where the power level is expected to
be higher than -20dBr, in Hz.</p>
<p>For example, 802.15.4 channels 11 thru 26 would
have the value 2,000,000 (2 MHz).</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>masked_by_regulatory_domain</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Indicates if this channel is masked by the
current regulatory domain and is thus unable
to be used.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### Device_Provision_Response {#Device_Provision_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Device_GetSupportedNetworkTypes_Response {#Device_GetSupportedNetworkTypes_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>network_types</code></td>
            <td>
                <code>vector&lt;string&gt;[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Device_GetSupportedChannels_Response {#Device_GetSupportedChannels_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>channels_info</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ChannelInfo'>ChannelInfo</a>&gt;[100]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceExtra_Form_Response {#DeviceExtra_Form_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### DeviceExtra_Join_Response {#DeviceExtra_Join_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### DeviceExtra_GetCredential_Response {#DeviceExtra_GetCredential_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>predential</code></td>
            <td>
                <code><a class='link' href='#Credential'>Credential</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EnergyScanResult {#EnergyScanResult}
*Defined in [fuchsia.lowpan/energy_scan_result.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/energy_scan_result.fidl#8)*



<p>Describes the result from one channel of an energy scan.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>channel_index</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_rssi</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_rssi</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EnergyScanResultStream_Next_Response {#EnergyScanResultStream_Next_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>results</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EnergyScanResult'>EnergyScanResult</a>&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BeaconInfoStream_Next_Response {#BeaconInfoStream_Next_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>beacons</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#BeaconInfo'>BeaconInfo</a>&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ProvisioningParams {#ProvisioningParams}
*Defined in [fuchsia.lowpan/provisioning_params.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/provisioning_params.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>identity</code></td>
            <td>
                <code><a class='link' href='#Identity'>Identity</a></code>
            </td>
            <td><p>The identity of the network.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>credential</code></td>
            <td>
                <code><a class='link' href='#Credential'>Credential</a>?</code>
            </td>
            <td><p>The credential used to authenticate to
the network.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### LowpanLookup_Lookup_Response {#LowpanLookup_Lookup_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### LowpanRegistry_Register_Response {#LowpanRegistry_Register_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {#Error}
Type: <code>int32</code>

*Defined in [fuchsia.lowpan/error.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/error.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED</code></td>
            <td><code>1</code></td>
            <td><p>An unspecified error has occurred. This error type should be
avoided unless the use of a more specific error would be misleading.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ARGUMENT</code></td>
            <td><code>2</code></td>
            <td><p>One or more of the arguments to the method contained invalid values.</p>
</td>
        </tr><tr>
            <td><code>INTERFACE_DISABLED</code></td>
            <td><code>3</code></td>
            <td><p>The requested operation cannot be completed because the
interface was disabled.</p>
</td>
        </tr><tr>
            <td><code>WRONG_STATE</code></td>
            <td><code>4</code></td>
            <td><p>The requested operation cannot be completed because the
interface was not in the prerequisite state.</p>
</td>
        </tr><tr>
            <td><code>INTERFACE_BUSY</code></td>
            <td><code>9</code></td>
            <td><p>The requested operation cannot be completed because the
interface is busy performing a mutually exclusive operation.
Try again later.</p>
</td>
        </tr></table>

### ProvisionError {#ProvisionError}
Type: <code>int32</code>

*Defined in [fuchsia.lowpan/error.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/error.fidl#29)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED</code></td>
            <td><code>1</code></td>
            <td><p>An unspecified error has occurred. This error type should be
avoided unless the use of a more specific error would be misleading.</p>
</td>
        </tr><tr>
            <td><code>CANCELLED</code></td>
            <td><code>5</code></td>
            <td><p>Provisioning did not successfully complete because the
operation was canceled.</p>
</td>
        </tr><tr>
            <td><code>CREDENTIAL_REJECTED</code></td>
            <td><code>6</code></td>
            <td><p>Provisioning did not successfully complete because the
credential was rejected. For example, the key was incorrect.</p>
</td>
        </tr><tr>
            <td><code>NETWORK_NOT_FOUND</code></td>
            <td><code>7</code></td>
            <td><p>Provisioning did not successfully complete because the
no peers on the requested network are in range.</p>
</td>
        </tr><tr>
            <td><code>NETWORK_ALREADY_EXISTS</code></td>
            <td><code>8</code></td>
            <td><p>Forming a new network did not successfully complete because the
a peer with the requested network identity is in range.</p>
</td>
        </tr></table>

### Role {#Role}
Type: <code>int32</code>

*Defined in [fuchsia.lowpan/role.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/role.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DETACHED</code></td>
            <td><code>1</code></td>
            <td><p>Detached role. The interface is not
currently participating on the network,
either because it cannot find a parent</p>
</td>
        </tr><tr>
            <td><code>END_DEVICE</code></td>
            <td><code>2</code></td>
            <td><p>End-device role. End devices do not route
traffic on behalf of other nodes.</p>
</td>
        </tr><tr>
            <td><code>ROUTER</code></td>
            <td><code>3</code></td>
            <td><p>Router role. Routers help route traffic
around the mesh network.</p>
<p>Note that this role is independent of the
device being a &quot;border router&quot;.</p>
<p>Not all network types support this role.</p>
</td>
        </tr><tr>
            <td><code>SLEEPY_END_DEVICE</code></td>
            <td><code>4</code></td>
            <td><p>Sleepy End-Device role.</p>
<p>End devices with this role are nominally asleep,
waking up periodically to check in with their
parent to see if there are packets destined for
them. Such devices are capable of extraordinarily
low power consumption, but packet latency can be
on the order of dozens of seconds(depending on how
the node is configured). Not all network types
support this role.</p>
<p>Not all network types support this role.</p>
</td>
        </tr><tr>
            <td><code>SLEEPY_ROUTER</code></td>
            <td><code>5</code></td>
            <td><p>Sleepy-router role.</p>
<p>Routers with this role are nominally asleep,
waking up periodically to check in with
other routers and their children.</p>
<p>Not all network types support this role.</p>
</td>
        </tr><tr>
            <td><code>LEADER</code></td>
            <td><code>6</code></td>
            <td><p>Leader role.</p>
<p>On Thread networks, for each partition/fragment
one router is designated as the &quot;leader&quot;, which
means that it is considered authoritative for
all network data. In most cases this role can be
considered as a synonym to Role::ROUTER.</p>
<p>Not all network types support this role.</p>
</td>
        </tr><tr>
            <td><code>COORDINATOR</code></td>
            <td><code>7</code></td>
            <td><p>Coordinator role.</p>
<p>Not all network types support this role.</p>
</td>
        </tr></table>

### ServiceError {#ServiceError}
Type: <code>int32</code>

*Defined in [fuchsia.lowpan/service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/service.fidl#11)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INTERNAL_SERVICE_ERROR</code></td>
            <td><code>1</code></td>
            <td><p>An unspecified internal error in the LoWPAN service has occurred.</p>
<p>This error almost always indicates a software bug of some sort.</p>
</td>
        </tr><tr>
            <td><code>INVALID_ARGUMENT</code></td>
            <td><code>2</code></td>
            <td><p>One of the arguments to this method was invalid.</p>
<p>This error is only returned if none of the other
error codes would be a better description.</p>
</td>
        </tr><tr>
            <td><code>DEVICE_NOT_FOUND</code></td>
            <td><code>3</code></td>
            <td><p>A device with this interface name has not been registered.</p>
</td>
        </tr><tr>
            <td><code>DEVICE_ALREADY_EXISTS</code></td>
            <td><code>4</code></td>
            <td><p>A device with this interface name has already been registered.</p>
</td>
        </tr><tr>
            <td><code>INVALID_INTERFACE_NAME</code></td>
            <td><code>5</code></td>
            <td><p>The given interface name was invalid.</p>
<p>This could be due to any of the following reasons:</p>
<ul>
<li>The interface name was too short. (&lt;= 2 characters)</li>
<li>The interface name was too long. (&gt; 32 characters)</li>
<li>The interface name contained invalid characters.</li>
</ul>
<p>Interface name regex: <code>^[a-z_][-_.+0-9a-z]{1,31}$</code></p>
</td>
        </tr></table>

### State {#State}
Type: <code>int32</code>

*Defined in [fuchsia.lowpan/state.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/state.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OFFLINE</code></td>
            <td><code>1</code></td>
            <td><p>Offline state.</p>
<p>This is the initial state of the LoWPAN
interface when the underlying driver starts.
In this state the NCP is idle and not
connected to any network.</p>
<p>This state can be explicitly entered by
calling <code>Reset</code>, <code>Leave</code>, or <code>setUp(false)</code>,
with the later two only working if we were not
previously in <code>State::FAULT</code>.</p>
</td>
        </tr><tr>
            <td><code>ATTACHING</code></td>
            <td><code>2</code></td>
            <td><p>Attaching state.</p>
<p>The interface enters this state when it starts
the process of trying to find other nodes so
that it can attach to any pre-existing network
fragment, or when it is in the process of
calculating the optimal values for unspecified
parameters when forming a new network.</p>
<p>The interface may stay in this state for a
prolonged period of time (or may spontaneously
enter this state from <code>State::ATTACHED</code> if the
underlying network technology is hierarchical
(like ZigBee IP) or if the device role is that
of an &quot;end-device&quot; (<code>Role::END_DEVICE</code>). This
is because such roles cannot create their own
network fragments.</p>
</td>
        </tr><tr>
            <td><code>ATTACHED</code></td>
            <td><code>3</code></td>
            <td><p>Attached state.</p>
<p>This state indicates that we are an active
participant on a network that has at least one
other peer node in range.</p>
<p>The Interface can enter this state from
<code>State::ATTACHING</code>.</p>
</td>
        </tr><tr>
            <td><code>ISOLATED</code></td>
            <td><code>4</code></td>
            <td><p>Isolated state.</p>
<p>This state indicates that there are no nearby
nodes for the provisioned network in range.
Once other nodes come into range, the
interface will automatically switch to
<code>State::ATTACHED</code>.</p>
<p>The interface can enter this state from either
<code>State::ATTACHING</code> or <code>State::ATTACHED</code>.</p>
</td>
        </tr><tr>
            <td><code>FAULT</code></td>
            <td><code>5</code></td>
            <td><p>Fault state.</p>
<p>The interface will enter this state when
the driver has detected some sort of problem
from which it was not immediately able to
recover.</p>
<p>This state can be entered spontaneously from
any other state. Calling <code>Reset</code> will cause
the device to return to <code>State::OFFLINE</code>.</p>
</td>
        </tr><tr>
            <td><code>COMMISSIONING</code></td>
            <td><code>6</code></td>
            <td><p>Commissioning state.</p>
<p>The interface enters this state after a call
to <code>startCommissioningSession(LowpanBeaconInfo)</code>.
This state may only be entered directly from
<code>State::OFFLINE</code>.</p>
</td>
        </tr></table>



## **TABLES**

### Identity {#Identity}


*Defined in [fuchsia.lowpan/identity.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/identity.fidl#7)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>raw_name</code></td>
            <td>
                <code>vector&lt;uint8&gt;[63]</code>
            </td>
            <td><p>The raw bytes for the network name.
This is typically a <a href="https://tools.ietf.org/html/rfc3454">StringPrep'd</a> UTF8 encoding.</p>
<p>Note that extra care must be taken when displaying
this value to users, since there are many ways
to make visually similar UTF8 strings that
have differing bytecode representations.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>xpanid</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8]</code>
            </td>
            <td><p>Extended PANID.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>net_type</code></td>
            <td>
                <code>string[64]</code>
            </td>
            <td><p>String identifying the type of network.</p>
<p>Well-known protocol ids are associated with
specific string values (like &quot;org.threadgroup.std.thread&quot;
or &quot;org.zigbee.std.zigbee-ip&quot;). For unknown protocol ids,
the string will map to something like
<code>fuchsia.lowpan.net_type.802.15.4.pid.XX</code>, where <code>XX</code> is
the value of the protocol id from a 802.14.5 beacon.
This field is optional when joining, forming, or provisioning.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>channel</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>Channel Index.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>panid</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>PANID for 802.14.5-based networks (or the equivalent).</p>
</td>
        </tr></table>



## **UNIONS**

### Device_Provision_Result {#Device_Provision_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_Provision_Response'>Device_Provision_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Device_GetSupportedNetworkTypes_Result {#Device_GetSupportedNetworkTypes_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_GetSupportedNetworkTypes_Response'>Device_GetSupportedNetworkTypes_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Device_GetSupportedChannels_Result {#Device_GetSupportedChannels_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Device_GetSupportedChannels_Response'>Device_GetSupportedChannels_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### DeviceExtra_Form_Result {#DeviceExtra_Form_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DeviceExtra_Form_Response'>DeviceExtra_Form_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### DeviceExtra_Join_Result {#DeviceExtra_Join_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DeviceExtra_Join_Response'>DeviceExtra_Join_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### DeviceExtra_GetCredential_Result {#DeviceExtra_GetCredential_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DeviceExtra_GetCredential_Response'>DeviceExtra_GetCredential_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### EnergyScanResultStream_Next_Result {#EnergyScanResultStream_Next_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#EnergyScanResultStream_Next_Response'>EnergyScanResultStream_Next_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### BeaconInfoStream_Next_Result {#BeaconInfoStream_Next_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#BeaconInfoStream_Next_Response'>BeaconInfoStream_Next_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### LowpanLookup_Lookup_Result {#LowpanLookup_Lookup_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#LowpanLookup_Lookup_Response'>LowpanLookup_Lookup_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ServiceError'>ServiceError</a></code>
            </td>
            <td></td>
        </tr></table>

### LowpanRegistry_Register_Result {#LowpanRegistry_Register_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#LowpanRegistry_Register_Response'>LowpanRegistry_Register_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ServiceError'>ServiceError</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### Credential {#Credential}
*Defined in [fuchsia.lowpan/credential.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/credential.fidl#14)*

<p>Describes a LoWPAN credential.</p>
<p>Currently only supports a symmetric master key,
but may be extended in the future to support other
types of credentials, such as passwords, PAKE
secrets, or a reference to a certificate/private-key
pair.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>master_key</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td><p>Describes a symmetric key credential.</p>
<p>The size of the symmetric key is defined by the
underlying network technology. For Thread this
is a 16-byte value.</p>
<p>Note that this value is not a password.</p>
</td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/beacon_info.fidl#7">BEACON_INFO_FLAG_CAN_ASSIST</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#7">LQI_UNSPECIFIED</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#8">RSSI_UNSPECIFIED</a></td>
            <td>
                    <code>-128</code>
                </td>
                <td><code>int8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#9">CHANNEL_UNSPECIFIED</a></td>
            <td>
                    <code>65535</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#11">MAX_CHANNELS</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#12">MAX_NET_TYPE_LEN</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#13">MAX_STREAM_SET_SIZE</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#15">NET_TYPE_THREAD_1_X</a></td>
            <td><code>org.threadgroup.std.thread.1</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#16">NET_TYPE_ZIGBEE_IP_1_X</a></td>
            <td><code>org.zigbee.std.zigbee-ip.1</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#17">NET_TYPE_UNKNOWN_802_15_4_PID</a></td>
            <td><code>fuchsia.lowpan.net_type.802.15.4.pid</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/const.fidl#18">NET_TYPE_RAW_6LOWPAN</a></td>
            <td><code>fuchsia.lowpan.net_type.6lowpan</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/service.fidl#9">MAX_LOWPAN_DEVICES</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    
</table>



## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.lowpan/service.fidl#7">interface_name</a></td>
            <td>
                <code>string</code></td>
            <td></td>
        </tr></table>

