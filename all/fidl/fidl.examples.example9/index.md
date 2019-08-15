Project: /_project.yaml
Book: /_book.yaml

# fidl.examples.example9


## **PROTOCOLS**

## Echo {:#Echo}
*Defined in [fidl.examples.example9/example-9.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-9.test.fidl#17)*


### Echo32 {:#Echo32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>uint32</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### Echo64 {:#Echo64}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>uint64</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### EchoEnum {:#EchoEnum}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#EchoMe'>EchoMe</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#EchoMe'>EchoMe</a></code>
            </td>
        </tr></table>

### EchoHandle {:#EchoHandle}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr></table>

### EchoChannel {:#EchoChannel}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>

### EchoStruct {:#EchoStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#EchoMore'>EchoMore</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#EchoMore'>EchoMore</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### EchoMore {:#EchoMore}
*Defined in [fidl.examples.example9/example-9.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-9.test.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>first</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>second</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### EchoMe {:#EchoMe}
Type: <code>uint32</code>

*Defined in [fidl.examples.example9/example-9.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-9.test.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>zero</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>one</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>











