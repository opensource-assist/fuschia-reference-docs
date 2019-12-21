[TOC]

# fuchsia.paver


## **PROTOCOLS**

## PayloadStream {#PayloadStream}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#56)*

<p>Protocol for streaming the FVM payload.</p>

### RegisterVmo {#RegisterVmo}

<p>Registers a VMO to stream into.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### ReadData {#ReadData}

<p>Reads data into the pre-registered vmo.</p>

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
                <code><a class='link' href='#ReadResult'>ReadResult</a></code>
            </td>
        </tr></table>

## Paver {#Paver}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#65)*


### FindDataSink {#FindDataSink}

<p>Attempts to auto-discover the data sink where assets and volumes will get paved to.
On devices with GPT, the partition must have a valid FVM partition in order for
auto-discovery to find it. If multiple devices are found suitable, error is returned.</p>
<p>|data_sink| will be closed on error, with an epitaph provided on failure reason.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data_sink</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DataSink'>DataSink</a>&gt;</code>
            </td>
        </tr></table>



### UseBlockDevice {#UseBlockDevice}

<p>Provide a block device to use as a data sink. Assets and volumes will be paved to
partitions within this block device.</p>
<p>It assumes that channel backing |block_device| also implements <code>fuchsia.io.Node</code> for now.</p>
<p>|data_sink| will be closed on error, with an epitaph provided on failure reason.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>block_device</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.block/'>fuchsia.hardware.block</a>/<a class='link' href='../fuchsia.hardware.block/#Block'>Block</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>data_sink</code></td>
            <td>
                <code>request&lt;<a class='link' href='#DynamicDataSink'>DynamicDataSink</a>&gt;</code>
            </td>
        </tr></table>



### FindBootManager {#FindBootManager}

<p>Attempts to auto-discover the boot manager.</p>
<p>|initialize| should only be set to true to initialize ABR metadata for the first time
(i.e. it should not be called every boot), or recover from corrupted ABR metadata.</p>
<p>|boot_manager| will be closed on error, with an epitaph provided on failure reason.
ZX_ERR_NOT_SUPPORTED indicates lack of support and configuration A is always booted from.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>boot_manager</code></td>
            <td>
                <code>request&lt;<a class='link' href='#BootManager'>BootManager</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>initialize</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## DataSink {#DataSink}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#94)*

<p>Protocol for reading and writing boot partitions.</p>

### ReadAsset {#ReadAsset}

<p>Reads partition corresponding to |configuration| and |asset| into a
vmo and returns it.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
        </tr><tr>
            <td><code>asset</code></td>
            <td>
                <code><a class='link' href='#Asset'>Asset</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#DataSink_ReadAsset_Result'>DataSink_ReadAsset_Result</a></code>
            </td>
        </tr></table>

### WriteAsset {#WriteAsset}

