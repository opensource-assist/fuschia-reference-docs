[TOC]

# fuchsia.hardware.securemem


## **PROTOCOLS**

## Device {#Device}
*Defined in [fuchsia.hardware.securemem/securemem.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-securemem/securemem.fidl#11)*

<p>This protocol currently is a temporary measure to allow for services to get the physical address
of a previously pinned VMO until trusted services can be handed BTI handles.</p>

### GetSecureMemoryPhysicalAddress {#GetSecureMemoryPhysicalAddress}

<p>Gets the physical address of a previously pinned VMO.</p>
<p>Note:</p>
<ul>
<li>The VMO must be contiguous.</li>
<li>|secure_mem| is expected to have a stable physical address that is pinned by some other
entity. The protocol implementation should not be expected to keep the VMO pinned.</li>
<li>The server implementation must not use an IOMMU-backed BTI handle, as the physical
address of the VMO being pinned must be stable.</li>
</ul>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>secure_mem</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>paddr</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>















