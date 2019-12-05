[TOC]

# fuchsia.boot


## **PROTOCOLS**

## Arguments {#Arguments}
*Defined in [fuchsia.boot/arguments.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/arguments.fidl#9)*

<p>Protocol for retrieving boot arguments.</p>

### Get {#Get}

<p>Get a <code>vmo</code> containing boot arguments, along with the <code>size</code> of the boot
arguments contained within.</p>

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

## FactoryItems {#FactoryItems}
*Defined in [fuchsia.boot/factory-items.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/factory-items.fidl#9)*

<p>Protocol for retrieving factory boot item payloads.</p>

### Get {#Get}

<p>Gets a <code>payload</code> for a <code>ZBI_TYPE_STORAGE_BOOTFS_FACTORY</code> boot item with
extra field set to <code>extra</code>.</p>
<p>NOTE: We return the <code>length</code> of the item, as VMOs must be page-aligned.</p>

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

## Items {#Items}
*Defined in [fuchsia.boot/items.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/items.fidl#9)*

<p>Protocol for retrieving boot item payloads.</p>

### Get {#Get}

<p>Get a <code>payload</code> for a boot item of <code>type</code> and <code>extra</code>.
NOTE: We return the <code>length</code> of the item, as VMOs must be page-aligned.</p>
<p>For a list of <code>type</code>s, refer to &lt;zircon/boot/image.h&gt;.
For a list of <code>extra</code>s, refer to &lt;zircon/boot/driver-config.h&gt;.</p>

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

## ReadOnlyLog {#ReadOnlyLog}
*Defined in [fuchsia.boot/log.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/log.fidl#9)*

<p>Protocol for providing the kernel log, readable.</p>

### Get {#Get}

<p>Get read-only handle to the kernel <code>log</code>.</p>

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

## WriteOnlyLog {#WriteOnlyLog}
*Defined in [fuchsia.boot/log.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/log.fidl#16)*

<p>Protocol for providing the kernel log, writable.</p>

### Get {#Get}

<p>Get write-only handle to the kernel <code>log</code>.</p>

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

## RootJob {#RootJob}
*Defined in [fuchsia.boot/root-job.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/root-job.fidl#11)*

<p>Protocol for providing the root job.</p>
<p>TODO(ZX-4072): Do not use this without first consulting the Zircon team.</p>

### Get {#Get}

<p>Get the root <code>job</code>.</p>

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

## RootJobForInspect {#RootJobForInspect}
*Defined in [fuchsia.boot/root-job.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/root-job.fidl#19)*

<p>Protocol for providing the root job with restricted rights, specifically:
INSPECT | ENUMERATE | DUPLICATE | TRANSFER</p>

### Get {#Get}

<p>Get the root <code>job</code>.</p>

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

## RootResource {#RootResource}
*Defined in [fuchsia.boot/root-resource.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-boot/root-resource.fidl#9)*

<p>Protocol for providing the root resource.</p>

### Get {#Get}

<p>Get the root |resource|.</p>

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

















