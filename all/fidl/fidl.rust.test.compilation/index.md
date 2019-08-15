Project: /_project.yaml
Book: /_book.yaml

# fidl.rust.test.compilation


## **PROTOCOLS**

## TestInterface {:#TestInterface}
*Defined in [fidl.rust.test.compilation/compilation.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/rust/fidl/compilation.test.fidl#17)*


### TestMethod {:#TestMethod}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>test_x_union</code></td>
            <td>
                <code><a class='link' href='#TestXUnion'>TestXUnion</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>test_x_union</code></td>
            <td>
                <code><a class='link' href='#TestXUnion'>TestXUnion</a></code>
            </td>
        </tr></table>

### TestErrorMethod {:#TestErrorMethod}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>arg</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#TestInterface_TestErrorMethod_Result'>TestInterface_TestErrorMethod_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### TestInterface_TestErrorMethod_Response {:#TestInterface_TestErrorMethod_Response}
*Defined in [fidl.rust.test.compilation/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#4)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### HasBigArray {:#HasBigArray}
*Defined in [fidl.rust.test.compilation/compilation.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/rust/fidl/compilation.test.fidl#22)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>big_arr</code></td>
            <td>
                <code>uint8[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Result {:#Result}
*Defined in [fidl.rust.test.compilation/compilation.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/rust/fidl/compilation.test.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ensure_that_type_named_result_compiles</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ErrorReturn {:#ErrorReturn}
Type: <code>uint32</code>

*Defined in [fidl.rust.test.compilation/compilation.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/rust/fidl/compilation.test.fidl#11)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CHANGED</code></td>
            <td><code>13</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### TestInterface_TestErrorMethod_Result {:#TestInterface_TestErrorMethod_Result}
*Defined in [fidl.rust.test.compilation/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#7)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#TestInterface_TestErrorMethod_Response'>TestInterface_TestErrorMethod_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#ErrorReturn'>ErrorReturn</a></code>
            </td>
            <td></td>
        </tr></table>

### HasStructWithBigArray {:#HasStructWithBigArray}
*Defined in [fidl.rust.test.compilation/compilation.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/rust/fidl/compilation.test.fidl#26)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant</code></td>
            <td>
                <code><a class='link' href='#HasBigArray'>HasBigArray</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### TestXUnion {:#TestXUnion}
*Defined in [fidl.rust.test.compilation/compilation.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/rust/fidl/compilation.test.fidl#7)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>





