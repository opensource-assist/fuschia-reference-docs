[TOC]

# fidl.llcpp.types.test


## **PROTOCOLS**

## TestInterface {#TestInterface}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#44)*


### TestMethod {#TestMethod}


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

## Baz {#Baz}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#55)*


### Foo {#Foo}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>req</code></td>
            <td>
                <code><a class='link' href='#FooRequest'>FooRequest</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>res</code></td>
            <td>
                <code><a class='link' href='#FooResponse'>FooResponse</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### CopyableStruct {#CopyableStruct}
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

### MoveOnlyStruct {#MoveOnlyStruct}
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

### FooRequest {#FooRequest}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#49)*



<p>Verifies that method argument types don't conflict with user-defined types.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FooResponse {#FooResponse}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#52)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### SampleTable {#SampleTable}


*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#38)*

<p>Verifies that user code can build and access tables.</p>


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

### TestUnion {#TestUnion}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#16)*

<p>Verifies that user code can manipulate these union payloads.</p>

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



## **XUNIONS**

### TestXUnion {#TestXUnion}
*Defined in [fidl.llcpp.types.test/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/llcpp/types.test.fidl#22)*


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
        </tr></table>



## **BITS**

### SampleBits {#SampleBits}
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



