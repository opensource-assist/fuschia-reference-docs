Project: /_project.yaml
Book: /_book.yaml

# test.fidlcat.examples


## **PROTOCOLS**

## Echo {:#Echo}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#7)*


### EchoString {:#EchoString}


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

## FidlcatTestInterface {:#FidlcatTestInterface}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#11)*


### Empty {:#Empty}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### String {:#String}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string[100]</code>
            </td>
        </tr></table>



### Bool {:#Bool}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### Int8 {:#Int8}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i8</code></td>
            <td>
                <code>int8</code>
            </td>
        </tr></table>



### Int16 {:#Int16}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i16</code></td>
            <td>
                <code>int16</code>
            </td>
        </tr></table>



### Int32 {:#Int32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr></table>



### Int64 {:#Int64}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>i64</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### Uint8 {:#Uint8}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui8</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr></table>



### Uint16 {:#Uint16}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui16</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### Uint32 {:#Uint32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui32</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### Uint64 {:#Uint64}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ui64</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### Float32 {:#Float32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>f32</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### Float64 {:#Float64}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>f64</code></td>
            <td>
                <code>float64</code>
            </td>
        </tr></table>



### Complex {:#Complex}


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



### StringInt {:#StringInt}


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



### Array1 {:#Array1}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>b_1</code></td>
            <td>
                <code>int32[1]</code>
            </td>
        </tr></table>



### Array2 {:#Array2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>b_2</code></td>
            <td>
                <code>int32[2]</code>
            </td>
        </tr></table>



### Vector {:#Vector}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v_1</code></td>
            <td>
                <code>vector&lt;int32&gt;[10]?</code>
            </td>
        </tr></table>



### TwoStringArrayInt {:#TwoStringArrayInt}


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



### TwoStringVectorInt {:#TwoStringVectorInt}


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



### TwoStringVectors {:#TwoStringVectors}


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



### VectorUint8 {:#VectorUint8}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;uint8&gt;[100]</code>
            </td>
        </tr></table>



### VectorUint32 {:#VectorUint32}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;uint32&gt;[100]</code>
            </td>
        </tr></table>



### Struct {:#Struct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>p</code></td>
            <td>
                <code><a class='link' href='#PrimitiveTypes'>PrimitiveTypes</a></code>
            </td>
        </tr></table>



### NullableStruct {:#NullableStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>p</code></td>
            <td>
                <code><a class='link' href='#PrimitiveTypes'>PrimitiveTypes</a>?</code>
            </td>
        </tr></table>



### NullableStructAndInt {:#NullableStructAndInt}


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



### TwoStringStructInt {:#TwoStringStructInt}


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



### TwoStringNullableStructInt {:#TwoStringNullableStructInt}


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



### Union {:#Union}


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



### NullableUnion {:#NullableUnion}


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



### NullableUnionIntFirst {:#NullableUnionIntFirst}


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



### XUnion {:#XUnion}


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



### NullableXUnion {:#NullableXUnion}


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



### NullableXUnionIntFirst {:#NullableXUnionIntFirst}


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



### ShortUnion {:#ShortUnion}


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



### ShortXUnion {:#ShortXUnion}


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



### DefaultEnumMessage {:#DefaultEnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#DefaultEnum'>DefaultEnum</a></code>
            </td>
        </tr></table>



### I8EnumMessage {:#I8EnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#I8Enum'>I8Enum</a></code>
            </td>
        </tr></table>



### I16EnumMessage {:#I16EnumMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ev</code></td>
            <td>
                <code><a class='link' href='#I16Enum'>I16Enum</a></code>
            </td>
        </tr></table>



### Table {:#Table}


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



### Handle {:#Handle}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>



### NullableHandle {:#NullableHandle}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
        </tr></table>



### HandleStructMessage {:#HandleStructMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>hs</code></td>
            <td>
                <code><a class='link' href='#HandleStruct'>HandleStruct</a></code>
            </td>
        </tr></table>



### TraversalOrderMessage {:#TraversalOrderMessage}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>t</code></td>
            <td>
                <code><a class='link' href='#TraversalOrder'>TraversalOrder</a></code>
            </td>
        </tr></table>



### Protocol {:#Protocol}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ch</code></td>
            <td>
                <code><a class='link' href='#ParamProtocol'>ParamProtocol</a></code>
            </td>
        </tr></table>



## ParamProtocol {:#ParamProtocol}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#147)*


### Method {:#Method}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **STRUCTS**

### PrimitiveTypes {:#PrimitiveTypes}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#71)*





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

### TwoStringStruct {:#TwoStringStruct}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#86)*





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

### HandleStruct {:#HandleStruct}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#129)*





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

### OptHandleStruct {:#OptHandleStruct}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#135)*





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

### TraversalOrder {:#TraversalOrder}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#140)*





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

### DefaultEnum {:#DefaultEnum}
Type: <code>uint32</code>

*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#111)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### I8Enum {:#I8Enum}
Type: <code>int8</code>

*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#115)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>-23</code></td>
            <td></td>
        </tr></table>

### I16Enum {:#I16Enum}
Type: <code>int16</code>

*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#119)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>X</code></td>
            <td><code>-23</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ValueTable {:#ValueTable}


*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#123)*



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
            <td><code>third_union</code></td>
            <td>
                <code><a class='link' href='#IntStructUnion'>IntStructUnion</a></code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### IntStructUnion {:#IntStructUnion}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#91)*


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

### U8U16Union {:#U8U16Union}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#101)*


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

### IntStructXunion {:#IntStructXunion}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#96)*


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

### U8U16Xunion {:#U8U16Xunion}
*Defined in [test.fidlcat.examples/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidlcat/lib/testdata/types.test.fidl#106)*


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





