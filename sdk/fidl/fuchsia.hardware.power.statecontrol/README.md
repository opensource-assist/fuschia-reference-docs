[TOC]

# fuchsia.hardware.power.statecontrol


## **PROTOCOLS**

## Admin {#Admin}
*Defined in [fuchsia.hardware.power.statecontrol/admin.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#35)*

<p>Provides administration services for the device manager service and the device tree it controls.</p>

### Suspend {#Suspend}

<p>Ask all devices to enter into the system power state indicated by 'state'.
The devices will get into a low power state, that corresponds to the system
power state 'state'.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#SystemPowerState'>SystemPowerState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Admin_Suspend_Result'>Admin_Suspend_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Admin_Suspend_Response {#Admin_Suspend_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### SystemPowerState {#SystemPowerState}
Type: <code>uint8</code>

*Defined in [fuchsia.hardware.power.statecontrol/admin.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#22)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FULLY_ON</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>REBOOT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>REBOOT_BOOTLOADER</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>REBOOT_RECOVERY</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>POWEROFF</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEXEC</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>SUSPEND_RAM</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Admin_Suspend_Result {#Admin_Suspend_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Admin_Suspend_Response'>Admin_Suspend_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#12">SUSPEND_FLAG_REBOOT</a></td>
            <td>
                    <code>3705405696</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>All available suspend flags.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#13">SUSPEND_FLAG_REBOOT_BOOTLOADER</a></td>
            <td>
                    <code>3705405697</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#14">SUSPEND_FLAG_REBOOT_RECOVERY</a></td>
            <td>
                    <code>3705405698</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#15">SUSPEND_FLAG_POWEROFF</a></td>
            <td>
                    <code>3705405952</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#16">SUSPEND_FLAG_MEXEC</a></td>
            <td>
                    <code>3705406208</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#17">SUSPEND_FLAG_SUSPEND_RAM</a></td>
            <td>
                    <code>3705406464</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-power-statecontrol/admin.fidl#31">MAX_SYSTEM_POWER_STATES</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