<p>Writes partition corresponding to <code>configuration</code> and <code>asset</code> with data from <code>payload</code>.
<code>payload</code> may need to be resized to the partition size, so the provided vmo must have
been created with <code>ZX_VMO_RESIZABLE</code> or must be a child VMO that was created with
<code>ZX_VMO_CHILD_RESIZABLE</code>. Will zero out rest of the partition if <code>payload</code> is smaller
than the size of the partition being written.</p>
<p>Returns <code>ZX_ERR_INVALID_ARGS</code> if <code>configuration</code> specifies active configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
        </tr><tr>
            <td><code>asset</code></td>
            <td>
                <code><a class='link' href='#Asset'>Asset</a></code>
            </td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WriteVolumes {#WriteVolumes}

<p>Writes FVM with data from streamed via <code>payload</code>. This potentially affects all
configurations.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code>request&lt;<a class='link' href='#PayloadStream'>PayloadStream</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WriteBootloader {#WriteBootloader}

<p>Writes bootloader partition with data from <code>payload</code>.</p>
<p><code>payload</code> may need to be resized to the partition size, so the provided vmo must have
been created with <code>ZX_VMO_RESIZABLE</code> or must be a child VMO that was created with
<code>ZX_VMO_CHILD_RESIZABLE</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WriteDataFile {#WriteDataFile}

<p>Writes /data/<code>filename</code> with data from <code>payload</code>. Overwrites file if it already exists.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>filename</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WipeVolume {#WipeVolume}

<p>Wipes the FVM partition from the device. Should not be confused with factory reset, which
is less intrusive. The result is that the default FVM volumes are re-created, but empty.</p>
<p>Notable use cases include recovering from corrupted FVM as well as setting device to a
&quot;clean&quot; state for automation.</p>
<p>If |block_device| is not provided, the paver will perform a search for the the FVM.
If multiple block devices have valid GPT, |block_device| can be provided to specify
which one to target. It assumed that channel backing |block_device| also implements
<code>fuchsia.io.Node</code> for now.</p>
<p>On success, returns a channel to the initialized FVM volume.</p>

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
                <code><a class='link' href='#DataSink_WipeVolume_Result'>DataSink_WipeVolume_Result</a></code>
            </td>
        </tr></table>

## DynamicDataSink {#DynamicDataSink}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#142)*

<p>Specialized DataSink with dynamic partition tables.</p>

### ReadAsset {#ReadAsset}

<p>Reads partition corresponding to |configuration| and |asset| into a
vmo and returns it.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
        </tr><tr>
            <td><code>asset</code></td>
            <td>
                <code><a class='link' href='#Asset'>Asset</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#DataSink_ReadAsset_Result'>DataSink_ReadAsset_Result</a></code>
            </td>
        </tr></table>

### WriteAsset {#WriteAsset}

<p>Writes partition corresponding to <code>configuration</code> and <code>asset</code> with data from <code>payload</code>.
<code>payload</code> may need to be resized to the partition size, so the provided vmo must have
been created with <code>ZX_VMO_RESIZABLE</code> or must be a child VMO that was created with
<code>ZX_VMO_CHILD_RESIZABLE</code>. Will zero out rest of the partition if <code>payload</code> is smaller
than the size of the partition being written.</p>
<p>Returns <code>ZX_ERR_INVALID_ARGS</code> if <code>configuration</code> specifies active configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
        </tr><tr>
            <td><code>asset</code></td>
            <td>
                <code><a class='link' href='#Asset'>Asset</a></code>
            </td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WriteVolumes {#WriteVolumes}

<p>Writes FVM with data from streamed via <code>payload</code>. This potentially affects all
configurations.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code>request&lt;<a class='link' href='#PayloadStream'>PayloadStream</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WriteBootloader {#WriteBootloader}

<p>Writes bootloader partition with data from <code>payload</code>.</p>
<p><code>payload</code> may need to be resized to the partition size, so the provided vmo must have
been created with <code>ZX_VMO_RESIZABLE</code> or must be a child VMO that was created with
<code>ZX_VMO_CHILD_RESIZABLE</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WriteDataFile {#WriteDataFile}

<p>Writes /data/<code>filename</code> with data from <code>payload</code>. Overwrites file if it already exists.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>filename</code></td>
            <td>
                <code>string[4096]</code>
            </td>
        </tr><tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WipeVolume {#WipeVolume}

<p>Wipes the FVM partition from the device. Should not be confused with factory reset, which
is less intrusive. The result is that the default FVM volumes are re-created, but empty.</p>
<p>Notable use cases include recovering from corrupted FVM as well as setting device to a
&quot;clean&quot; state for automation.</p>
<p>If |block_device| is not provided, the paver will perform a search for the the FVM.
If multiple block devices have valid GPT, |block_device| can be provided to specify
which one to target. It assumed that channel backing |block_device| also implements
<code>fuchsia.io.Node</code> for now.</p>
<p>On success, returns a channel to the initialized FVM volume.</p>

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
                <code><a class='link' href='#DataSink_WipeVolume_Result'>DataSink_WipeVolume_Result</a></code>
            </td>
        </tr></table>

### InitializePartitionTables {#InitializePartitionTables}

<p>Initializes partitions on given block device.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### WipePartitionTables {#WipePartitionTables}

<p>Wipes all entries from the partition table of the specified block device.
Currently only supported on devices with a GPT.</p>
<p><em>WARNING</em>: This API may destructively remove non-fuchsia maintained partitions from
the block device.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

## BootManager {#BootManager}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#157)*

<p>Protocol for managing boot configurations.</p>

### QueryActiveConfiguration {#QueryActiveConfiguration}

<p>Queries active configuration.</p>

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
                <code><a class='link' href='#BootManager_QueryActiveConfiguration_Result'>BootManager_QueryActiveConfiguration_Result</a></code>
            </td>
        </tr></table>

### QueryConfigurationStatus {#QueryConfigurationStatus}

<p>Queries status of |configuration|.</p>
<p>Returns <code>ZX_ERR_INVALID_ARGS</code> if <code>Configuration.RECOVERY</code> is passed in via |configuration|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#BootManager_QueryConfigurationStatus_Result'>BootManager_QueryConfigurationStatus_Result</a></code>
            </td>
        </tr></table>

### SetConfigurationActive {#SetConfigurationActive}

<p>Updates persistent metadata identifying which configuration should be selected as 'primary'
for booting purposes. Should only be called after <code>KERNEL</code> as well as optional
<code>VERIFIED_BOOT_METADATA</code> assets for specified <code>configuration</code> were written successfully.</p>
<p>Returns <code>ZX_ERR_INVALID_ARGS</code> if <code>Configuration.RECOVERY</code> is passed in via |configuration|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SetConfigurationUnbootable {#SetConfigurationUnbootable}

<p>Updates persistent metadata identifying whether |configuration| is bootable.
Should only be called in the following situations:</p>
<ul>
<li>Before <code>KERNEL</code> as well as optional <code>VERIFIED_BOOT_METADATA</code> assets for specified
|configuration| are written.</li>
<li>After successfully booting from a new configuration and marking it healthy. This method
would be then called on the old configuration.</li>
<li>After &quot;successfully&quot; booting from a new configuration, but encountering an unrecoverable
error during health check. This method would be then called on the new configuration.</li>
</ul>
<p>If the configuration is unbootable, no action is taken.</p>
<p>Returns <code>ZX_ERR_INVALID_ARGS</code> if <code>Configuration.RECOVERY</code> is passed in via |configuration|.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>

### SetActiveConfigurationHealthy {#SetActiveConfigurationHealthy}

<p>Updates persistent metadata identifying that active configuration is stable. Used to signal
&quot;rollback to previous slot&quot; logic is not needed anymore. Meant to be called in subsequent
boot attempt after <code>SetActiveConfiguration</code> was called. Will return error if active
configuration is currently unbootable.</p>
<p>If the configuration is already marked healthy, no action is taken.</p>

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
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### DataSink_ReadAsset_Response {#DataSink_ReadAsset_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>asset</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DataSink_WipeVolume_Response {#DataSink_WipeVolume_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>volume</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.block.volume/'>fuchsia.hardware.block.volume</a>/<a class='link' href='../fuchsia.hardware.block.volume/#VolumeManager'>VolumeManager</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BootManager_QueryActiveConfiguration_Response {#BootManager_QueryActiveConfiguration_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#Configuration'>Configuration</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BootManager_QueryConfigurationStatus_Response {#BootManager_QueryConfigurationStatus_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#ConfigurationStatus'>ConfigurationStatus</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ReadInfo {#ReadInfo}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#39)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>offset</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#off'>off</a></code>
            </td>
            <td><p>Offset into VMO where read data starts.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Size of read data.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Configuration {#Configuration}
Type: <code>uint32</code>

*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#14)*

<p>Describes the version of an asset.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>A</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>B</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>RECOVERY</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### Asset {#Asset}
Type: <code>uint32</code>

*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#22)*

<p>Describes assets which may be updated. Each asset has 3 versions, each tied to a particular
configuration.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>KERNEL</code></td>
            <td><code>1</code></td>
            <td><p>Zircon Boot Image (ZBI) containing the kernel image as well as bootfs.</p>
</td>
        </tr><tr>
            <td><code>VERIFIED_BOOT_METADATA</code></td>
            <td><code>2</code></td>
            <td><p>Metadata used for verified boot purposes.</p>
</td>
        </tr></table>

### ConfigurationStatus {#ConfigurationStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#30)*

<p>Set of states configuration may be in.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>HEALTHY</code></td>
            <td><code>1</code></td>
            <td><p>Bootable and health checked.</p>
</td>
        </tr><tr>
            <td><code>PENDING</code></td>
            <td><code>2</code></td>
            <td><p>Bootable but not yet marked healthy.</p>
</td>
        </tr><tr>
            <td><code>UNBOOTABLE</code></td>
            <td><code>3</code></td>
            <td><p>Unbootable.</p>
</td>
        </tr></table>





## **UNIONS**

### DataSink_ReadAsset_Result {#DataSink_ReadAsset_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DataSink_ReadAsset_Response'>DataSink_ReadAsset_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### DataSink_WipeVolume_Result {#DataSink_WipeVolume_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DataSink_WipeVolume_Response'>DataSink_WipeVolume_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### BootManager_QueryActiveConfiguration_Result {#BootManager_QueryActiveConfiguration_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#BootManager_QueryActiveConfiguration_Response'>BootManager_QueryActiveConfiguration_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### BootManager_QueryConfigurationStatus_Result {#BootManager_QueryConfigurationStatus_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#BootManager_QueryConfigurationStatus_Response'>BootManager_QueryConfigurationStatus_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td></td>
        </tr></table>

### ReadResult {#ReadResult}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#46)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#status'>status</a></code>
            </td>
            <td><p>Error encountered while reading data.</p>
</td>
        </tr><tr>
            <td><code>eof</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>End of file reached.</p>
</td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ReadInfo'>ReadInfo</a></code>
            </td>
            <td><p>Information about location of successfully read data within pre-registered VMO.</p>
</td>
        </tr></table>









