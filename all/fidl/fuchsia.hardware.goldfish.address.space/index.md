Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.goldfish.address.space


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.goldfish.address.space/goldfish-address-space.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-address-space/goldfish-address-space.fidl#10)*


### AllocateBlock {:#AllocateBlock}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>size</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>paddr</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
        </tr></table>

### DeallocateBlock {:#DeallocateBlock}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>paddr</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>















