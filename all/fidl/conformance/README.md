[TOC]

# conformance


## **PROTOCOLS**

## EthernetDevice {#EthernetDevice}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#19)*




## **STRUCTS**

### ThreeByte {#ThreeByte}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elem1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elem2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elem3</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FiveByte {#FiveByte}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elem1</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elem2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ThreeByteInStruct {#ThreeByteInStruct}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elem1</code></td>
            <td>
                <code><a class='link' href='#ThreeByte'>ThreeByte</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elem2</code></td>
            <td>
                <code><a class='link' href='#ThreeByte'>ThreeByte</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elem3</code></td>
            <td>
                <code><a class='link' href='#ThreeByte'>ThreeByte</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FiveByteInStruct {#FiveByteInStruct}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elem1</code></td>
            <td>
                <code><a class='link' href='#FiveByte'>FiveByte</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elem2</code></td>
            <td>
                <code><a class='link' href='#FiveByte'>FiveByte</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>elem3</code></td>
            <td>
                <code><a class='link' href='#FiveByte'>FiveByte</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ThreeByteInVector {#ThreeByteInVector}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elems</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ThreeByte'>ThreeByte</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FiveByteInVector {#FiveByteInVector}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elems</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#FiveByte'>FiveByte</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ThreeByteInArray {#ThreeByteInArray}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elems</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FiveByteInArray {#FiveByteInArray}
*Defined in [conformance/alignment.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/alignment.test.fidl#42)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>elems</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructWithInt {#StructWithInt}
*Defined in [conformance/arrays_and_vectors.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/arrays_and_vectors.test.fidl#12)*





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

### StructWithArrays {#StructWithArrays}
*Defined in [conformance/arrays_and_vectors.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/arrays_and_vectors.test.fidl#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>arr_int</code></td>
            <td>
                <code>int32[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arr_string</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arr_nullable_string</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arr_struct</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arr_nullable_struct</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arr_arr_int</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructWithVectors {#StructWithVectors}
*Defined in [conformance/arrays_and_vectors.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/arrays_and_vectors.test.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vec_empty</code></td>
            <td>
                <code>vector&lt;int32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vec_int</code></td>
            <td>
                <code>vector&lt;int32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vec_string</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vec_nullable_string</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vec_struct</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StructWithInt'>StructWithInt</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vec_nullable_struct</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StructWithInt'>StructWithInt</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vec_vec_int</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestXUnionInTable {#TestXUnionInTable}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#XUnionInTable'>XUnionInTable</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InterfaceConfig {#InterfaceConfig}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#26)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>ip_address_config</code></td>
            <td>
                <code><a class='link' href='#IpAddressConfig'>IpAddressConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestAddEthernetDeviceRequest {#TestAddEthernetDeviceRequest}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>topological_path</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#InterfaceConfig'>InterfaceConfig</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>this_should_be_a_handle</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NodeAttributes {#NodeAttributes}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mode</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>content_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>storage_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>link_count</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>creation_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>modification_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FileGetAttrResponse {#FileGetAttrResponse}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#NodeAttributes'>NodeAttributes</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructWithOptionals {#StructWithOptionals}
*Defined in [conformance/optionals.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/optionals.test.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>s2</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>t</code></td>
            <td>
                <code><a class='link' href='#TableWithEmptyStruct'>TableWithEmptyStruct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#XUnionWithEmptyStruct'>XUnionWithEmptyStruct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xu2</code></td>
            <td>
                <code><a class='link' href='#XUnionWithEmptyStruct'>XUnionWithEmptyStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#UnionWithEmptyStruct'>UnionWithEmptyStruct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u2</code></td>
            <td>
                <code><a class='link' href='#UnionWithEmptyStruct'>UnionWithEmptyStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyBool {#MyBool}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyByte {#MyByte}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyInt8 {#MyInt8}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyInt16 {#MyInt16}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyInt32 {#MyInt32}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyInt64 {#MyInt64}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#27)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyUint8 {#MyUint8}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyUint16 {#MyUint16}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#35)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyUint32 {#MyUint32}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#39)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyUint64 {#MyUint64}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#43)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyFloat32 {#MyFloat32}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#47)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MyFloat64 {#MyFloat64}
*Defined in [conformance/primitives.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/primitives.test.fidl#51)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Length2StringWrapper {#Length2StringWrapper}
*Defined in [conformance/strings.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/strings.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>length_2_string</code></td>
            <td>
                <code>string[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StringWrapper {#StringWrapper}
*Defined in [conformance/strings.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/strings.test.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>str</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EmptyStruct {#EmptyStruct}
*Defined in [conformance/structs.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/structs.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### EmptyStructSandwich {#EmptyStructSandwich}
*Defined in [conformance/structs.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/structs.test.fidl#9)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>es</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
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

### Uint8Uint16Uint32Uint64 {#Uint8Uint16Uint32Uint64}
*Defined in [conformance/structs.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/structs.test.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>f1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f2</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f3</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f4</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Uint64Uint32Uint16Uint8 {#Uint64Uint32Uint16Uint8}
*Defined in [conformance/structs.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/structs.test.fidl#22)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>f1</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f2</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f3</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f4</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructOfSimpleTable {#StructOfSimpleTable}
*Defined in [conformance/tables.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/tables.test.fidl#15)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SimpleTableThenUint64 {#SimpleTableThenUint64}
*Defined in [conformance/tables.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/tables.test.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#SimpleTable'>SimpleTable</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>number</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructOfTableWithStringAndVector {#StructOfTableWithStringAndVector}
*Defined in [conformance/tables.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/tables.test.fidl#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#TableWithStringAndVector'>TableWithStringAndVector</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructSize16Align8 {#StructSize16Align8}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#20)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>f1</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f2</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich1 {#Sandwich1}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>the_union</code></td>
            <td>
                <code><a class='link' href='#UnionSize8Align4'>UnionSize8Align4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich1WithOptUnion {#Sandwich1WithOptUnion}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>opt_union</code></td>
            <td>
                <code><a class='link' href='#UnionSize8Align4'>UnionSize8Align4</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich2 {#Sandwich2}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#44)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>the_union</code></td>
            <td>
                <code><a class='link' href='#UnionSize12Align4'>UnionSize12Align4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich3 {#Sandwich3}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#50)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>the_union</code></td>
            <td>
                <code><a class='link' href='#UnionSize24Align8'>UnionSize24Align8</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich4 {#Sandwich4}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#63)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>the_union</code></td>
            <td>
                <code><a class='link' href='#UnionSize36Align4'>UnionSize36Align4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich5 {#Sandwich5}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#77)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>union_of_union</code></td>
            <td>
                <code><a class='link' href='#UnionOfUnion'>UnionOfUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructSize3Align1 {#StructSize3Align1}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#83)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>three_bytes</code></td>
            <td>
                <code>uint8[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StructSize3Align2 {#StructSize3Align2}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#87)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>f1</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich6 {#Sandwich6}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#105)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>the_union</code></td>
            <td>
                <code><a class='link' href='#UnionWithVector'>UnionWithVector</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich7 {#Sandwich7}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#111)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>opt_sandwich1</code></td>
            <td>
                <code><a class='link' href='#Sandwich1'>Sandwich1</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich8 {#Sandwich8}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#118)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>union_of_union</code></td>
            <td>
                <code><a class='link' href='#UnionOfUnion'>UnionOfUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Regression1 {#Regression1}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#124)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>f1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f2</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f3</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f4</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f5</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f6</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Regression2 {#Regression2}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#133)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>head</code></td>
            <td>
                <code><a class='link' href='#Regression1'>Regression1</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f7</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Regression3 {#Regression3}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#138)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>opt_value</code></td>
            <td>
                <code><a class='link' href='#Regression2'>Regression2</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Table_StructWithReservedSandwichStruct {#Table_StructWithReservedSandwichStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#157)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#Table_StructWithReservedSandwich'>Table_StructWithReservedSandwich</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Table_StructWithUint32SandwichStruct {#Table_StructWithUint32SandwichStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#168)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#Table_StructWithUint32Sandwich'>Table_StructWithUint32Sandwich</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Table_UnionWithVector_ReservedSandwichStruct {#Table_UnionWithVector_ReservedSandwichStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#178)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#Table_UnionWithVector_ReservedSandwich'>Table_UnionWithVector_ReservedSandwich</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Table_UnionWithVector_StructSandwichStruct {#Table_UnionWithVector_StructSandwichStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#188)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#Table_UnionWithVector_StructSandwich'>Table_UnionWithVector_StructSandwich</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### XUnionWithStructStruct {#XUnionWithStructStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#196)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#XUnionWithStruct'>XUnionWithStruct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### XUnionWithXUnionStruct {#XUnionWithXUnionStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#204)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#XUnionWithXUnion'>XUnionWithXUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Size5Alignment1 {#Size5Alignment1}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#213)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>uint8[5]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Size5Alignment4 {#Size5Alignment4}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#217)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>four</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>one</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Size5Alignment1Vector {#Size5Alignment1Vector}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#222)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Size5Alignment1'>Size5Alignment1</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Size5Alignment4Vector {#Size5Alignment4Vector}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#226)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Size5Alignment4'>Size5Alignment4</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Size5Alignment1Array {#Size5Alignment1Array}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#230)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>a</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Size5Alignment4Array {#Size5Alignment4Array}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#234)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>a</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ArrayStruct {#ArrayStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#244)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>unions</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>optional_unions</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TransformerEmptyStruct {#TransformerEmptyStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#249)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### EmptyStructUnionStruct {#EmptyStructUnionStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#257)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#EmptyStructUnion'>EmptyStructUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Size8Align8 {#Size8Align8}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#261)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### NoCodingTablesStressor {#NoCodingTablesStressor}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#265)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>f1</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f2</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u1</code></td>
            <td>
                <code><a class='link' href='#UnionSize36Align4'>UnionSize36Align4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f3</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f4</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u2</code></td>
            <td>
                <code><a class='link' href='#UnionSize36Align4'>UnionSize36Align4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f5</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f6</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u3</code></td>
            <td>
                <code><a class='link' href='#UnionSize36Align4'>UnionSize36Align4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f7</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>p1</code></td>
            <td>
                <code><a class='link' href='#Size8Align8'>Size8Align8</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f8</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>p2</code></td>
            <td>
                <code><a class='link' href='#Size8Align8'>Size8Align8</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f9</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### OutOfLineSandwich1 {#OutOfLineSandwich1}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#282)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Sandwich1'>Sandwich1</a>&gt;[1]</code>
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

### OutOfLineSandwich1WithOptUnion {#OutOfLineSandwich1WithOptUnion}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#288)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Sandwich1WithOptUnion'>Sandwich1WithOptUnion</a>&gt;[1]</code>
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

### Regression4 {#Regression4}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#295)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>f1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f2</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>s1</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f3</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f4</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f5</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f6</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich4Align8 {#Sandwich4Align8}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#305)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sandwich4</code></td>
            <td>
                <code><a class='link' href='#Sandwich4'>Sandwich4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>alignment8_enforcement</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich4Align8WithPointer {#Sandwich4Align8WithPointer}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#310)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sandwich4</code></td>
            <td>
                <code><a class='link' href='#Sandwich4'>Sandwich4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>alignment8_enforcement</code></td>
            <td>
                <code><a class='link' href='#Size8Align8'>Size8Align8</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Sandwich9 {#Sandwich9}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#320)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>before</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>the_union</code></td>
            <td>
                <code><a class='link' href='#UnionWithVectorOfVectors'>UnionWithVectorOfVectors</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>after</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SimpleTableArrayStruct {#SimpleTableArrayStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#330)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>the_array</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StringUnionVector {#StringUnionVector}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#334)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>the_vector</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StringUnion'>StringUnion</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LaunchInfo {#LaunchInfo}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#338)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>url</code></td>
            <td>
                <code>string[200]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arguments</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>out</code></td>
            <td>
                <code><a class='link' href='#TransformerEmptyStruct'>TransformerEmptyStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#TransformerEmptyStruct'>TransformerEmptyStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>directory_request</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flat_namespace</code></td>
            <td>
                <code><a class='link' href='#TransformerEmptyStruct'>TransformerEmptyStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>additional_services</code></td>
            <td>
                <code><a class='link' href='#TransformerEmptyStruct'>TransformerEmptyStruct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CreateComponentRequest {#CreateComponentRequest}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#349)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>launch_info</code></td>
            <td>
                <code><a class='link' href='#LaunchInfo'>LaunchInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>controller</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### UnionWithBoundStringStruct {#UnionWithBoundStringStruct}
*Defined in [conformance/union.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/union.test.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>v</code></td>
            <td>
                <code><a class='link' href='#UnionWithBoundString'>UnionWithBoundString</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SingleVariantUnionStruct {#SingleVariantUnionStruct}
*Defined in [conformance/union.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/union.test.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#SingleVariantUnion'>SingleVariantUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ReverseOrdinalUnionStruct {#ReverseOrdinalUnionStruct}
*Defined in [conformance/union.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/union.test.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='#ReverseOrdinalUnion'>ReverseOrdinalUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Int64Struct {#Int64Struct}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#9)*





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

### TestInlineXUnionInStruct {#TestInlineXUnionInStruct}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#32)*





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

### TestOptionalXUnionInStruct {#TestOptionalXUnionInStruct}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#38)*





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

### TestStrictXUnionInStruct {#TestStrictXUnionInStruct}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#44)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#SampleStrictXUnion'>SampleStrictXUnion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TestFlexibleXUnionInStruct {#TestFlexibleXUnionInStruct}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#48)*





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





## **TABLES**

### XUnionInTable {#XUnionInTable}


*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#9)*



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

### TableWithEmptyStruct {#TableWithEmptyStruct}


*Defined in [conformance/optionals.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/optionals.test.fidl#12)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
            </td>
            <td></td>
        </tr></table>

### SimpleTable {#SimpleTable}


*Defined in [conformance/tables.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/tables.test.fidl#7)*



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

### TableWithStringAndVector {#TableWithStringAndVector}


*Defined in [conformance/tables.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/tables.test.fidl#24)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>baz</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>

### Table_StructWithReservedSandwich {#Table_StructWithReservedSandwich}


*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#150)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>s1</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>s2</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr></table>

### Table_StructWithUint32Sandwich {#Table_StructWithUint32Sandwich}


*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#161)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>i</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>s1</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>s2</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>i2</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### Table_UnionWithVector_ReservedSandwich {#Table_UnionWithVector_ReservedSandwich}


*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#172)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>uv</code></td>
            <td>
                <code><a class='link' href='#UnionWithVector'>UnionWithVector</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr></table>

### Table_UnionWithVector_StructSandwich {#Table_UnionWithVector_StructSandwich}


*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#182)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>s1</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>uv</code></td>
            <td>
                <code><a class='link' href='#UnionWithVector'>UnionWithVector</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>s2</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
        </tr></table>

### TransformerSimpleTable {#TransformerSimpleTable}


*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#326)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### IpAddressConfig {#IpAddressConfig}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#21)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>padding_size_24_align_4</code></td>
            <td>
                <code>uint32[6]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dhcp</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### UnionWithEmptyStruct {#UnionWithEmptyStruct}
*Defined in [conformance/optionals.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/optionals.test.fidl#20)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>force_alignment_of_8</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr></table>

### UnionSize8Align4 {#UnionSize8Align4}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#7)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### UnionSize12Align4 {#UnionSize12Align4}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#13)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused3</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant</code></td>
            <td>
                <code>uint8[6]</code>
            </td>
            <td></td>
        </tr></table>

### UnionSize24Align8 {#UnionSize24Align8}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#25)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused3</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant</code></td>
            <td>
                <code><a class='link' href='#StructSize16Align8'>StructSize16Align8</a></code>
            </td>
            <td></td>
        </tr></table>

### UnionSize36Align4 {#UnionSize36Align4}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#56)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused3</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variant</code></td>
            <td>
                <code>uint8[32]</code>
            </td>
            <td></td>
        </tr></table>

### UnionOfUnion {#UnionOfUnion}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#69)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused1</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>size8align4</code></td>
            <td>
                <code><a class='link' href='#UnionSize8Align4'>UnionSize8Align4</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>size12align4</code></td>
            <td>
                <code><a class='link' href='#UnionSize12Align4'>UnionSize12Align4</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>unused2</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>size24align8</code></td>
            <td>
                <code><a class='link' href='#UnionSize24Align8'>UnionSize24Align8</a></code>
            </td>
            <td></td>
        </tr></table>

### UnionWithVector {#UnionWithVector}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#92)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector_of_uint8</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector_s3_a1</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StructSize3Align1'>StructSize3Align1</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector_s3_a2</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#StructSize3Align2'>StructSize3Align2</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>array_s3_a1</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>array_s3_a2</code></td>
            <td>
                <code>[2]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector_union</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#UnionSize8Align4'>UnionSize8Align4</a>&gt;</code>
            </td>
            <td></td>
        </tr></table>

### StringUnion {#StringUnion}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#238)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr></table>

### EmptyStructUnion {#EmptyStructUnion}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#252)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unused</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>es</code></td>
            <td>
                <code><a class='link' href='#TransformerEmptyStruct'>TransformerEmptyStruct</a></code>
            </td>
            <td></td>
        </tr></table>

### UnionWithVectorOfVectors {#UnionWithVectorOfVectors}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#316)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>v</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
        </tr></table>

### UnionWithBoundString {#UnionWithBoundString}
*Defined in [conformance/union.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/union.test.fidl#7)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>boundFiveStr</code></td>
            <td>
                <code>string[5]</code>
            </td>
            <td></td>
        </tr></table>

### SingleVariantUnion {#SingleVariantUnion}
*Defined in [conformance/union.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/union.test.fidl#15)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### ReverseOrdinalUnion {#ReverseOrdinalUnion}
*Defined in [conformance/union.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/union.test.fidl#24)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>z</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr></table>

### SimpleUnion {#SimpleUnion}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#13)*


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
            <td><code>str</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### XUnionWithEmptyStruct {#XUnionWithEmptyStruct}
*Defined in [conformance/optionals.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/optionals.test.fidl#16)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
            </td>
            <td></td>
        </tr></table>

### XUnionWithStruct {#XUnionWithStruct}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#192)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#StructSize3Align1'>StructSize3Align1</a></code>
            </td>
            <td></td>
        </tr></table>

### XUnionWithXUnion {#XUnionWithXUnion}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#200)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#XUnionWithStruct'>XUnionWithStruct</a></code>
            </td>
            <td></td>
        </tr></table>

### XUnionWithUnions {#XUnionWithUnions}
*Defined in [conformance/transformer.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/transformer.test.fidl#208)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>u1</code></td>
            <td>
                <code><a class='link' href='#UnionSize8Align4'>UnionSize8Align4</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>u2</code></td>
            <td>
                <code><a class='link' href='#UnionSize12Align4'>UnionSize12Align4</a></code>
            </td>
            <td></td>
        </tr></table>

### SampleXUnion {#SampleXUnion}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#20)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code>uint32</code>
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

### SampleStrictXUnion {#SampleStrictXUnion}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#26)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code>uint32</code>
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





