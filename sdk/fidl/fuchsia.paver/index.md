Project: /_project.yaml
Book: /_book.yaml

# fuchsia.paver


## **PROTOCOLS**

## PayloadStream {:#PayloadStream}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#55)*

 Protocol for streaming the FVM payload.

### RegisterVmo {:#RegisterVmo}

 Registers a VMO to stream into.

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
                <code>int32</code>
            </td>
        </tr></table>

### ReadData {:#ReadData}

 Reads data into the pre-registered vmo.

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

## Paver {:#Paver}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#71)*

 Protocol for managing boot partitions.

 Most of the protocol methods rely on auto-discovery of the storage device
 which will be paved. If the device has no pre-initialized storage devices or
 multiple, the methods will fail. For devices with dynamic partitions (i.e. GPT),
 |InitializePartitionTables| and |WipeVolumes| can be used to control which device is
 paved to.

### InitializeAbr {:#InitializeAbr}

 Initializes ABR metadata. Should only be called to initialize ABR
 metadata for the first time (i.e. it should not be called every boot),
 or recover from corrupted ABR metadata.

 Returns `ZX_ERR_NOT_SUPPORTED` if A/B partition scheme is not supported
 and we always boot from configuration A.

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

### QueryActiveConfiguration {:#QueryActiveConfiguration}

 Queries active configuration.

 Returns `ZX_ERR_NOT_SUPPORTED` if A/B partition scheme is not supported
 and we always boot from configuration A.

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
                <code><a class='link' href='#Paver_QueryActiveConfiguration_Result'>Paver_QueryActiveConfiguration_Result</a></code>
            </td>
        </tr></table>

### QueryConfigurationStatus {:#QueryConfigurationStatus}

 Queries status of |configuration|.

 Returns `ZX_ERR_INVALID_ARGS` if `Configuration.RECOVERY` is passed in via |configuration|.

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
                <code><a class='link' href='#Paver_QueryConfigurationStatus_Result'>Paver_QueryConfigurationStatus_Result</a></code>
            </td>
        </tr></table>

### SetConfigurationActive {:#SetConfigurationActive}

 Updates persistent metadata identifying which configuration should be selected as 'primary'
 for booting purposes. Should only be called after `KERNEL` as well as optional
 `VERIFIED_BOOT_METADATA` assets for specified `configuration` were written successfully.

 Returns `ZX_ERR_INVALID_ARGS` if `Configuration.RECOVERY` is passed in via |configuration|.

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
                <code>int32</code>
            </td>
        </tr></table>

### SetConfigurationUnbootable {:#SetConfigurationUnbootable}

 Updates persistent metadata identifying whether |configuration| is bootable.
 Should only be called in the following situations:
 * Before `KERNEL` as well as optional `VERIFIED_BOOT_METADATA` assets for specified
   |configuration| are written.
 * After successfully booting from a new configuration and marking it healthy. This method
   would be then called on the old configuration.
 * After "successfully" booting from a new configuration, but encountering an unrecoverable
   error during health check. This method would be then called on the new configuration.

 If the configuration is unbootable, no action is taken.

 Returns `ZX_ERR_INVALID_ARGS` if `Configuration.RECOVERY` is passed in via |configuration|.

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
                <code>int32</code>
            </td>
        </tr></table>

### SetActiveConfigurationHealthy {:#SetActiveConfigurationHealthy}

 Updates persistent metadata identifying that active configuration is stable. Used to signal
 "rollback to previous slot" logic is not needed anymore. Meant to be called in subsequent
 boot attempt after `SetActiveConfiguration` was called. Will return error if active
 configuration is currently unbootable.

 If the configuration is already marked healthy, no action is taken.

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

### ReadAsset {:#ReadAsset}

 Reads partition corresponding to |configuration| and |asset| into a
 vmo and returns it.

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
                <code><a class='link' href='#Paver_ReadAsset_Result'>Paver_ReadAsset_Result</a></code>
            </td>
        </tr></table>

### WriteAsset {:#WriteAsset}

 Writes partition corresponding to `configuration` and `asset` with data from `payload`.
 `payload` may need to be resized to the partition size, so the provided vmo must have
 been created with `ZX_VMO_RESIZABLE` or must be a child VMO that was created with
 `ZX_VMO_CHILD_RESIZABLE`. Will zero out rest of the partition if `payload` is smaller
 than the size of the partition being written.


 Returns `ZX_ERR_INVALID_ARGS` if `configuration` specifies active configuration.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
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

### WriteVolumes {:#WriteVolumes}

 Writes FVM with data from streamed via `payload`. This potentially affects all
 configurations.

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
                <code>int32</code>
            </td>
        </tr></table>

