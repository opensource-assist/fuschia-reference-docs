[TOC]

# test.fidlcodec.examples


## **PROTOCOLS**

## Echo {#Echo}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#7)*


### EchoString {#EchoString}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>string[100]?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>response</code></td>
            <td>
                <code>string[100]?</code>
            </td>
        </tr></table>

## FidlCodecTestInterface {#FidlCodecTestInterface}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#11)*


### Empty {#Empty}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### String {#String}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>



### Bool {#Bool}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### Int8 {#Int8}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i8</code></td>
            <td>
                <code>int8</code>
            </td>
        </tr></table>



### Int16 {#Int16}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i16</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>



### Int32 {#Int32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### Int64 {#Int64}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i64</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### Uint8 {#Uint8}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui8</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>



### Uint16 {#Uint16}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui16</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Uint32 {#Uint32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui32</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### Uint64 {#Uint64}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui64</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### Float32 {#Float32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>f32</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### Float64 {#Float64}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>f64</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>



### Complex {#Complex}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>real</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>imaginary</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### StringInt {#StringInt}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### Array1 {#Array1}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>b_1</code></td>
            <td>
                <code>int32[1]</code>
            </td>
        </tr></table>



### Array2 {#Array2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>b_2</code></td>
            <td>
                <code>int32[2]</code>
            </td>
        </tr></table>



### Vector {#Vector}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v_1</code></td>
            <td>
                <code>vector&lt;int32&gt;[10]?</code>
            </td>
        </tr></table>



### TwoStringArrayInt {#TwoStringArrayInt}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>arr</code></td>
            <td>
                <code>[2]</code>
            </td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### TwoStringVectorInt {#TwoStringVectorInt}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>vec</code></td>
            <td>
                <code>vector&lt;string&gt;[10]</code>
            </td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### TwoStringVectors {#TwoStringVectors}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v_1</code></td>
            <td>
                <code>vector&lt;string&gt;[10]</code>
            </td>
        </tr><tr>
            <td><code>v_2</code></td>
            <td>
                <code>vector&lt;string&gt;[10]</code>
            </td>
        </tr></table>



### VectorUint8 {#VectorUint8}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;uint8&gt;[100]</code>
            </td>
        </tr></table>



### VectorUint32 {#VectorUint32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;uint32&gt;[100]</code>
            </td>
        </tr></table>



### VectorStruct {#VectorStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SmallStruct'>SmallStruct</a>&gt;[100]</code>
            </td>
        </tr></table>



### ArrayStruct {#ArrayStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>a</code></td>
            <td>
                <code>[3]</code>
            </td>
        </tr></table>



### VectorStruct2 {#VectorStruct2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SmallUnevenStruct'>SmallUnevenStruct</a>&gt;[100]</code>
            </td>
        </tr></table>



### ArrayStruct2 {#ArrayStruct2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>a</code></td>
            <td>
                <code>[3]</code>
            </td>
        </tr></table>



### Struct {#Struct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>p</code></td>
            <td>
                <code><a class='link' href='#PrimitiveTypes'>PrimitiveTypes</a></code>
            </td>
        </tr></table>



### BoolStruct {#BoolStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#BoolStructType'>BoolStructType</a></code>
            </td>
        </tr></table>



### NullableStruct {#NullableStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>p</code></td>
            <td>
                <code><a class='link' href='#PrimitiveTypes'>PrimitiveTypes</a>?</code>
            </td>
        </tr></table>



### NullableStructAndInt {#NullableStructAndInt}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>p</code></td>
            <td>
                <code><a class='link' href='#PrimitiveTypes'>PrimitiveTypes</a>?</code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### ArrayNullableStruct {#ArrayNullableStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>a</code></td>
            <td>
                <code>[3]</code>
            </td>
        </tr></table>



### SmallStructAfterByte {#SmallStructAfterByte}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>u</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>s1</code></td>
            <td>
                <code><a class='link' href='#SmallStruct'>SmallStruct</a></code>
            </td>
        </tr><tr>
            <td><code>s2</code></td>
            <td>
                <code><a class='link' href='#SmallStruct'>SmallStruct</a></code>
            </td>
        </tr></table>



### TwoStringStructInt {#TwoStringStructInt}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#TwoStringStruct'>TwoStringStruct</a></code>
            </td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### TwoStringNullableStructInt {#TwoStringNullableStructInt}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#TwoStringStruct'>TwoStringStruct</a>?</code>
            </td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### Union {#Union}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>isu</code></td>
            <td>
                <code><a class='link' href='#IntStructUnion'>IntStructUnion</a></code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### NullableUnion {#NullableUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>isu</code></td>
            <td>
                <code><a class='link' href='#IntStructUnion'>IntStructUnion</a>?</code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### NullableUnionIntFirst {#NullableUnionIntFirst}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>isu</code></td>
            <td>
                <code><a class='link' href='#IntStructUnion'>IntStructUnion</a>?</code>
            </td>
        </tr></table>



