[TOC]

# fuchsia.power


## **PROTOCOLS**

## BatteryInfoProvider {#BatteryInfoProvider}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#103)*

<p>Provider interface used to obtain battery status details</p>

### GetBatteryInfo {#GetBatteryInfo}

<p>Gets battery info</p>

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
                <code><a class='link' href='#BatteryInfo'>BatteryInfo</a></code>
            </td>
        </tr></table>

### Watch {#Watch}

<p>Registers a watcher for battery info changes</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#BatteryInfoWatcher'>BatteryInfoWatcher</a></code>
            </td>
        </tr></table>



## BatteryInfoWatcher {#BatteryInfoWatcher}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#112)*

<p>Watcher on battery info</p>

### OnChangeBatteryInfo {#OnChangeBatteryInfo}

<p>Callback triggered when battery info changes</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#BatteryInfo'>BatteryInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## BatteryManager {#BatteryManager}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#119)*

<p>General manager interface for battery management</p>

### GetBatteryInfo {#GetBatteryInfo}

<p>Gets battery info</p>

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
                <code><a class='link' href='#BatteryInfo'>BatteryInfo</a></code>
            </td>
        </tr></table>

### Watch {#Watch}

<p>Registers a watcher for battery info changes</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#BatteryInfoWatcher'>BatteryInfoWatcher</a></code>
            </td>
        </tr></table>







## **ENUMS**

### BatteryStatus {#BatteryStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#10)*

<p>The overall status of the battery, informing its general availability.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td><p>uninitialized battery status</p>
</td>
        </tr><tr>
            <td><code>OK</code></td>
            <td><code>1</code></td>
            <td><p>battery present and available</p>
</td>
        </tr><tr>
            <td><code>NOT_AVAILABLE</code></td>
            <td><code>2</code></td>
            <td><p>battery present, but not available (e.g. disabled)</p>
</td>
        </tr><tr>
            <td><code>NOT_PRESENT</code></td>
            <td><code>3</code></td>
            <td><p>battery not present (e.g. removed or no battery)</p>
</td>
        </tr></table>

### ChargeStatus {#ChargeStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#22)*

<p>The status of the battery with respect to charging.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_CHARGING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHARGING</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DISCHARGING</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>FULL</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### ChargeSource {#ChargeSource}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#31)*

<p>The power source for an actively charging battery.</p>


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
            <td><code>AC_ADAPTER</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>USB</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>WIRELESS</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### LevelStatus {#LevelStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#40)*

<p>The general status of the battery level.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>OK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>WARNING</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOW</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>CRITICAL</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### HealthStatus {#HealthStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#49)*

<p>The general status related to the overall health of the battery.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>GOOD</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>COLD</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>HOT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEAD</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>OVER_VOLTAGE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSPECIFIED_FAILURE</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### BatteryInfo {#BatteryInfo}


*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#72)*

<p>Current battery state information</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#BatteryStatus'>BatteryStatus</a></code>
            </td>
            <td><p>General battery status with respect to presence &amp; availability</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>charge_status</code></td>
            <td>
                <code><a class='link' href='#ChargeStatus'>ChargeStatus</a></code>
            </td>
            <td><p>The current state of the battery with respect to charging</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>charge_source</code></td>
            <td>
                <code><a class='link' href='#ChargeSource'>ChargeSource</a></code>
            </td>
            <td><p>The charge source while battery is actively charging.
When not actively charging, this will reflect that the source is
NONE (not charging) or UNKNOWN.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>level_percent</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>Battery level in percentage. Level percent is only available if
level status is known.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>level_status</code></td>
            <td>
                <code><a class='link' href='#LevelStatus'>LevelStatus</a></code>
            </td>
            <td><p>Battery level as a general status, including low and critical</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>health</code></td>
            <td>
                <code><a class='link' href='#HealthStatus'>HealthStatus</a></code>
            </td>
            <td><p>Overall battery health</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>time_remaining</code></td>
            <td>
                <code><a class='link' href='#TimeRemaining'>TimeRemaining</a></code>
            </td>
            <td><p>Time remaining relative to the current charge status</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>timestamp</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#time'>time</a></code>
            </td>
            <td><p>Timestamp to distinguish between latest and stale status</p>
</td>
        </tr></table>





## **XUNIONS**

### TimeRemaining {#TimeRemaining}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#60)*

<p>The time remaining while actively charging or discharging.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>indeterminate</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
            </td>
            <td><p>Representation of indeterminate state with zero duration.</p>
</td>
        </tr><tr>
            <td><code>battery_life</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
            </td>
            <td><p>Remaining battery life while discharging</p>
</td>
        </tr><tr>
            <td><code>full_charge</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
            </td>
            <td><p>Remaining time until full while charging</p>
</td>
        </tr></table>







