Project: /_project.yaml
Book: /_book.yaml

# fidl.examples.example5


## **PROTOCOLS**

## Thing {:#Thing}
*Defined in [fidl.examples.example5/example-5.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-5.test.fidl#32)*


### one_function {:#one_function}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### two_function {:#two_function}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### three_function {:#three_function}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>r</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fidl.examples.example5/index.html#Thing'>Thing</a>&gt;</code>
            </td>
        </tr></table>



### four_function {:#four_function}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>r</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fidl.examples.example5/index.html#Thing'>Thing</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>r</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### Point {:#Point}
*Defined in [fidl.examples.example5/example-5.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-5.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Enum {:#Enum}
Type: <code>uint32</code>

*Defined in [fidl.examples.example5/example-5.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-5.test.fidl#17)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### Enum2 {:#Enum2}
Type: <code>uint64</code>

*Defined in [fidl.examples.example5/example-5.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-5.test.fidl#21)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>enum_0</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>enum_1</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### Enum23 {:#Enum23}
Type: <code>int32</code>

*Defined in [fidl.examples.example5/example-5.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-5.test.fidl#26)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>enum_3</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>enum_4</code></td>
            <td><code>-23</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### NotAPoint {:#NotAPoint}
*Defined in [fidl.examples.example5/example-5.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/example-5.test.fidl#11)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr></table>