### ArrayNullableUnion {#ArrayNullableUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>a</code></td>
            <td>
                <code>[3]</code>
            </td>
        </tr></table>



### XUnion {#XUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>isu</code></td>
            <td>
                <code><a class='link' href='#IntStructXunion'>IntStructXunion</a></code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### NullableXUnion {#NullableXUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>isu</code></td>
            <td>
                <code><a class='link' href='#IntStructXunion'>IntStructXunion</a>?</code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### NullableXUnionIntFirst {#NullableXUnionIntFirst}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>isu</code></td>
            <td>
                <code><a class='link' href='#IntStructXunion'>IntStructXunion</a>?</code>
            </td>
        </tr></table>



### ShortUnion {#ShortUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#U8U16Union'>U8U16Union</a></code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### ShortUnionReserved {#ShortUnionReserved}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#U8U16UnionReserved'>U8U16UnionReserved</a></code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### ShortXUnion {#ShortXUnion}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#U8U16Xunion'>U8U16Xunion</a></code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### U8U16UnionStruct {#U8U16UnionStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#U8U16UnionStructType'>U8U16UnionStructType</a></code>
            </td>
        </tr></table>



### DefaultEnumMessage {#DefaultEnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#DefaultEnum'>DefaultEnum</a></code>
            </td>
        </tr></table>



### I8EnumMessage {#I8EnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#I8Enum'>I8Enum</a></code>
            </td>
        </tr></table>



### I16EnumMessage {#I16EnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#I16Enum'>I16Enum</a></code>
            </td>
        </tr></table>



### I32EnumMessage {#I32EnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#I32Enum'>I32Enum</a></code>
            </td>
        </tr></table>



### I64EnumMessage {#I64EnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#I64Enum'>I64Enum</a></code>
            </td>
        </tr></table>



### DefaultBitsMessage {#DefaultBitsMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code><a class='link' href='#DefaultBits'>DefaultBits</a></code>
            </td>
        </tr></table>



### I8BitsMessage {#I8BitsMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code><a class='link' href='#I8Bits'>I8Bits</a></code>
            </td>
        </tr></table>



### I16BitsMessage {#I16BitsMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code><a class='link' href='#I16Bits'>I16Bits</a></code>
            </td>
        </tr></table>



### I32BitsMessage {#I32BitsMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code><a class='link' href='#I32Bits'>I32Bits</a></code>
            </td>
        </tr></table>



### I64BitsMessage {#I64BitsMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code><a class='link' href='#I64Bits'>I64Bits</a></code>
            </td>
        </tr></table>



### Table {#Table}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#ValueTable'>ValueTable</a></code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### Handle {#Handle}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### NullableHandle {#NullableHandle}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
        </tr></table>



### HandleStructMessage {#HandleStructMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hs</code></td>
            <td>
                <code><a class='link' href='#HandleStruct'>HandleStruct</a></code>
            </td>
        </tr></table>



### HandleTableMessage {#HandleTableMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>t</code></td>
            <td>
                <code><a class='link' href='#HandleTable'>HandleTable</a></code>
            </td>
        </tr></table>



### TraversalOrderMessage {#TraversalOrderMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>t</code></td>
            <td>
                <code><a class='link' href='#TraversalOrder'>TraversalOrder</a></code>
            </td>
        </tr></table>



### Protocol {#Protocol}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code><a class='link' href='#ParamProtocol'>ParamProtocol</a></code>
            </td>
        </tr></table>



## ParamProtocol {#ParamProtocol}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#242)*


