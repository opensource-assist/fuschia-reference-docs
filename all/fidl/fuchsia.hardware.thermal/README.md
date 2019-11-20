[TOC]

# fuchsia.hardware.thermal


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.hardware.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#98)*


### GetInfo {#GetInfo}

<p>Get information about the device's current state.</p>

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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ThermalInfo'>ThermalInfo</a>?</code>
            </td>
        </tr></table>

### GetDeviceInfo {#GetDeviceInfo}

<p>Get information about the device's thermal capabilities and trip points.</p>

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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ThermalDeviceInfo'>ThermalDeviceInfo</a>?</code>
            </td>
        </tr></table>

### GetDvfsInfo {#GetDvfsInfo}

<p>Get the device's operating points.
TODO(bradenkell): Can this be removed? GetDeviceInfo() provides the same information.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>power_domain</code></td>
            <td>
                <code><a class='link' href='#PowerDomain'>PowerDomain</a></code>
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
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#OperatingPoint'>OperatingPoint</a>?</code>
            </td>
        </tr></table>

### GetTemperatureCelsius {#GetTemperatureCelsius}

<p>Get the current temperature in degrees Celsius.</p>

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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>temp</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### GetStateChangeEvent {#GetStateChangeEvent}

<p>Get an event to get trip point notifications on. <code>ZX_USER_SIGNAL_</code>0 is changed when either
trip point is reached. It is deasserted when the state is read via GetInfo.</p>

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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;event&gt;?</code>
            </td>
        </tr></table>

### GetStateChangePort {#GetStateChangePort}

<p>Get a port to get trip point notification packets.</p>

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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>handle</code></td>
            <td>
                <code>handle&lt;port&gt;?</code>
            </td>
        </tr></table>

### SetTripCelsius {#SetTripCelsius}

<p>Sets a trip point in degrees Celsius. When the sensor reaches the trip point temperature the
device will notify on an event.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>temp</code></td>
            <td>
                <code>float32</code>
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

### GetDvfsOperatingPoint {#GetDvfsOperatingPoint}

<p>Get the current operating point index.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>power_domain</code></td>
            <td>
                <code><a class='link' href='#PowerDomain'>PowerDomain</a></code>
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
        </tr><tr>
            <td><code>op_idx</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>

### SetDvfsOperatingPoint {#SetDvfsOperatingPoint}

<p>Set the operating point index.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>op_idx</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr><tr>
            <td><code>power_domain</code></td>
            <td>
                <code><a class='link' href='#PowerDomain'>PowerDomain</a></code>
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

### GetFanLevel {#GetFanLevel}

<p>Get the current fan level.</p>

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
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>fan_level</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetFanLevel {#SetFanLevel}

<p>Set the fan level.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fan_level</code></td>
            <td>
                <code>uint32</code>
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



## **STRUCTS**

### OperatingPoint {#OperatingPoint}
*Defined in [fuchsia.hardware.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#31)*



<p>scpi_opp_t is typedef'd to this.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>opp</code></td>
            <td>
                <code>[16]</code>
            </td>
            <td><p>The device's operating points.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>latency</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>In microseconds.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The number of operating points in opp.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### OperatingPointEntry {#OperatingPointEntry}
*Defined in [fuchsia.hardware.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#41)*



<p>scpi_opp_entry_t is typedef'd to this.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>freq_hz</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The operating point frequency in Hz.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>volt_uv</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The operating point voltage in microvolts.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ThermalInfo {#ThermalInfo}
*Defined in [fuchsia.hardware.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#49)*



<p>Temperature units are degrees Celsius.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>State is a bitmask of <code>THERMAL_STATE_</code>* values.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>passive_temp_celsius</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The sensor temperature at which the system should activate passive cooling policy.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>critical_temp_celsius</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The sensor temperature at which the system should perform critical shutdown.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_trip_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The number of trip points supported.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>active_trip</code></td>
            <td>
                <code>float32[16]</code>
            </td>
            <td><p>The currently active trip point.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ThermalTemperatureInfo {#ThermalTemperatureInfo}
*Defined in [fuchsia.hardware.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#63)*



<p>Temperature units are degrees Celsius.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>up_temp_celsius</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The temperature must rise to up_temp to get to this trip point.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>down_temp_celsius</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The temperature must fall to down_temp to get to this trip point.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>fan_level</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The fan level for this trip point.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>big_cluster_dvfs_opp</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The operating point index of the big cluster.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>little_cluster_dvfs_opp</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td><p>The operating point index of the little cluster.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>gpu_clk_freq_source</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The GPU clock source index.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ThermalDeviceInfo {#ThermalDeviceInfo}
*Defined in [fuchsia.hardware.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#78)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>active_cooling</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Active cooling support.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>passive_cooling</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Passive cooling support.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>gpu_throttling</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>GPU throttling support.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>num_trip_points</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Number of trip points.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>big_little</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Big-little architecture.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>critical_temp_celsius</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>Critical temperature in degrees Celsius.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>trip_point_info</code></td>
            <td>
                <code>[16]</code>
            </td>
            <td><p>Trip point information.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>opps</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td><p>Operating point information.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PowerDomain {#PowerDomain}
Type: <code>uint32</code>

*Defined in [fuchsia.hardware.thermal/thermal.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#25)*

<p>Devices with big-little architecture may have different operating points for each cluster.
Other devices use <code>BIG_CLUSTER_POWER_DOMAIN</code> for getting/setting the operating point.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BIG_CLUSTER_POWER_DOMAIN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LITTLE_CLUSTER_POWER_DOMAIN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#10">MAX_TRIP_POINTS</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of trip points that can be used.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#14">MAX_DVFS_DOMAINS</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of DVFS domains a device can support (one for each cluster in a big-little
architecture).</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#17">MAX_DVFS_OPPS</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>The maximum number of operating points that can be used.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#20">THERMAL_STATE_NORMAL</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Bitmask values for ThermalInfo.state.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-thermal/thermal.fidl#21">THERMAL_STATE_TRIP_VIOLATION</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