### WriteBootloader {:#WriteBootloader}

 Writes bootloader partition with data from `payload`.

 `payload` may need to be resized to the partition size, so the provided vmo must have
 been created with `ZX_VMO_RESIZABLE` or must be a child VMO that was created with
 `ZX_VMO_CHILD_RESIZABLE`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
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

### WriteDataFile {:#WriteDataFile}

 Writes /data/`filename` with data from `payload`. Overwrites file if it already exists.

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
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
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

### WipeVolumes {:#WipeVolumes}

 Wipes the FVM partition from the device. Should not be confused with factory reset, which
 is less intrusive.

 Notable use cases include recovering from corrupted FVM as well as setting device to a
 "clean" state for automation.

 If |block_device| is not provided, the paver will perform a search for
 the the FVM. If multiple block devices have valid GPT, |block_device| can be provided
 to specify which one to target. It assumed that channel backing
 |block_device| also implements `fuchsia.io.Node` for now.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>block_device</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.block/index.html'>fuchsia.hardware.block</a>/<a class='link' href='../fuchsia.hardware.block/index.html#Block'>Block</a>&gt;?</code>
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

### InitializePartitionTables {:#InitializePartitionTables}

 Initializes GPT on given block device and then adds an FVM partition.

 |gpt_block_device| specifies the block device to use. It assumed that channel
 backing |gpt_block_device| also implements `fuchsia.io.Node` for now.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gpt_block_device</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.block/index.html'>fuchsia.hardware.block</a>/<a class='link' href='../fuchsia.hardware.block/index.html#Block'>Block</a>&gt;</code>
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

### WipePartitionTables {:#WipePartitionTables}

 Wipes all entries from the partition table of the specified block device.
 Currently only supported on devices with a GPT.

 If |block_device| is not provided, the paver will perform a search for
 the the FVM. If multiple block devices have valid GPT, |block_device| can be provided
 to specify which one to target. It assumed that channel backing
 |block_device| also implements `fuchsia.io.Node` for now.

 *WARNING*: This API may destructively remove non-fuchsia maintained partitions from
 the block device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>block_device</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.hardware.block/index.html'>fuchsia.hardware.block</a>/<a class='link' href='../fuchsia.hardware.block/index.html#Block'>Block</a>&gt;?</code>
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

### Paver_QueryActiveConfiguration_Response {:#Paver_QueryActiveConfiguration_Response}
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

### Paver_QueryConfigurationStatus_Response {:#Paver_QueryConfigurationStatus_Response}
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

### Paver_ReadAsset_Response {:#Paver_ReadAsset_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>asset</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ReadInfo {:#ReadInfo}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Offset into VMO where read data starts.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Size of read data.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Configuration {:#Configuration}
Type: <code>uint32</code>

*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#13)*

 Describes the version of an asset.


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

### Asset {:#Asset}
Type: <code>uint32</code>

*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#21)*

 Describes assets which may be updated. Each asset has 3 versions, each tied to a particular
 configuration.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>KERNEL</code></td>
            <td><code>1</code></td>
            <td> Zircon Boot Image (ZBI) containing the kernel image as well as bootfs.
</td>
        </tr><tr>
            <td><code>VERIFIED_BOOT_METADATA</code></td>
            <td><code>2</code></td>
            <td> Metadata used for verified boot purposes.
</td>
        </tr></table>

### ConfigurationStatus {:#ConfigurationStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#29)*

 Set of states configuration may be in.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>HEALTHY</code></td>
            <td><code>1</code></td>
            <td> Bootable and health checked.
</td>
        </tr><tr>
            <td><code>PENDING</code></td>
            <td><code>2</code></td>
            <td> Bootable but not yet marked healthy.
</td>
        </tr><tr>
            <td><code>UNBOOTABLE</code></td>
            <td><code>3</code></td>
            <td> Unbootable.
</td>
        </tr></table>





## **UNIONS**

### Paver_QueryActiveConfiguration_Result {:#Paver_QueryActiveConfiguration_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Paver_QueryActiveConfiguration_Response'>Paver_QueryActiveConfiguration_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Paver_QueryConfigurationStatus_Result {:#Paver_QueryConfigurationStatus_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Paver_QueryConfigurationStatus_Response'>Paver_QueryConfigurationStatus_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Paver_ReadAsset_Result {:#Paver_ReadAsset_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Paver_ReadAsset_Response'>Paver_ReadAsset_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### ReadResult {:#ReadResult}
*Defined in [fuchsia.paver/paver.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-paver/paver.fidl#45)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>err</code></td>
            <td>
                <code>int32</code>
            </td>
            <td> Error encountered while reading data.
</td>
        </tr><tr>
            <td><code>eof</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> End of file reached.
</td>
        </tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#ReadInfo'>ReadInfo</a></code>
            </td>
            <td> Information about location of successfully read data within pre-registered VMO.
</td>
        </tr></table>







