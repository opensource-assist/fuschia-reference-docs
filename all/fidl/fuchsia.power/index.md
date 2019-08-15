Project: /_project.yaml
Book: /_book.yaml

# fuchsia.power


## **PROTOCOLS**

## BatteryInfoProvider {:#BatteryInfoProvider}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#101)*

 Provider interface used to obtain battery status details

### GetBatteryInfo {:#GetBatteryInfo}

 Gets battery info

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

### Watch {:#Watch}

 Registers a watcher for battery info changes

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#BatteryInfoWatcher'>BatteryInfoWatcher</a></code>
            </td>
        </tr></table>



## BatteryInfoWatcher {:#BatteryInfoWatcher}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#110)*

 Watcher on battery info

### OnChangeBatteryInfo {:#OnChangeBatteryInfo}

 Callback triggered when battery info changes

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

## BatteryManager {:#BatteryManager}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#117)*

 General manager interface for battery management

### GetBatteryInfo {:#GetBatteryInfo}

 Gets battery info

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

### Watch {:#Watch}

 Registers a watcher for battery info changes

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

### BatteryStatus {:#BatteryStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#10)*

 The overall status of the battery, informing its general availability.


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
            <td><code>NOT_AVAILABLE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_PRESENT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### ChargeStatus {:#ChargeStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#22)*

 The status of the battery with respect to charging.


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

### ChargeSource {:#ChargeSource}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#31)*

 The power source for an actively charging battery.


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

### LevelStatus {:#LevelStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#40)*

 The general status of the battery level.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>WARNING</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOW</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CRITICAL</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### HealthStatus {:#HealthStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#48)*

 The general status related to the overall health of the battery.


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

### BatteryInfo {:#BatteryInfo}


*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#71)*

 Current battery state information


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#BatteryStatus'>BatteryStatus</a></code>
            </td>
            <td> General battery status with respect to presence & availability
</td>
        </tr><tr>
            <td>2</td>
            <td><code>charge_status</code></td>
            <td>
                <code><a class='link' href='#ChargeStatus'>ChargeStatus</a></code>
            </td>
            <td> The current state of the battery with respect to charging
</td>
        </tr><tr>
            <td>3</td>
            <td><code>charge_source</code></td>
            <td>
                <code><a class='link' href='#ChargeSource'>ChargeSource</a></code>
            </td>
            <td> The charge source while battery is actively charging.
 When not actively charging, this will reflect that the source is
 NONE (not charging) or UNKNOWN.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>level_percent</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Battery level in percentage
</td>
        </tr><tr>
            <td>5</td>
            <td><code>level_status</code></td>
            <td>
                <code><a class='link' href='#LevelStatus'>LevelStatus</a></code>
            </td>
            <td> Battery level as a general status, including low and critical
</td>
        </tr><tr>
            <td>6</td>
            <td><code>health</code></td>
            <td>
                <code><a class='link' href='#HealthStatus'>HealthStatus</a></code>
            </td>
            <td> Overall battery health
</td>
        </tr><tr>
            <td>7</td>
            <td><code>time_remaining</code></td>
            <td>
                <code><a class='link' href='#TimeRemaining'>TimeRemaining</a></code>
            </td>
            <td> Time remaining relative to the current charge status
</td>
        </tr><tr>
            <td>8</td>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Timestamp to distinguish between latest and stale status
</td>
        </tr></table>





## **XUNIONS**

### TimeRemaining {:#TimeRemaining}
*Defined in [fuchsia.power/battery.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/battery.fidl#59)*

 The time remaining while actively charging or discharging.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>indeterminate</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Representation of indeterminate state with zero duration.
</td>
        </tr><tr>
            <td><code>battery_life</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Remaining battery life while discharging
</td>
        </tr><tr>
            <td><code>full_charge</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Remaining time until full while charging
</td>
        </tr></table>





