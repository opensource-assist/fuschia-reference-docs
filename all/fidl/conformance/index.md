Project: /_project.yaml
Book: /_book.yaml

# conformance


## **PROTOCOLS**

## EthernetDevice {:#EthernetDevice}
*Defined in [conformance/mix_and_match.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/mix_and_match.test.fidl#19)*




## **STRUCTS**

### StructWithInt {:#StructWithInt}
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

### StructWithArrays {:#StructWithArrays}
*Defined in [conformance/arrays_and_vectors.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/arrays_and_vectors.test.fidl#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>arr_empty</code></td>
            <td>
                <code>int32[0]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
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
            <td><code>arr_struct</code></td>
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

### StructWithVectors {:#StructWithVectors}
*Defined in [conformance/arrays_and_vectors.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/arrays_and_vectors.test.fidl#24)*





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
            <td><code>vec_struct</code></td>
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

### TestXUnionInTable {:#TestXUnionInTable}
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

### InterfaceConfig {:#InterfaceConfig}
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

### TestAddEthernetDeviceRequest {:#TestAddEthernetDeviceRequest}
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

### NodeAttributes {:#NodeAttributes}
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

### FileGetAttrResponse {:#FileGetAttrResponse}
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

### StructWithOptionals {:#StructWithOptionals}
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

### EmptyStruct {:#EmptyStruct}
*Defined in [conformance/structs.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/structs.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### EmptyStructSandwich {:#EmptyStructSandwich}
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

### Uint8Uint16Uint32Uint64 {:#Uint8Uint16Uint32Uint64}
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

### Uint64Uint32Uint16Uint8 {:#Uint64Uint32Uint16Uint8}
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

### StructOfSimpleTable {:#StructOfSimpleTable}
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

### SimpleTableThenUint64 {:#SimpleTableThenUint64}
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

### StructOfTableWithStringAndVector {:#StructOfTableWithStringAndVector}
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

### Int64Struct {:#Int64Struct}
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

### TestInlineXUnionInStruct {:#TestInlineXUnionInStruct}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#27)*





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

### TestOptionalXUnionInStruct {:#TestOptionalXUnionInStruct}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#33)*





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





## **TABLES**

### XUnionInTable {:#XUnionInTable}


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

### TableWithEmptyStruct {:#TableWithEmptyStruct}


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

### SimpleTable {:#SimpleTable}


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

### TableWithStringAndVector {:#TableWithStringAndVector}


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



## **UNIONS**

### IpAddressConfig {:#IpAddressConfig}
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

### UnionWithEmptyStruct {:#UnionWithEmptyStruct}
*Defined in [conformance/optionals.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/optionals.test.fidl#20)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>s2</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a>?</code>
            </td>
            <td></td>
        </tr></table>

### SimpleUnion {:#SimpleUnion}
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
            <td><code>os</code></td>
            <td>
                <code><a class='link' href='#Int64Struct'>Int64Struct</a>?</code>
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

### XUnionWithEmptyStruct {:#XUnionWithEmptyStruct}
*Defined in [conformance/optionals.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/optionals.test.fidl#16)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#EmptyStruct'>EmptyStruct</a></code>
            </td>
            <td></td>
        </tr></table>

### SampleXUnion {:#SampleXUnion}
*Defined in [conformance/xunion.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/tools/fidl/gidl-conformance-suite/xunion.test.fidl#21)*


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





