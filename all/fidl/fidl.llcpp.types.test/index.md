Project: /_project.yaml
Book: /_book.yaml

# fidl.llcpp.types.test


## **PROTOCOLS**

## TestInterface {:#TestInterface}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#39)*


### TestMethod {:#TestMethod}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#TestUnion'>TestUnion</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#TestUnion'>TestUnion</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### CopyableStruct {:#CopyableStruct}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MoveOnlyStruct {:#MoveOnlyStruct}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>h</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### SampleTable {:#SampleTable}


*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#33)*

 Verifies that user code can build and access tables.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>x</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>y</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>vector_of_struct</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#CopyableStruct'>CopyableStruct</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### TestUnion {:#TestUnion}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#16)*

 Verifies that user code can manipulate these union payloads.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>primitive</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>copyable</code></td>
            <td>
                <code><a class='link' href='#CopyableStruct'>CopyableStruct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>move_only</code></td>
            <td>
                <code><a class='link' href='#MoveOnlyStruct'>MoveOnlyStruct</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**

### SampleBits {:#SampleBits}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>B</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>D</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>E</td>
            <td>8</td>
            <td></td>
        </tr></table>



