Project: /_project.yaml
Book: /_book.yaml

# fidl.test.compatibility


## **PROTOCOLS**

## Echo {:#Echo}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#536)*


### EchoStruct {:#EchoStruct}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#Struct'>Struct</a></code>
            </td>
        </tr><tr>
            <td><code>forward_to_server</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#Struct'>Struct</a></code>
            </td>
        </tr></table>

### EchoStructNoRetVal {:#EchoStructNoRetVal}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#Struct'>Struct</a></code>
            </td>
        </tr><tr>
            <td><code>forward_to_server</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### EchoEvent {:#EchoEvent}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#Struct'>Struct</a></code>
            </td>
        </tr></table>

### EchoArrays {:#EchoArrays}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#ArraysStruct'>ArraysStruct</a></code>
            </td>
        </tr><tr>
            <td><code>forward_to_server</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#ArraysStruct'>ArraysStruct</a></code>
            </td>
        </tr></table>

### EchoVectors {:#EchoVectors}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#VectorsStruct'>VectorsStruct</a></code>
            </td>
        </tr><tr>
            <td><code>forward_to_server</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#VectorsStruct'>VectorsStruct</a></code>
            </td>
        </tr></table>

### EchoTable {:#EchoTable}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#AllTypesTable'>AllTypesTable</a></code>
            </td>
        </tr><tr>
            <td><code>forward_to_server</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#AllTypesTable'>AllTypesTable</a></code>
            </td>
        </tr></table>

### EchoXunions {:#EchoXunions}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#AllTypesXunion'>AllTypesXunion</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>forward_to_server</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#AllTypesXunion'>AllTypesXunion</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### this_is_a_struct {:#this_is_a_struct}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#7)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### this_is_an_empty_struct {:#this_is_an_empty_struct}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### primitive_types {:#primitive_types}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#28)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
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

### default_values {:#default_values}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#42)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>b1</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr><tr>
            <td><code>b2</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>false</td>
        </tr><tr>
            <td><code>i8</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
            <td>-23</td>
        </tr><tr>
            <td><code>i16</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
            <td>34</td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>-34595</td>
        </tr><tr>
            <td><code>i64</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>3948038</td>
        </tr><tr>
            <td><code>u8</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>0</td>
        </tr><tr>
            <td><code>u16</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
            <td>348</td>
        </tr><tr>
            <td><code>u32</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>9038</td>
        </tr><tr>
            <td><code>u64</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>19835</td>
        </tr><tr>
            <td><code>f32</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>1.30</td>
        </tr><tr>
            <td><code>f64</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>0.0000054</td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>hello</td>
        </tr>
</table>

