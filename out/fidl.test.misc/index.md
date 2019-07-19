Project: /_project.yaml
Book: /_book.yaml

# fidl.test.misc


## **PROTOCOLS**

## Echo {:#Echo}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#128)*


### EchoString {:#EchoString}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>

## NameCollision {:#NameCollision}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#132)*


## ReturnsCollision {:#ReturnsCollision}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#135)*


### NameCollision {:#NameCollision}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>collision</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#NameCollision'>NameCollision</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Int64Struct {:#Int64Struct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HasOptionalFieldStruct {:#HasOptionalFieldStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#22)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Has2OptionalFieldStruct {:#Has2OptionalFieldStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#26)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Empty {:#Empty}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### EmptyStructSandwich {:#EmptyStructSandwich}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>e</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#Empty'>Empty</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SampleXUnionInStruct {:#SampleXUnionInStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#87)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SampleXUnion'>SampleXUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InlineXUnionInStruct {:#InlineXUnionInStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#91)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SampleXUnion'>SampleXUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### OptionalXUnionInStruct {:#OptionalXUnionInStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#97)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SampleXUnion'>SampleXUnion</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VariousDefaults {:#VariousDefaults}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#121)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>int64_with_default</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>5</td>
        </tr><tr>
            <td><code>string_with_default</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>stuff</td>
        </tr><tr>
            <td><code>enum_with_default</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SampleEnum'>SampleEnum</a></code>
            </td>
            <td></td>
            <td><a class='link' href='../fidl.test.misc/index.html#MEMBER_B'>MEMBER_B</a></td>
        </tr><tr>
            <td><code>bool_with_default</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr>
</table>



## **ENUMS**

### SampleEnum {:#SampleEnum}
Type: <code>uint32</code>

*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#115)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>MEMBER_A</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEMBER_B</code></td>
            <td><code>34</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEMBER_C</code></td>
            <td><code>45</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### SimpleTable {:#SimpleTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#48)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>y</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr></table>

### OlderSimpleTable {:#OlderSimpleTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#58)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr></table>

### NewerSimpleTable {:#NewerSimpleTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#65)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>y</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>z</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr></table>

### ComplexTable {:#ComplexTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#75)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>simple</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SampleXUnion'>SampleXUnion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>strings</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
        </tr></table>

### XUnionInTable {:#XUnionInTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#103)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SampleXUnion'>SampleXUnion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### PrimitiveArrayInTable {:#PrimitiveArrayInTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#109)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>arr</code></td>
            <td>
                <code>int32[9]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>after</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### SimpleUnion {:#SimpleUnion}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#40)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>i64</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#Int64Struct'>Int64Struct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>os</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>str</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### SampleXUnion {:#SampleXUnion}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#81)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>su</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SimpleUnion'>SimpleUnion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>st</code></td>
            <td>
                <code><a class='link' href='../fidl.test.misc/index.html#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
        </tr></table>



## **BITS**
### Uint32Bits {:#Uint32Bits}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>ONE</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>TWO</td>
            <td>2</td>
            <td></td>
        </tr></table>### SampleBits {:#SampleBits}
Type: <code>uint32</code>


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



