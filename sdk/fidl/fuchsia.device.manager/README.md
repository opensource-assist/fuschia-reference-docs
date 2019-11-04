[TOC]

# fuchsia.device.manager


## **PROTOCOLS**

## Administrator {#Administrator}
*Defined in [fuchsia.device.manager/administrator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#33)*

 Provides administration services for the device manager service and the device tree it controls.

### Suspend {#Suspend}

 Ask all devices to enter the suspend state indicated by `flags`. Flags should be some
 combination of `DEVICE_SUSPEND_FLAG_*` from the DDK.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
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

## DeviceController {#DeviceController}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#108)*

 Protocol for controlling devices in a devhost process from the devcoordinator

### BindDriver {#BindDriver}

 Bind the requested driver to this device.  `driver_path` is informational,
 but all calls to BindDriver/CreateDevice should use the same `driver_path`
 each time they use a `driver` VMO with the same contents. Returns a `status`
 and optionally a channel to the driver's test output. `test_output` will be
 not present unless the driver is configured to run its run_unit_tests hook, in
 which case the other end of the channel will have been passed to the driver.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>driver_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>driver</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
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
            <td><code>test_output</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
        </tr></table>

### ConnectProxy {#ConnectProxy}

 Give this device a channel to its shadow in another process.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>shadow</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### Unbind {#Unbind}

 Ask devhost to unbind this device. On success, the remote end of this
 interface channel will close instead of returning a result.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### CompleteRemoval {#CompleteRemoval}

 Ask the devhost to complete the removal of this device, which previously had
 invoked |ScheduleRemove|. This is a special case that can be removed
 once |device_remove| invokes |unbind|.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Suspend {#Suspend}

 Ask devhost to suspend this device, using the target state indicated by `flags`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>flags</code></td>
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

### Resume {#Resume}

 Ask devhost to resume this device, using the target system state indicated by
 'target_system_state'.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>target_system_state</code></td>
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

### CompleteCompatibilityTests {#CompleteCompatibilityTests}

 Inform devhost about the compatibility test status when compatibility tests
 fail or complete successfully.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#CompatibilityTestStatus'>CompatibilityTestStatus</a></code>
            </td>
        </tr></table>



## DevhostController {#DevhostController}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#146)*

 Protocol for controlling a devhost process from the devcoordinator

### CreateDeviceStub {#CreateDeviceStub}

 Create a device in the devhost that only implements the device protocol
 and claims to support the given `protocol_id`.  This device will communicate
 with the devcoordinator via `rpc`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rpc</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>protocol_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>local_device_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CreateDevice {#CreateDevice}

 Create a device in the devhost representing the shadowed half of device
 in another devhost.  This new device will communicate with the devcoordinator
 via `rpc`, and with its other half via `parent_proxy`.

 The new device will have the given driver responsible for running its half
 of the driver's cross-process protocol.  It's create() method will be invoked,
 giving it access to `parent_proxy` and `proxy_args`.

 parent_proxy, if present, will usually be a channel to the upper half of
 a shadowed device.  The one exception is when this method is used
 to create the Platform Bus, in which case it will be a channel to a
 fuchsia.boot.Items protocol.

 `local_device_id` will be a unique value within the device's devhost

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rpc</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>driver_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>driver</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>parent_proxy</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
        </tr><tr>
            <td><code>proxy_args</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr><tr>
            <td><code>local_device_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CreateCompositeDevice {#CreateCompositeDevice}

 Introduce a composite device that has the given name and properties.
 `components` will be a list of all of the composite's components,
 described using devhost local device ids.  The order of the components
 will match the original composite creation request.  The new device will
 communicate with devcoordinator via `rpc`.

 `local_device_id` will be a unique value within the device's devhost, identifying
 the resulting composite device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rpc</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>components</code></td>
            <td>
                <code>vector&lt;uint64&gt;[16]</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[31]</code>
            </td>
        </tr><tr>
            <td><code>local_device_id</code></td>
            <td>
                <code>uint64</code>
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

## Coordinator {#Coordinator}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#185)*

 Interface for the devices in devhosts to coordinate with the devcoordinator.

### AddDevice {#AddDevice}

 Record the addition of a new device that can be communicated with via `rpc`.
 For binding purposes, it is has properties `props`. `name` and `driver_path`
 are informational and used for debugging.  The device will have `protocol_id`
 as its primary protocol id.  `args` should only be used for shadowed devices,
 and will be forwarded to the shadow device. `client_remote`, if present,
 will be passed to the device as an open connection for the client.
 On success, the returned `local_device_id` is the identifier assigned by devmgr.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rpc</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>props</code></td>
            <td>
                <code>vector&lt;uint64&gt;[256]</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[31]</code>
            </td>
        </tr><tr>
            <td><code>protocol_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>driver_path</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr><tr>
            <td><code>args</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr><tr>
            <td><code>device_add_config</code></td>
            <td>
                <code><a class='link' href='#AddDeviceConfig'>AddDeviceConfig</a></code>
            </td>
        </tr><tr>
            <td><code>client_remote</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddDevice_Result'>Coordinator_AddDevice_Result</a></code>
            </td>
        </tr></table>

### AddDeviceInvisible {#AddDeviceInvisible}

 Behaves as AddDevice, but marks the device as initially invisible.  This means
 that it will not be visible to other devices or the devfs until it is later marked
 visible (via MakeVisible).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>rpc</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>props</code></td>
            <td>
                <code>vector&lt;uint64&gt;[256]</code>
            </td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[31]</code>
            </td>
        </tr><tr>
            <td><code>protocol_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>driver_path</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr><tr>
            <td><code>args</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr><tr>
            <td><code>client_remote</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddDeviceInvisible_Result'>Coordinator_AddDeviceInvisible_Result</a></code>
            </td>
        </tr></table>

### ScheduleRemove {#ScheduleRemove}

 Requests the devcoordinator schedule the removal of this device,
 and the unbinding of its children.
 If |unbind_self| is true, the unbind hook for this device will also be called.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>unbind_self</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### ScheduleUnbindChildren {#ScheduleUnbindChildren}

 Requests the devcoordinator schedule the unbinding of this device's children.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### UnbindDone {#UnbindDone}

 Sent as the response to |Unbind|.

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
                <code><a class='link' href='#Coordinator_UnbindDone_Result'>Coordinator_UnbindDone_Result</a></code>
            </td>
        </tr></table>

### RemoveDone {#RemoveDone}

 Sent as the response to |CompleteRemoval|.

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
                <code><a class='link' href='#Coordinator_RemoveDone_Result'>Coordinator_RemoveDone_Result</a></code>
            </td>
        </tr></table>

### MakeVisible {#MakeVisible}

 Mark this device as visible.

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
                <code><a class='link' href='#Coordinator_MakeVisible_Result'>Coordinator_MakeVisible_Result</a></code>
            </td>
        </tr></table>

### BindDevice {#BindDevice}

 Attempt to bind a driver against this device.  If `driver_path` is null,
 this will initiate the driver matching algorithm.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>driver_path</code></td>
            <td>
                <code>string[1024]?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_BindDevice_Result'>Coordinator_BindDevice_Result</a></code>
            </td>
        </tr></table>

### GetTopologicalPath {#GetTopologicalPath}

 Returns the topological path of this device.

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
                <code><a class='link' href='#Coordinator_GetTopologicalPath_Result'>Coordinator_GetTopologicalPath_Result</a></code>
            </td>
        </tr></table>

### LoadFirmware {#LoadFirmware}

 Requests that the firmware at the given path be loaded and returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fw_path</code></td>
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
                <code><a class='link' href='#Coordinator_LoadFirmware_Result'>Coordinator_LoadFirmware_Result</a></code>
            </td>
        </tr></table>

### GetMetadata {#GetMetadata}

 Retrieve the metadata blob associated with this device and the given key.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_GetMetadata_Result'>Coordinator_GetMetadata_Result</a></code>
            </td>
        </tr></table>

### GetMetadataSize {#GetMetadataSize}

 Retrieve the metadata size associated with this device and the given key.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_GetMetadataSize_Result'>Coordinator_GetMetadataSize_Result</a></code>
            </td>
        </tr></table>

### AddMetadata {#AddMetadata}

 Add metadata blob associated with this device and the given key.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddMetadata_Result'>Coordinator_AddMetadata_Result</a></code>
            </td>
        </tr></table>

### PublishMetadata {#PublishMetadata}

 Behaves like AddMetadata, but instead of associating it with the
 requesting device, associates it with the device at `device_path`.  If
 the device at `device_path` is not a child of the requesting device AND
 the requesting device is not running in the sys devhost, then this will
 fail.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_path</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_PublishMetadata_Result'>Coordinator_PublishMetadata_Result</a></code>
            </td>
        </tr></table>

### AddCompositeDevice {#AddCompositeDevice}

 Adds the given composite device.  This causes the devcoordinator to try to match the
 components against the existing device tree, and to monitor all new device additions
 in order to find the components as they are created.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>name</code></td>
            <td>
                <code>string[31]</code>
            </td>
        </tr><tr>
            <td><code>comp_desc</code></td>
            <td>
                <code><a class='link' href='#CompositeDeviceDescriptor'>CompositeDeviceDescriptor</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddCompositeDevice_Result'>Coordinator_AddCompositeDevice_Result</a></code>
            </td>
        </tr></table>

### DirectoryWatch {#DirectoryWatch}

 Watches a directory, receiving events of added messages on the
 watcher request channel.
 See fuchsia.io.Directory for more information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mask</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>options</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>watcher</code></td>
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
                <code><a class='link' href='#Coordinator_DirectoryWatch_Result'>Coordinator_DirectoryWatch_Result</a></code>
            </td>
        </tr></table>

### RunCompatibilityTests {#RunCompatibilityTests}

 Run Compatibility tests for the driver that binds to this device.
 The hook_wait_time is the time that the driver expects to take for
 each device hook in nanoseconds.
 Returns whether the compatibility tests started, and does not convey
 anything about the status of the test.

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
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Coordinator_RunCompatibilityTests_Result'>Coordinator_RunCompatibilityTests_Result</a></code>
            </td>
        </tr></table>

## DebugDumper {#DebugDumper}
*Defined in [fuchsia.device.manager/debug.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/debug.fidl#15)*

 Dumps text debug information.

 All methods dump ascii text into a VMO, this allows the caller the flexibility to decide
 how much data they want. Use the returned `written` value to read the data, no string
 termination is guaranteed.

### DumpTree {#DumpTree}

 Print device tree into `output`, returns bytes `written` and bytes `available` to write.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
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
            <td><code>written</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>available</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### DumpDrivers {#DumpDrivers}

 Print information about all drivers into `output`, returns bytes `written` and bytes `available` to write.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
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
            <td><code>written</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>available</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### DumpBindingProperties {#DumpBindingProperties}

 Print all devices and their binding properties into `output`, returns bytes `written`
 and bytes `available` to write.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
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
            <td><code>written</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>available</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## **STRUCTS**

### Coordinator_AddDevice_Response {#Coordinator_AddDevice_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>local_device_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Coordinator_AddDeviceInvisible_Response {#Coordinator_AddDeviceInvisible_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>local_device_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Coordinator_UnbindDone_Response {#Coordinator_UnbindDone_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_RemoveDone_Response {#Coordinator_RemoveDone_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_MakeVisible_Response {#Coordinator_MakeVisible_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_BindDevice_Response {#Coordinator_BindDevice_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_GetTopologicalPath_Response {#Coordinator_GetTopologicalPath_Response}
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

### Coordinator_LoadFirmware_Response {#Coordinator_LoadFirmware_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Coordinator_GetMetadata_Response {#Coordinator_GetMetadata_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Coordinator_GetMetadataSize_Response {#Coordinator_GetMetadataSize_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Coordinator_AddMetadata_Response {#Coordinator_AddMetadata_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_PublishMetadata_Response {#Coordinator_PublishMetadata_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_AddCompositeDevice_Response {#Coordinator_AddCompositeDevice_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_DirectoryWatch_Response {#Coordinator_DirectoryWatch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Coordinator_RunCompatibilityTests_Response {#Coordinator_RunCompatibilityTests_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### BindInstruction {#BindInstruction}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>op</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> bitfield that encodes the operation and execution conditions
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>arg</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> bitfield that encodes the arguments
</td>
            <td>No default</td>
        </tr>
</table>

### DeviceComponentPart {#DeviceComponentPart}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#65)*



 A part of a description of a DeviceComponent


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>match_program_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>match_program</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceComponent {#DeviceComponent}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#74)*



 A piece of a composite device


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parts_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>parts</code></td>
            <td>
                <code>[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceMetadata {#DeviceMetadata}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#83)*



 Metadata that can be added to a device


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>data</code></td>
            <td>
                <code>vector&lt;uint8&gt;[8192]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CompositeDeviceDescriptor {#CompositeDeviceDescriptor}
*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#89)*



 Composite device parts and properties


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>props</code></td>
            <td>
                <code>vector&lt;uint64&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>components</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DeviceComponent'>DeviceComponent</a>&gt;[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>coresident_device_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metadata</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DeviceMetadata'>DeviceMetadata</a>&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### SystemPowerState {#SystemPowerState}
Type: <code>uint8</code>

*Defined in [fuchsia.device.manager/administrator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#20)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SYSTEM_POWER_STATE_FULLY_ON</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_POWER_STATE_REBOOT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_POWER_STATE_REBOOT_BOOTLOADER</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_POWER_STATE_REBOOT_RECOVERY</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_POWER_STATE_POWEROFF</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_POWER_STATE_MEXEC</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_POWER_STATE_SUSPEND_RAM</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### CompatibilityTestStatus {#CompatibilityTestStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.device.manager/coordinator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#97)*

 A enum of CompatibilityTestStatus


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_BIND_NO_DDKADD</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_BIND_TIMEOUT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_UNBIND_NO_DDKREMOVE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_UNBIND_TIMEOUT</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_SUSPEND_DDKREMOVE</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERR_INTERNAL</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Coordinator_AddDevice_Result {#Coordinator_AddDevice_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddDevice_Response'>Coordinator_AddDevice_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_AddDeviceInvisible_Result {#Coordinator_AddDeviceInvisible_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddDeviceInvisible_Response'>Coordinator_AddDeviceInvisible_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_UnbindDone_Result {#Coordinator_UnbindDone_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_UnbindDone_Response'>Coordinator_UnbindDone_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_RemoveDone_Result {#Coordinator_RemoveDone_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_RemoveDone_Response'>Coordinator_RemoveDone_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_MakeVisible_Result {#Coordinator_MakeVisible_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_MakeVisible_Response'>Coordinator_MakeVisible_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_BindDevice_Result {#Coordinator_BindDevice_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_BindDevice_Response'>Coordinator_BindDevice_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_GetTopologicalPath_Result {#Coordinator_GetTopologicalPath_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_GetTopologicalPath_Response'>Coordinator_GetTopologicalPath_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_LoadFirmware_Result {#Coordinator_LoadFirmware_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_LoadFirmware_Response'>Coordinator_LoadFirmware_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_GetMetadata_Result {#Coordinator_GetMetadata_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_GetMetadata_Response'>Coordinator_GetMetadata_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_GetMetadataSize_Result {#Coordinator_GetMetadataSize_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_GetMetadataSize_Response'>Coordinator_GetMetadataSize_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_AddMetadata_Result {#Coordinator_AddMetadata_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddMetadata_Response'>Coordinator_AddMetadata_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_PublishMetadata_Result {#Coordinator_PublishMetadata_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_PublishMetadata_Response'>Coordinator_PublishMetadata_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_AddCompositeDevice_Result {#Coordinator_AddCompositeDevice_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_AddCompositeDevice_Response'>Coordinator_AddCompositeDevice_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_DirectoryWatch_Result {#Coordinator_DirectoryWatch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_DirectoryWatch_Response'>Coordinator_DirectoryWatch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Coordinator_RunCompatibilityTests_Result {#Coordinator_RunCompatibilityTests_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Coordinator_RunCompatibilityTests_Response'>Coordinator_RunCompatibilityTests_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>





## **BITS**

### AddDeviceConfig {#AddDeviceConfig}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>ALLOW_MULTI_COMPOSITE</td>
            <td>1</td>
            <td>  Device can be a component in multiple composite devices
</td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#10">SUSPEND_FLAG_REBOOT</a></td>
            <td>
                    <code>3705405696</code>
                </td>
                <td><code>uint32</code></td>
            <td> All available suspend flags
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#11">SUSPEND_FLAG_REBOOT_BOOTLOADER</a></td>
            <td>
                    <code>3705405697</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#12">SUSPEND_FLAG_REBOOT_RECOVERY</a></td>
            <td>
                    <code>3705405698</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#13">SUSPEND_FLAG_POWEROFF</a></td>
            <td>
                    <code>3705405952</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#14">SUSPEND_FLAG_MEXEC</a></td>
            <td>
                    <code>3705406208</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#15">SUSPEND_FLAG_SUSPEND_RAM</a></td>
            <td>
                    <code>3705406464</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/administrator.fidl#29">MAX_SYSTEM_POWER_STATES</a></td>
            <td>
                    <code>7</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#31">DEVICE_NAME_MAX</a></td>
            <td>
                    <code>31</code>
                </td>
                <td><code>uint32</code></td>
            <td> This definition must match `ZX_DEVICE_NAME_MAX` and is checked by a static assert.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#35">DEVICE_PATH_MAX</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of bytes in a path
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#38">DEVICE_ARGS_MAX</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of bytes in a device arguments string.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#41">METADATA_BYTES_MAX</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of bytes in a metadata payload
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#44">METADATA_MAX</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of metadata that can be added to a device
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#47">PROPERTIES_MAX</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of properties that can be attached to a device
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#50">COMPONENTS_MAX</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of components that a composite device can have
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#53">DEVICE_COMPONENT_PARTS_MAX</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum number of parts that a composite device component can have
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-device-manager/coordinator.fidl#56">DEVICE_COMPONENT_PART_INSTRUCTIONS_MAX</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td> Maximum instructions in a match program
</td>
        </tr>
    
</table>