### Method {#Method}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## FidlCodecXUnion {#FidlCodecXUnion}
*Defined in [test.fidlcodec.examples/xunionmigration.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/xunionmigration.fidl#7)*


### SendAfterMigration {#SendAfterMigration}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#NowAsXUnion'>NowAsXUnion</a></code>
            </td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>





## **STRUCTS**

### BoolStructType {#BoolStructType}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#92)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### PrimitiveTypes {#PrimitiveTypes}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#96)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SmallStruct {#SmallStruct}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#111)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>a</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>c</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SmallUnevenStruct {#SmallUnevenStruct}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#117)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>a</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TwoStringStruct {#TwoStringStruct}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#122)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value1</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value2</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### U8U16UnionStructType {#U8U16UnionStructType}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#153)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#U8U16Union'>U8U16Union</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### HandleStruct {#HandleStruct}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#219)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>h1</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>h2</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>h3</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### OptHandleStruct {#OptHandleStruct}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#225)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sh1</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>sh2</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TraversalOrder {#TraversalOrder}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#235)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#OptHandleStruct'>OptHandleStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>h1</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>h2</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### DefaultEnum {#DefaultEnum}
Type: <code>uint32</code>

*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#157)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### I8Enum {#I8Enum}
Type: <code>int8</code>

*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#161)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>-23</code></td>
            <td></td>
        </tr></table>

### I16Enum {#I16Enum}
Type: <code>int16</code>

*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#165)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>-23</code></td>
            <td></td>
        </tr></table>

### I32Enum {#I32Enum}
Type: <code>int32</code>

*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#169)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>-23</code></td>
            <td></td>
        </tr></table>

### I64Enum {#I64Enum}
Type: <code>int64</code>

*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#173)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>-23</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ReservedExample {#ReservedExample}


*Defined in [test.fidlcodec.examples/reserved_member.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/reserved_member.test.fidl#7)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>first_int16</code></td>
            <td>
                <code>int16</code>
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

### ValueTable {#ValueTable}


*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#212)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>first_int16</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>second_struct</code></td>
            <td>
                <code><a class='link' href='#TwoStringStruct'>TwoStringStruct</a></code>
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
            <td><code>third_union</code></td>
            <td>
                <code><a class='link' href='#IntStructUnion'>IntStructUnion</a></code>
            </td>
            <td></td>
        </tr></table>

### HandleTable {#HandleTable}


*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#230)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>h1</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>s1</code></td>
            <td>
                <code><a class='link' href='#OptHandleStruct'>OptHandleStruct</a></code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### IntStructUnion {#IntStructUnion}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#127)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant_i</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant_tss</code></td>
            <td>
                <code><a class='link' href='#TwoStringStruct'>TwoStringStruct</a></code>
            </td>
            <td></td>
        </tr></table>

### U8U16Union {#U8U16Union}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#137)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant_u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant_u16</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr></table>

### U8U16UnionReserved {#U8U16UnionReserved}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#142)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant_u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant_u16</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr></table>

### OriginalUnion {#OriginalUnion}
*Defined in [test.fidlcodec.examples/xunionmigration.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/xunionmigration.fidl#16)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant_u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant_u16</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### IntStructXunion {#IntStructXunion}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#132)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant_i</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant_tss</code></td>
            <td>
                <code><a class='link' href='#TwoStringStruct'>TwoStringStruct</a></code>
            </td>
            <td></td>
        </tr></table>

### U8U16Xunion {#U8U16Xunion}
*Defined in [test.fidlcodec.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/types.test.fidl#148)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant_u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant_u16</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr></table>

### NowAsXUnion {#NowAsXUnion}
*Defined in [test.fidlcodec.examples/xunionmigration.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/lib/fidl_codec/testdata/xunionmigration.fidl#11)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>variant_u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant_u16</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr></table>



## **BITS**

### DefaultBits {#DefaultBits}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>A</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>B</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>C</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>D</td>
            <td>8</td>
            <td></td>
        </tr></table>

### I8Bits {#I8Bits}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>A</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>B</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>C</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>D</td>
            <td>8</td>
            <td></td>
        </tr></table>

### I16Bits {#I16Bits}
Type: <code>uint16</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>A</td>
            <td>256</td>
            <td></td>
        </tr><tr>
            <td>B</td>
            <td>512</td>
            <td></td>
        </tr><tr>
            <td>C</td>
            <td>1024</td>
            <td></td>
        </tr><tr>
            <td>D</td>
            <td>2048</td>
            <td></td>
        </tr></table>

### I32Bits {#I32Bits}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>A</td>
            <td>65536</td>
            <td></td>
        </tr><tr>
            <td>B</td>
            <td>131072</td>
            <td></td>
        </tr><tr>
            <td>C</td>
            <td>262144</td>
            <td></td>
        </tr><tr>
            <td>D</td>
            <td>524288</td>
            <td></td>
        </tr></table>

### I64Bits {#I64Bits}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>A</td>
            <td>4294967296</td>
            <td></td>
        </tr><tr>
            <td>B</td>
            <td>8589934592</td>
            <td></td>
        </tr><tr>
            <td>C</td>
            <td>17179869184</td>
            <td></td>
        </tr><tr>
            <td>D</td>
            <td>34359738368</td>
            <td></td>
        </tr></table>





