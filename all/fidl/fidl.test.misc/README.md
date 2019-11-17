[TOC]

# fidl.test.misc


## **PROTOCOLS**

## Echo {#Echo}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#132)*


### EchoString {#EchoString}


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

## NameCollision {#NameCollision}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#136)*


## ReturnsCollision {#ReturnsCollision}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#139)*


### NameCollision {#NameCollision}


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
                <code><a class='link' href='#NameCollision'>NameCollision</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Int64Struct {#Int64Struct}
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

### HasOptionalFieldStruct {#HasOptionalFieldStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#22)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code><a class='link' href='#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Has2OptionalFieldStruct {#Has2OptionalFieldStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#26)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code><a class='link' href='#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code><a class='link' href='#Int64Struct'>Int64Struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Empty {#Empty}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### EmptyStructSandwich {#EmptyStructSandwich}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#38)*





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
                <code><a class='link' href='#Empty'>Empty</a></code>
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

### SampleXUnionInStruct {#SampleXUnionInStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#91)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InlineXUnionInStruct {#InlineXUnionInStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#95)*





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
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a></code>
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

### OptionalXUnionInStruct {#OptionalXUnionInStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#101)*





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
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a>?</code>
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

### VariousDefaults {#VariousDefaults}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#125)*





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
                <code><a class='link' href='#SampleEnum'>SampleEnum</a></code>
            </td>
            <td></td>
            <td><a class='link' href='#SampleEnum.MEMBER_B'>SampleEnum.MEMBER_B</a></td>
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

### SampleEnum {#SampleEnum}
Type: <code>uint32</code>

*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#119)*



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

### SimpleTable {#SimpleTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#52)*



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

### OlderSimpleTable {#OlderSimpleTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#62)*



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

### NewerSimpleTable {#NewerSimpleTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#69)*



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

### ComplexTable {#ComplexTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#79)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>simple</code></td>
            <td>
                <code><a class='link' href='#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a></code>
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

### XUnionInTable {#XUnionInTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#107)*



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
                <code><a class='link' href='#SampleXUnion'>SampleXUnion</a></code>
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

### PrimitiveArrayInTable {#PrimitiveArrayInTable}


*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#113)*



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

### SimpleUnion {#SimpleUnion}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#44)*


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
                <code><a class='link' href='#Int64Struct'>Int64Struct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>reserved_ordinal_3</code></td>
            <td>
                <code>uint64</code>
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

### XUnionContainingEmptyStruct {#XUnionContainingEmptyStruct}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#34)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>empty</code></td>
            <td>
                <code><a class='link' href='#Empty'>Empty</a></code>
            </td>
            <td></td>
        </tr></table>

### SampleXUnion {#SampleXUnion}
*Defined in [fidl.test.misc/fidl_test.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/lib/fidl/cpp/fidl_test.test.fidl#85)*


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
                <code><a class='link' href='#SimpleUnion'>SimpleUnion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>st</code></td>
            <td>
                <code><a class='link' href='#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
        </tr></table>



## **BITS**

### Uint32Bits {#Uint32Bits}
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
        </tr></table>

### SampleBits {#SampleBits}
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



