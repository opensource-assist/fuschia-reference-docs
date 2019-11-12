[TOC]

# fuchsia.device


## **PROTOCOLS**

## Controller {#Controller}
*Defined in [fuchsia.device/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#128)*

 Interface for manipulating a device in a devhost

### Bind {#Bind}

 Attempt to bind the requested driver to this device

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>driver</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_Bind_Result'>Controller_Bind_Result</a></code>
            </td>
        </tr></table>

### Rebind {#Rebind}

 This api will unbind all the children of this device and bind the
 requested driver. If the driver is empty, it will autobind.
 The Rebind will not return until the bind completes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>driver</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_Rebind_Result'>Controller_Rebind_Result</a></code>
            </td>
        </tr></table>

### ScheduleUnbind {#ScheduleUnbind}

 Disconnect this device and allow its parent to be bound again.
 This may not complete before it returns.

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
                <code><a class='link' href='#Controller_ScheduleUnbind_Result'>Controller_ScheduleUnbind_Result</a></code>
            </td>
        </tr></table>

### GetDriverName {#GetDriverName}

 Return the name of the driver managing this the device

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
            <td><code>name</code></td>
            <td>
                <code>string[32]?</code>
            </td>
        </tr></table>

### GetDeviceName {#GetDeviceName}

 Return the name of the device

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[32]</code>
            </td>
        </tr></table>

### GetTopologicalPath {#GetTopologicalPath}

 Return the topological path for this device

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
            <td><code>path</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr></table>

### GetTopologicalPathNew {#GetTopologicalPathNew}

 Return the topological path for this device

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
                <code><a class='link' href='#Controller_GetTopologicalPathNew_Result'>Controller_GetTopologicalPathNew_Result</a></code>
            </td>
        </tr></table>

### GetEventHandle {#GetEventHandle}

 Get an event for monitoring device conditions (see `DEVICE_SIGNAL_*` constants)

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
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;?</code>
            </td>
        </tr></table>

### GetDriverLogFlags {#GetDriverLogFlags}

 Return the current logging flags for this device's driver

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
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetDriverLogFlags {#SetDriverLogFlags}

 Set the logging flags for this device's driver.
 Each set bit in `clear_flags` will be cleared in the log flags state.
 Each set bit in `set_flags` will then be set in the log flags state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>clear_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>set_flags</code></td>
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

### DebugSuspend {#DebugSuspend}

 Debug command: execute the device's suspend hook

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
        </tr></table>

### DebugResume {#DebugResume}

 Debug command: execute the device's resume hook

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
        </tr></table>

### RunCompatibilityTests {#RunCompatibilityTests}

 Runs compatibility tests for the driver that binds to this device.
 The |hook_wait_time| is the time that the driver expects to take for
 each device hook in nanoseconds.
 Returns whether the driver passed the compatibility check.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hook_wait_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetDevicePowerCaps {#GetDevicePowerCaps}

 Gets the device power capabilities. Used by the system wide power manager
 to manage power for this device.

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
                <code><a class='link' href='#Controller_GetDevicePowerCaps_Result'>Controller_GetDevicePowerCaps_Result</a></code>
            </td>
        </tr></table>

### GetDevicePerformanceStates {#GetDevicePerformanceStates}

 Gets the device performance states. Used by the system wide power manager
 to manage power for this device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>states</code></td>
            <td>
                <code>[20]</code>
            </td>
        </tr><tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>

### UpdatePowerStateMapping {#UpdatePowerStateMapping}

 Updates the mapping between system power states to device power states. Used by the system
 wide power manager to manage power for this device

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mapping</code></td>
            <td>
                <code>[7]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_UpdatePowerStateMapping_Result'>Controller_UpdatePowerStateMapping_Result</a></code>
            </td>
        </tr></table>

### GetPowerStateMapping {#GetPowerStateMapping}

 Get the mapping between system power states to device power states. Used by the system
 wide power manager to manage power for this device.

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
                <code><a class='link' href='#Controller_GetPowerStateMapping_Result'>Controller_GetPowerStateMapping_Result</a></code>
            </td>
        </tr></table>

### Suspend {#Suspend}

 Transition this device from a working to a sleep state or from a sleep state to a deeper sleep
 state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_state</code></td>
            <td>
                <code><a class='link' href='#DevicePowerState'>DevicePowerState</a></code>
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
            <td><code>out_state</code></td>
            <td>
                <code><a class='link' href='#DevicePowerState'>DevicePowerState</a></code>
            </td>
        </tr></table>

### Resume {#Resume}

 Transition this device from a sleep state to a working state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_state</code></td>
            <td>
                <code><a class='link' href='#DevicePowerState'>DevicePowerState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Controller_Resume_Result'>Controller_Resume_Result</a></code>
            </td>
        </tr></table>

### SetPerformanceState {#SetPerformanceState}

 Set the performance state of this device to the requested performance state. This is only
 called for the current device and none of the descendants are aware of the state
 transition.
 On success, the out_state and the requested_state is same. If the device is in a working
 state, the performance state will be changed to requested_state immediately. If the device
 is in non-working state, the performance state will be the requested_state whenever the
 device transitions to working state.
 On failure, the out_state will have the state that the device can go into.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>requested_state</code></td>
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
        </tr><tr>
            <td><code>out_state</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### ConfigureAutoSuspend {#ConfigureAutoSuspend}

 Configure autosuspend of device to this deepest sleep state.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enable</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>requested_deepest_sleep_state</code></td>
            <td>
                <code><a class='link' href='#DevicePowerState'>DevicePowerState</a></code>
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

## NameProvider {#NameProvider}
*Defined in [fuchsia.device/name-provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/name-provider.fidl#17)*

 Interface for getting device names.

### GetDeviceName {#GetDeviceName}

 Return the name of this Fuchsia device.

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
                <code><a class='link' href='#NameProvider_GetDeviceName_Result'>NameProvider_GetDeviceName_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Controller_Bind_Response {#Controller_Bind_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_Rebind_Response {#Controller_Rebind_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_ScheduleUnbind_Response {#Controller_ScheduleUnbind_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_GetTopologicalPathNew_Response {#Controller_GetTopologicalPathNew_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_GetDevicePowerCaps_Response {#Controller_GetDevicePowerCaps_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dpstates</code></td>
            <td>
                <code>[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_UpdatePowerStateMapping_Response {#Controller_UpdatePowerStateMapping_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Controller_GetPowerStateMapping_Response {#Controller_GetPowerStateMapping_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mapping</code></td>
            <td>
                <code>[7]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Controller_Resume_Response {#Controller_Resume_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>out_state</code></td>
            <td>
                <code><a class='link' href='#DevicePowerState'>DevicePowerState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DevicePowerStateInfo {#DevicePowerStateInfo}
*Defined in [fuchsia.device/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#90)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state_id</code></td>
            <td>
                <code><a class='link' href='#DevicePowerState'>DevicePowerState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_supported</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Is this state supported?
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>restore_latency</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Restore time for coming out of this state to working D0 state.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>wakeup_capable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Is this device wakeup_capable?
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>system_wake_state</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> Deepest system system sleep state that the device can wake the system from.
</td>
            <td>No default</td>
        </tr>
</table>

### DevicePerformanceStateInfo {#DevicePerformanceStateInfo}
*Defined in [fuchsia.device/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#108)*



 Performance state info for a device. A performance state is relevant only
 when the device is in non-sleeping working device power state.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>state_id</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>restore_latency</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Restore time for coming out of this state to fully working performance state.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_supported</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Is this state supported?
</td>
            <td>No default</td>
        </tr>
</table>

### SystemPowerStateInfo {#SystemPowerStateInfo}
*Defined in [fuchsia.device/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#118)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>suspend_flag</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>wakeup_enable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Should wakeup be enabled from this system state?
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>dev_state</code></td>
            <td>
                <code><a class='link' href='#DevicePowerState'>DevicePowerState</a></code>
            </td>
            <td> Device power state that the device should be in for this system power state.
</td>
            <td>No default</td>
        </tr>
</table>

### NameProvider_GetDeviceName_Response {#NameProvider_GetDeviceName_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### DevicePowerState {#DevicePowerState}
Type: <code>uint8</code>

*Defined in [fuchsia.device/controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#42)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEVICE_POWER_STATE_D0</code></td>
            <td><code>0</code></td>
            <td> Mandatory Working state. Device is fully functional, can take I/O,
 issue interrrupts. This state is mandatory for all devices
 The device enters into this state by default, when powered on.
</td>
        </tr><tr>
            <td><code>DEVICE_POWER_STATE_D1</code></td>
            <td><code>1</code></td>
            <td> [OPTIONAL] Device is not working when in this state. It cannot process
 I/O nor issue interrupts, unless it is armed for some special interrupts
 that can wake up the system/device. When in this state, the restore time
 of getting back to working state is less than other low-power states
 Power savings in this state are lesser than other low power states.
 Device may retain some hardware context and full initialization
 may not be needed when resuming from this state.
</td>
        </tr><tr>
            <td><code>DEVICE_POWER_STATE_D2</code></td>
            <td><code>2</code></td>
            <td> [OPTIONAL] Device is not working when in this state. It cannot process
 I/O nor issue interrupts, unless it is armed for some special interrupts
 that can wake up the system/device. When in this state, the restore time
 of getting back to working state is more than DEVICE_POWER_STATE_D1 and
 less than restore time of getting back from DEVICE_POWER_STATE_D3HOT,
 DEVICE_POWER_STATE_D3COLD. Power savings in this state are lesser
 than DEVICE_POWER_STATE_D3COLD, DEVICE_POWER_STATE_D3HOT.
 Device may retain some hardware context and full initialization
 may not be needed when resuming from this state.
</td>
        </tr><tr>
            <td><code>DEVICE_POWER_STATE_D3HOT</code></td>
            <td><code>3</code></td>
            <td> [OPTIONAL] Device is not working when in this state. It cannot process
 I/O nor issue interrupts, unless it is armed for some special interrupts
 that can wake up the system/device. When in this state, the restore time
 of getting back to working state is more than DEVICE_POWER_STATE_D1,
 DEVICE_POWER_STATE_D3HOT and less than restore time of getting back from
 DEVICE_POWER_STATE_D3COLD. Power savings in this state are lesser
 than DEVICE_POWER_STATE_D3COLD. Device has no context and full initialization
 by the device driver when resuming from this state.
 Although the device is completely off, it is still powered on and is enumerable.
</td>
        </tr><tr>
            <td><code>DEVICE_POWER_STATE_D3COLD</code></td>
            <td><code>4</code></td>
            <td> [MANDATORY] Device is not working when in this state. It cannot process
 I/O nor issue interrupts, unless it is armed for some special interrupts
 that can wake up the system/device. When in this state, the restore time
 of getting back to working state is more than all other low power states.
 Power savings are more compared to all other low-power states.
 Device has no context and full initialization by the device driver when
 resuming from this state. In this state, the power to this device is turned off.
 Device may be powered by other auxiliary supplies to support wake capability.
</td>
        </tr></table>





## **UNIONS**

### Controller_Bind_Result {#Controller_Bind_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Bind_Response'>Controller_Bind_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_Rebind_Result {#Controller_Rebind_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Rebind_Response'>Controller_Rebind_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_ScheduleUnbind_Result {#Controller_ScheduleUnbind_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_ScheduleUnbind_Response'>Controller_ScheduleUnbind_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_GetTopologicalPathNew_Result {#Controller_GetTopologicalPathNew_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_GetTopologicalPathNew_Response'>Controller_GetTopologicalPathNew_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_GetDevicePowerCaps_Result {#Controller_GetDevicePowerCaps_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_GetDevicePowerCaps_Response'>Controller_GetDevicePowerCaps_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_UpdatePowerStateMapping_Result {#Controller_UpdatePowerStateMapping_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_UpdatePowerStateMapping_Response'>Controller_UpdatePowerStateMapping_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_GetPowerStateMapping_Result {#Controller_GetPowerStateMapping_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_GetPowerStateMapping_Response'>Controller_GetPowerStateMapping_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Controller_Resume_Result {#Controller_Resume_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Controller_Resume_Response'>Controller_Resume_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### NameProvider_GetDeviceName_Result {#NameProvider_GetDeviceName_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#NameProvider_GetDeviceName_Response'>NameProvider_GetDeviceName_Response</a></code>
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
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#11">MAX_DEVICE_NAME_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maxmium length for a device name
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#13">MAX_DEVICE_PATH_LEN</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maximum length of a device path
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#15">MAX_DRIVER_NAME_LEN</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maxmium length for a driver name
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#17">MAX_DRIVER_PATH_LEN</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint64</code></td>
            <td> Maximum length for a driver path
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#20">MAX_DEVICE_POWER_STATES</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum device power states. In future this should account
 for performance states.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#21">MIN_DEVICE_POWER_STATES</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#22">MAX_DEVICE_PERFORMANCE_STATES</a></td>
            <td>
                    <code>20</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#23">MIN_DEVICE_PERFORMANCE_STATES</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#27">DEVICE_SIGNAL_READABLE</a></td>
            <td>
                    <code>16777216</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on a device event handle if the device's read() method
 will return data.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#31">DEVICE_SIGNAL_OOB</a></td>
            <td>
                    <code>33554432</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on a device event handle if the device has some out-of-band
 mechanism that needs attention.
 This is primarily used by the PTY support.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#34">DEVICE_SIGNAL_WRITABLE</a></td>
            <td>
                    <code>67108864</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on a device event handle if the device's write() method
 will accept data.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#37">DEVICE_SIGNAL_ERROR</a></td>
            <td>
                    <code>134217728</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on a device event handle if the device has encountered an error.
 This is primarily used by the PTY support.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#40">DEVICE_SIGNAL_HANGUP</a></td>
            <td>
                    <code>268435456</code>
                </td>
                <td><code>uint32</code></td>
            <td> Signal that will be active on a device event handle if the device has been disconnected.
 This is primarily used by the PTY support.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/controller.fidl#87">DEVICE_PERFORMANCE_STATE_P0</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
            <td> [MANDATORY] Default performance state when the device is in DEVICE_POWER_STATE_D0
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/name-provider.fidl#9">DEFAULT_DEVICE_NAME</a></td>
            <td><code>fuchsia</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device/name-provider.fidl#13">DEVICE_NAME_MAX</a></td>
            <td>
                    <code>255</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum length of a device name (without a null byte), based on
 HOST_NAME_MAX as defined by <limits.h>.
</td>
        </tr>
    
</table>

