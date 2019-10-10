Project: /_project.yaml
Book: /_book.yaml

# fuchsia.boot


## **PROTOCOLS**

## Arguments {:#Arguments}
*Defined in [fuchsia.boot/arguments.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/arguments.fidl#9)*

 Protocol for retrieving boot arguments.

### Get {:#Get}

 Get a `vmo` containing boot arguments, along with the `size` of the boot
 arguments contained within.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

## FactoryItems {:#FactoryItems}
*Defined in [fuchsia.boot/factory-items.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/factory-items.fidl#9)*

 Protocol for retrieving factory boot item payloads.

### Get {:#Get}

 Gets a `payload` for a `ZBI_TYPE_STORAGE_BOOTFS_FACTORY` boot item with
 extra field set to `extra`.

 NOTE: We return the `length` of the item, as VMOs must be page-aligned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>extra</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr><tr>
            <td><code>length</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

## Items {:#Items}
*Defined in [fuchsia.boot/items.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/items.fidl#9)*

 Protocol for retrieving boot item payloads.

### Get {:#Get}

 Get a `payload` for a boot item of `type` and `extra`.
 NOTE: We return the `length` of the item, as VMOs must be page-aligned.

 For a list of `type`s, refer to <zircon/boot/image.h>.
 For a list of `extra`s, refer to <zircon/boot/driver-config.h>.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>extra</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr><tr>
            <td><code>length</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

## ReadOnlyLog {:#ReadOnlyLog}
*Defined in [fuchsia.boot/log.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/log.fidl#9)*

 Protocol for providing the kernel log, readable.

### Get {:#Get}

 Get read-only handle to the kernel `log`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log</code></td>
            <td>
                <code>handle&lt;debuglog&gt;</code>
            </td>
        </tr></table>

## WriteOnlyLog {:#WriteOnlyLog}
*Defined in [fuchsia.boot/log.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/log.fidl#16)*

 Protocol for providing the kernel log, writable.

### Get {:#Get}

 Get write-only handle to the kernel `log`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>log</code></td>
            <td>
                <code>handle&lt;debuglog&gt;</code>
            </td>
        </tr></table>

## RootJob {:#RootJob}
*Defined in [fuchsia.boot/root-job.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/root-job.fidl#11)*

 Protocol for providing the root job.

 TODO(ZX-4072): Do not use this without first consulting the Zircon team.

### Get {:#Get}

 Get the root `job`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>job</code></td>
            <td>
                <code>handle&lt;job&gt;</code>
            </td>
        </tr></table>

## RootJobForInspect {:#RootJobForInspect}
*Defined in [fuchsia.boot/root-job.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/root-job.fidl#19)*

 Protocol for providing the root job with restricted rights, specifically:
 INSPECT | ENUMERATE | DUPLICATE | TRANSFER

### Get {:#Get}

 Get the root `job`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>job</code></td>
            <td>
                <code>handle&lt;job&gt;</code>
            </td>
        </tr></table>

## RootResource {:#RootResource}
*Defined in [fuchsia.boot/root-resource.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/root-resource.fidl#9)*

 Protocol for providing the root resource.

### Get {:#Get}

 Get the root |resource|.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>resource</code></td>
            <td>
                <code>handle&lt;resource&gt;</code>
            </td>
        </tr></table>