### arrays {:#arrays}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#62)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>b_0</code></td>
            <td>
                <code>bool[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_0</code></td>
            <td>
                <code>int8[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_0</code></td>
            <td>
                <code>int16[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_0</code></td>
            <td>
                <code>int32[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_0</code></td>
            <td>
                <code>int64[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_0</code></td>
            <td>
                <code>uint8[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_0</code></td>
            <td>
                <code>uint16[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_0</code></td>
            <td>
                <code>uint32[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_0</code></td>
            <td>
                <code>uint64[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_0</code></td>
            <td>
                <code>float32[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_0</code></td>
            <td>
                <code>float64[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_0</code></td>
            <td>
                <code>handle[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_1</code></td>
            <td>
                <code>bool[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_1</code></td>
            <td>
                <code>int8[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_1</code></td>
            <td>
                <code>int16[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_1</code></td>
            <td>
                <code>int32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_1</code></td>
            <td>
                <code>int64[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_1</code></td>
            <td>
                <code>uint8[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_1</code></td>
            <td>
                <code>uint16[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_1</code></td>
            <td>
                <code>uint32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_1</code></td>
            <td>
                <code>uint64[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_1</code></td>
            <td>
                <code>float32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_1</code></td>
            <td>
                <code>float64[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_1</code></td>
            <td>
                <code>handle[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### arrays_2d {:#arrays_2d}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#89)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>b</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_handle</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### vectors {:#vectors}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#108)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>b_0</code></td>
            <td>
                <code>vector&lt;bool&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_0</code></td>
            <td>
                <code>vector&lt;int8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_0</code></td>
            <td>
                <code>vector&lt;int16&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_0</code></td>
            <td>
                <code>vector&lt;int32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_0</code></td>
            <td>
                <code>vector&lt;int64&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_0</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_0</code></td>
            <td>
                <code>vector&lt;uint16&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_0</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_0</code></td>
            <td>
                <code>vector&lt;uint64&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_0</code></td>
            <td>
                <code>vector&lt;float32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_0</code></td>
            <td>
                <code>vector&lt;float64&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_0</code></td>
            <td>
                <code>vector&lt;handle&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_1</code></td>
            <td>
                <code>vector&lt;vector&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_sized_0</code></td>
            <td>
                <code>vector&lt;bool&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_sized_0</code></td>
            <td>
                <code>vector&lt;int8&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_sized_0</code></td>
            <td>
                <code>vector&lt;int16&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_sized_0</code></td>
            <td>
                <code>vector&lt;int32&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_sized_0</code></td>
            <td>
                <code>vector&lt;int64&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_sized_0</code></td>
            <td>
                <code>vector&lt;uint8&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_sized_0</code></td>
            <td>
                <code>vector&lt;uint16&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_sized_0</code></td>
            <td>
                <code>vector&lt;uint32&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_sized_0</code></td>
            <td>
                <code>vector&lt;uint64&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_sized_0</code></td>
            <td>
                <code>vector&lt;float32&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_sized_0</code></td>
            <td>
                <code>vector&lt;float64&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_sized_0</code></td>
            <td>
                <code>vector&lt;handle&gt;[1]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_sized_1</code></td>
            <td>
                <code>vector&lt;bool&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_sized_1</code></td>
            <td>
                <code>vector&lt;int8&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_sized_1</code></td>
            <td>
                <code>vector&lt;int16&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_sized_1</code></td>
            <td>
                <code>vector&lt;int32&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_sized_1</code></td>
            <td>
                <code>vector&lt;int64&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_sized_1</code></td>
            <td>
                <code>vector&lt;uint8&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_sized_1</code></td>
            <td>
                <code>vector&lt;uint16&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_sized_1</code></td>
            <td>
                <code>vector&lt;uint32&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_sized_1</code></td>
            <td>
                <code>vector&lt;uint64&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_sized_1</code></td>
            <td>
                <code>vector&lt;float32&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_sized_1</code></td>
            <td>
                <code>vector&lt;float64&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_sized_1</code></td>
            <td>
                <code>vector&lt;handle&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_nullable_0</code></td>
            <td>
                <code>vector&lt;bool&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_nullable_0</code></td>
            <td>
                <code>vector&lt;int8&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_nullable_0</code></td>
            <td>
                <code>vector&lt;int16&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_nullable_0</code></td>
            <td>
                <code>vector&lt;int32&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_nullable_0</code></td>
            <td>
                <code>vector&lt;int64&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_nullable_0</code></td>
            <td>
                <code>vector&lt;uint8&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_nullable_0</code></td>
            <td>
                <code>vector&lt;uint16&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_nullable_0</code></td>
            <td>
                <code>vector&lt;uint32&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_nullable_0</code></td>
            <td>
                <code>vector&lt;uint64&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_nullable_0</code></td>
            <td>
                <code>vector&lt;float32&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_nullable_0</code></td>
            <td>
                <code>vector&lt;float64&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_nullable_0</code></td>
            <td>
                <code>vector&lt;handle&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_nullable_1</code></td>
            <td>
                <code>vector&lt;vector&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;bool&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;int8&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;int16&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;int32&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;int64&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;uint8&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;uint16&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;uint32&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;uint64&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;float32&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;float64&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_nullable_sized_0</code></td>
            <td>
                <code>vector&lt;handle&gt;[1]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;bool&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int8&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int16&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int32&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int64&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint8&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint16&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint32&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint64&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;float32&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;float64&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;handle&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### handles {:#handles}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#234)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>handle_handle</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>process_handle</code></td>
            <td>
                <code>handle&lt;process&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>thread_handle</code></td>
            <td>
                <code>handle&lt;thread&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmo_handle</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>event_handle</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>port_handle</code></td>
            <td>
                <code>handle&lt;port&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>log_handle</code></td>
            <td>
                <code>handle&lt;debuglog&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>socket_handle</code></td>
            <td>
                <code>handle&lt;socket&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>eventpair_handle</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>job_handle</code></td>
            <td>
                <code>handle&lt;job&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vmar_handle</code></td>
            <td>
                <code>handle&lt;vmar&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>fifo_handle</code></td>
            <td>
                <code>handle&lt;fifo&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>timer_handle</code></td>
            <td>
                <code>handle&lt;timer&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_handle_handle</code></td>
            <td>
                <code>handle&lt;handle&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_process_handle</code></td>
            <td>
                <code>handle&lt;process&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_thread_handle</code></td>
            <td>
                <code>handle&lt;thread&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_vmo_handle</code></td>
            <td>
                <code>handle&lt;vmo&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_channel_handle</code></td>
            <td>
                <code>handle&lt;channel&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_event_handle</code></td>
            <td>
                <code>handle&lt;event&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_port_handle</code></td>
            <td>
                <code>handle&lt;port&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_interrupt_handle</code></td>
            <td>
                <code>handle&lt;interrupt&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_log_handle</code></td>
            <td>
                <code>handle&lt;debuglog&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_socket_handle</code></td>
            <td>
                <code>handle&lt;socket&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_eventpair_handle</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_job_handle</code></td>
            <td>
                <code>handle&lt;job&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_vmar_handle</code></td>
            <td>
                <code>handle&lt;vmar&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_fifo_handle</code></td>
            <td>
                <code>handle&lt;fifo&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_timer_handle</code></td>
            <td>
                <code>handle&lt;timer&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### strings {:#strings}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#268)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_s</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>size_0_s</code></td>
            <td>
                <code>string[2]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>size_1_s</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_size_0_s</code></td>
            <td>
                <code>string[2]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_size_1_s</code></td>
            <td>
                <code>string[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### structs {:#structs}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#384)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_struct'>this_is_a_struct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_s</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_struct'>this_is_a_struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>es</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_an_empty_struct'>this_is_an_empty_struct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### unions {:#unions}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#390)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>u</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_union'>this_is_a_union</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_u</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_union'>this_is_a_union</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Struct {:#Struct}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#396)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>primitive_types</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#primitive_types'>primitive_types</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>default_values</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#default_values'>default_values</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arrays</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#arrays'>arrays</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arrays_2d</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#arrays_2d'>arrays_2d</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vectors</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#vectors'>vectors</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#handles'>handles</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>strings</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#strings'>strings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>default_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#default_enum'>default_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#i8_enum'>i8_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#i16_enum'>i16_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#i32_enum'>i32_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#i64_enum'>i64_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u8_enum'>u8_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u16_enum'>u16_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u32_enum'>u32_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_enum</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u64_enum'>u64_enum</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>default_bits</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#default_bits'>default_bits</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_bits</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u8_bits'>u8_bits</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_bits</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u16_bits'>u16_bits</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_bits</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u32_bits'>u32_bits</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_bits</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#u64_bits'>u64_bits</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>structs</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#structs'>structs</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>unions</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#unions'>unions</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_table'>this_is_a_table</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xunion</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_xunion'>this_is_a_xunion</a></code>
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
        </tr>
</table>

### ArraysStruct {:#ArraysStruct}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#426)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bools</code></td>
            <td>
                <code>bool[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int8s</code></td>
            <td>
                <code>int8[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int16s</code></td>
            <td>
                <code>int16[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int32s</code></td>
            <td>
                <code>int32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int64s</code></td>
            <td>
                <code>int64[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint8s</code></td>
            <td>
                <code>uint8[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint16s</code></td>
            <td>
                <code>uint16[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint32s</code></td>
            <td>
                <code>uint32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint64s</code></td>
            <td>
                <code>uint64[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>float32s</code></td>
            <td>
                <code>float32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>float64s</code></td>
            <td>
                <code>float64[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enums</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bits</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>handle[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_handles</code></td>
            <td>
                <code>handle[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>strings</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_strings</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>structs</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_structs</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>unions</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_unions</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arrays</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vectors</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_vectors</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tables</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xunions</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VectorsStruct {:#VectorsStruct}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#456)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bools</code></td>
            <td>
                <code>vector&lt;bool&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int8s</code></td>
            <td>
                <code>vector&lt;int8&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int16s</code></td>
            <td>
                <code>vector&lt;int16&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int32s</code></td>
            <td>
                <code>vector&lt;int32&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>int64s</code></td>
            <td>
                <code>vector&lt;int64&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint8s</code></td>
            <td>
                <code>vector&lt;uint8&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint16s</code></td>
            <td>
                <code>vector&lt;uint16&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint32s</code></td>
            <td>
                <code>vector&lt;uint32&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>uint64s</code></td>
            <td>
                <code>vector&lt;uint64&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>float32s</code></td>
            <td>
                <code>vector&lt;float32&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>float64s</code></td>
            <td>
                <code>vector&lt;float64&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enums</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#default_enum'>default_enum</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bits</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#default_bits'>default_bits</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_handles</code></td>
            <td>
                <code>vector&lt;handle&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>strings</code></td>
            <td>
                <code>vector&lt;string&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_strings</code></td>
            <td>
                <code>vector&lt;string&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>structs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#this_is_a_struct'>this_is_a_struct</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_structs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#this_is_a_struct'>this_is_a_struct</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>unions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#this_is_a_union'>this_is_a_union</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_unions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#this_is_a_union'>this_is_a_union</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>arrays</code></td>
            <td>
                <code>vector&lt;array&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vectors</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_vectors</code></td>
            <td>
                <code>vector&lt;vector&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tables</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#this_is_a_table'>this_is_a_table</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>xunions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fidl.test.compatibility/index.html#this_is_a_xunion'>this_is_a_xunion</a>&gt;[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### default_enum {:#default_enum}
Type: <code>uint32</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#277)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kZero</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### i8_enum {:#i8_enum}
Type: <code>int8</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#282)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kNegativeOne</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### i16_enum {:#i16_enum}
Type: <code>int16</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#287)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kNegativeOne</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kTwo</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### i32_enum {:#i32_enum}
Type: <code>int32</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#293)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kNegativeOne</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kTwo</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>kThree</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### i64_enum {:#i64_enum}
Type: <code>int64</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#300)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kNegativeOne</code></td>
            <td><code>-1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kTwo</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>kThree</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFour</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### u8_enum {:#u8_enum}
Type: <code>uint8</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#308)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kTwo</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>kThree</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFour</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFive</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### u16_enum {:#u16_enum}
Type: <code>uint16</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#316)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kTwo</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>kThree</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFour</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFive</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>kSix</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>

### u32_enum {:#u32_enum}
Type: <code>uint32</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#325)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kTwo</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>kThree</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFour</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFive</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>kSix</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>kSeven</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### u64_enum {:#u64_enum}
Type: <code>uint64</code>

*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#335)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kOne</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kTwo</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>kThree</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFour</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFive</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>kSix</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>kSeven</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>kEight</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### this_is_a_table {:#this_is_a_table}


*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#19)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### AllTypesTable {:#AllTypesTable}


*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#486)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>bool_member</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>int8_member</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>int16_member</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>int32_member</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>int64_member</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>uint8_member</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>uint16_member</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>uint32_member</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>9</td>
            <td><code>uint64_member</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>10</td>
            <td><code>float32_member</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>11</td>
            <td><code>float64_member</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>12</td>
            <td><code>enum_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#default_enum'>default_enum</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>13</td>
            <td><code>bits_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#default_bits'>default_bits</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>14</td>
            <td><code>handle_member</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>15</td>
            <td><code>string_member</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>16</td>
            <td><code>struct_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_struct'>this_is_a_struct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>17</td>
            <td><code>union_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_union'>this_is_a_union</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>18</td>
            <td><code>array_member</code></td>
            <td>
                <code>uint32[3]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>19</td>
            <td><code>vector_member</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>20</td>
            <td><code>table_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_table'>this_is_a_table</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>21</td>
            <td><code>xunion_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_xunion'>this_is_a_xunion</a></code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### this_is_a_union {:#this_is_a_union}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#14)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### this_is_a_xunion {:#this_is_a_xunion}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#23)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### AllTypesXunion {:#AllTypesXunion}
*Defined in [fidl.test.compatibility/compatibility_service.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#511)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>bool_member</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>int8_member</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>int16_member</code></td>
            <td>
                <code>int16</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>int32_member</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>int64_member</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint8_member</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint16_member</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint32_member</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint64_member</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>float32_member</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>float64_member</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>enum_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#default_enum'>default_enum</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bits_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#default_bits'>default_bits</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>handle_member</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>string_member</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>struct_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_struct'>this_is_a_struct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>union_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_union'>this_is_a_union</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>array_member</code></td>
            <td>
                <code>uint32[3]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector_member</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>table_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_table'>this_is_a_table</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>xunion_member</code></td>
            <td>
                <code><a class='link' href='../fidl.test.compatibility/index.html#this_is_a_xunion'>this_is_a_xunion</a></code>
            </td>
            <td></td>
        </tr></table>



## **BITS**
### default_bits {:#default_bits}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>kOne</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>kTwo</td>
            <td>2</td>
            <td></td>
        </tr></table>### u8_bits {:#u8_bits}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>kOne</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>kTwo</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>kThree</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>kFour</td>
            <td>8</td>
            <td></td>
        </tr><tr>
            <td>kFive</td>
            <td>16</td>
            <td></td>
        </tr></table>### u16_bits {:#u16_bits}
Type: <code>uint16</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>kOne</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>kTwo</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>kThree</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>kFour</td>
            <td>8</td>
            <td></td>
        </tr><tr>
            <td>kFive</td>
            <td>16</td>
            <td></td>
        </tr><tr>
            <td>kSix</td>
            <td>32</td>
            <td></td>
        </tr></table>### u32_bits {:#u32_bits}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>kOne</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>kTwo</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>kThree</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>kFour</td>
            <td>8</td>
            <td></td>
        </tr><tr>
            <td>kFive</td>
            <td>16</td>
            <td></td>
        </tr><tr>
            <td>kSix</td>
            <td>32</td>
            <td></td>
        </tr><tr>
            <td>kSeven</td>
            <td>64</td>
            <td></td>
        </tr></table>### u64_bits {:#u64_bits}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>kOne</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>kTwo</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>kThree</td>
            <td>4</td>
            <td></td>
        </tr><tr>
            <td>kFour</td>
            <td>8</td>
            <td></td>
        </tr><tr>
            <td>kFive</td>
            <td>16</td>
            <td></td>
        </tr><tr>
            <td>kSix</td>
            <td>32</td>
            <td></td>
        </tr><tr>
            <td>kSeven</td>
            <td>64</td>
            <td></td>
        </tr><tr>
            <td>kEight</td>
            <td>128</td>
            <td></td>
        </tr></table>



## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#60">arrays_size</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#106">vectors_size</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fidl/compatibility_test/compatibility_service.test.fidl#266">strings_size</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

