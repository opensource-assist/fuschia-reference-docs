Project: /_project.yaml
Book: /_book.yaml

# fuchsia.hardware.goldfish.control


## **PROTOCOLS**

## Device {:#Device}
*Defined in [fuchsia.hardware.goldfish.control/goldfish-control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-control/goldfish-control.fidl#16)*


### CreateColorBuffer {:#CreateColorBuffer}

 Create shared color buffer. Color buffer is automatically freed when
 all references to `vmo` have been closed. Fails if VMO is not
 associated with goldfish heap memory.
 Returns ZX_ERR_ALREADY_EXISTS if color buffer has already been created.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>format</code></td>
            <td>
                <code><a class='link' href='#FormatType'>FormatType</a></code>
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

### GetColorBuffer {:#GetColorBuffer}

 Get color buffer for VMO. Fails if VMO is not associated with a color
 buffer.

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
            <td><code>res</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>





## **ENUMS**

### FormatType {:#FormatType}
Type: <code>uint32</code>

*Defined in [fuchsia.hardware.goldfish.control/goldfish-control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-hardware-goldfish-control/goldfish-control.fidl#10)*

 Color buffer formats.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>RGBA</code></td>
            <td><code>6408</code></td>
            <td></td>
        </tr><tr>
            <td><code>BGRA</code></td>
            <td><code>32993</code></td>
            <td></td>
        </tr></table>











