Project: /_project.yaml
Book: /_book.yaml

# fuchsia.power


## **PROTOCOLS**

## PowerManager {:#PowerManager}
*Defined in [fuchsia.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/power.fidl#44)*

 Manager Interface used to manage power

### GetBatteryStatus {:#GetBatteryStatus}

 Gets battery status

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
                <code><a class='link' href='../fuchsia.power/index.html#BatteryStatus'>BatteryStatus</a></code>
            </td>
        </tr></table>

### Watch {:#Watch}

 watcher called when battery status changes

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='../fuchsia.power/index.html#PowerManagerWatcher'>PowerManagerWatcher</a></code>
            </td>
        </tr></table>



## PowerManagerWatcher {:#PowerManagerWatcher}
*Defined in [fuchsia.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/power.fidl#53)*

 Watcher on battery status

### OnChangeBatteryStatus {:#OnChangeBatteryStatus}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>battery_status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.power/index.html#BatteryStatus'>BatteryStatus</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### BatteryStatus {:#BatteryStatus}
*Defined in [fuchsia.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/power.fidl#13)*



 Provides battery status


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../fuchsia.power/index.html#Status'>Status</a></code>
            </td>
            <td> Error status
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>batteryPresent</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If battery is present
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>charging</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If battery is charging
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>discharging</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If battery is dis-charging
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>critical</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If battery is at critical level
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>powerAdapterOnline</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If power cable is plugged in
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>timestamp</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> To distinguish between latest and stale status
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>level</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Battery level in percentage
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>remainingBatteryLife</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Remaining Battery life in hours. It is negative when battery is not discharging
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Status {:#Status}
Type: <code>uint32</code>

*Defined in [fuchsia.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.power/power.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NotAvailable</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>











