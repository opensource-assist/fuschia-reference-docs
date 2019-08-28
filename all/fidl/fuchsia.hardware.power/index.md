Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.power


## **PROTOCOLS**

## Source {:#Source}
*Defined in [fuchsia.hardware.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#59)*


### GetPowerInfo {:#GetPowerInfo}


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
                <code><a class='link' href='#SourceInfo'>SourceInfo</a></code>
            </td>
        </tr></table>

### GetStateChangeEvent {:#GetStateChangeEvent}


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
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>

### GetBatteryInfo {:#GetBatteryInfo}


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
                <code><a class='link' href='#BatteryInfo'>BatteryInfo</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### SourceInfo {:#SourceInfo}
*Defined in [fuchsia.hardware.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#PowerType'>PowerType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BatteryInfo {:#BatteryInfo}
*Defined in [fuchsia.hardware.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>unit</code></td>
            <td>
                <code><a class='link' href='#BatteryUnit'>BatteryUnit</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>design_capacity</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>last_full_capacity</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>design_voltage</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>capacity_warning</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>capacity_low</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>capacity_granularity_low_warning</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>capacity_granularity_warning_full</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>present_rate</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>remaining_capacity</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>present_voltage</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### PowerType {:#PowerType}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#8)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>AC</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BATTERY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### BatteryUnit {:#BatteryUnit}
Type: <code>uint32</code>

*Defined in [fuchsia.hardware.power/power.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#23)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>MW</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>MA</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#13">POWER_STATE_ONLINE</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#14">POWER_STATE_DISCHARGING</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#15">POWER_STATE_CHARGING</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power/power.fidl#16">POWER_STATE_CRITICAL</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    
</table>

