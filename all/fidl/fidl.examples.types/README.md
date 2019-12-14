[TOC]

# fidl.examples.types


## **PROTOCOLS**

## this_is_a_protocol {#this_is_a_protocol}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#20)*


### Copy {#Copy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>count</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



## **STRUCTS**

### this_is_a_struct {#this_is_a_struct}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#7)*





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

### protocols_and_requests {#protocols_and_requests}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>nonnullable_protocol</code></td>
            <td>
                <code><a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_protocol</code></td>
            <td>
                <code><a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nonnullable_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### primitive_types {#primitive_types}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#31)*





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

### default_values {#default_values}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#45)*





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
            <td>1.3</td>
        </tr><tr>
            <td><code>f64</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
            <td>5.4e-06</td>
        </tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>hello</td>
        </tr>
</table>

### arrays {#arrays}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#63)*





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
                <code>bool[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_1</code></td>
            <td>
                <code>int8[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_1</code></td>
            <td>
                <code>int16[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_1</code></td>
            <td>
                <code>int32[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_1</code></td>
            <td>
                <code>int64[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_1</code></td>
            <td>
                <code>uint8[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_1</code></td>
            <td>
                <code>uint16[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_1</code></td>
            <td>
                <code>uint32[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_1</code></td>
            <td>
                <code>uint64[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_1</code></td>
            <td>
                <code>float32[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_1</code></td>
            <td>
                <code>float64[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_1</code></td>
            <td>
                <code>handle[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_2</code></td>
            <td>
                <code>[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### vectors {#vectors}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#106)*





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
                <code>vector&lt;bool&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_sized_1</code></td>
            <td>
                <code>vector&lt;int8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_sized_1</code></td>
            <td>
                <code>vector&lt;int16&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_sized_1</code></td>
            <td>
                <code>vector&lt;int32&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_sized_1</code></td>
            <td>
                <code>vector&lt;int64&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_sized_1</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_sized_1</code></td>
            <td>
                <code>vector&lt;uint16&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_sized_1</code></td>
            <td>
                <code>vector&lt;uint32&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_sized_1</code></td>
            <td>
                <code>vector&lt;uint64&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_sized_1</code></td>
            <td>
                <code>vector&lt;float32&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_sized_1</code></td>
            <td>
                <code>vector&lt;float64&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_sized_1</code></td>
            <td>
                <code>vector&lt;handle&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]</code>
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
                <code>vector&lt;bool&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int8&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int16&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int32&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;int64&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint16&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint32&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;uint64&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;float32&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;float64&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_nullable_sized_1</code></td>
            <td>
                <code>vector&lt;handle&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>b_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i8_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i16_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i32_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>i64_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u8_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u16_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u32_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>u64_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f32_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>f64_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>handle_nullable_sized_2</code></td>
            <td>
                <code>vector&lt;vector&gt;[32]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### handles {#handles}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#239)*





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
            <td><code>channel_handle</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
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
            <td><code>interrupt_handle</code></td>
            <td>
                <code>handle&lt;interrupt&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>debuglog_handle</code></td>
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
            <td><code>resource_handle</code></td>
            <td>
                <code>handle&lt;resource&gt;</code>
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
            <td><code>guest_handle</code></td>
            <td>
                <code>handle&lt;guest&gt;</code>
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
            <td><code>bti_handle</code></td>
            <td>
                <code>handle&lt;bti&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>profile_handle</code></td>
            <td>
                <code>handle&lt;profile&gt;</code>
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
            <td><code>nullable_debuglog_handle</code></td>
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
            <td><code>nullable_resource_handle</code></td>
            <td>
                <code>handle&lt;resource&gt;?</code>
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
            <td><code>nullable_guest_handle</code></td>
            <td>
                <code>handle&lt;guest&gt;?</code>
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
        </tr><tr>
            <td><code>nullable_bti_handle</code></td>
            <td>
                <code>handle&lt;bti&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_profile_handle</code></td>
            <td>
                <code>handle&lt;profile&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### strings {#strings}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#283)*





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
                <code>string[4]</code>
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
                <code>string[4]?</code>
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

### structs {#structs}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#350)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#this_is_a_struct'>this_is_a_struct</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_s</code></td>
            <td>
                <code><a class='link' href='#this_is_a_struct'>this_is_a_struct</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### unions {#unions}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#355)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code><a class='link' href='#this_is_a_union'>this_is_a_union</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_u</code></td>
            <td>
                <code><a class='link' href='#this_is_a_union'>this_is_a_union</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### xunions {#xunions}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#360)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>xu</code></td>
            <td>
                <code><a class='link' href='#this_is_a_xunion'>this_is_a_xunion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_xu</code></td>
            <td>
                <code><a class='link' href='#this_is_a_xunion'>this_is_a_xunion</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### protocols {#protocols}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#365)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>i</code></td>
            <td>
                <code><a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_i</code></td>
            <td>
                <code><a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### requests {#requests}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#370)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>r</code></td>
            <td>
                <code>request&lt;<a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>nullable_r</code></td>
            <td>
                <code>request&lt;<a class='link' href='#this_is_a_protocol'>this_is_a_protocol</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### default_enum {#default_enum}
Type: <code>uint32</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#292)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### i8_enum {#i8_enum}
Type: <code>int8</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#296)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### i16_enum {#i16_enum}
Type: <code>int16</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#300)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### i32_enum {#i32_enum}
Type: <code>int32</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#304)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### i64_enum {#i64_enum}
Type: <code>int64</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#308)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### u8_enum {#u8_enum}
Type: <code>uint8</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#312)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### u16_enum {#u16_enum}
Type: <code>uint16</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#316)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### u32_enum {#u32_enum}
Type: <code>uint32</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#320)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>

### u64_enum {#u64_enum}
Type: <code>uint64</code>

*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#324)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>x</code></td>
            <td><code>23</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### this_is_a_union {#this_is_a_union}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#11)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### this_is_a_xunion {#this_is_a_xunion}
*Defined in [fidl.examples.types/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#15)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>s</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>



## **BITS**

### default_bits {#default_bits}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>x</td>
            <td>64</td>
            <td></td>
        </tr></table>

### u8_bits {#u8_bits}
Type: <code>uint8</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>x</td>
            <td>1</td>
            <td></td>
        </tr></table>

### u16_bits {#u16_bits}
Type: <code>uint16</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>x</td>
            <td>2</td>
            <td></td>
        </tr><tr>
            <td>y</td>
            <td>4</td>
            <td></td>
        </tr></table>

### u32_bits {#u32_bits}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>x</td>
            <td>8</td>
            <td></td>
        </tr></table>

### u64_bits {#u64_bits}
Type: <code>uint64</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>x</td>
            <td>4611686018427387904</td>
            <td></td>
        </tr><tr>
            <td>y</td>
            <td>9223372036854775808</td>
            <td></td>
        </tr></table>



## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="arrays_size">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#61">arrays_size</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="vectors_size">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#104">vectors_size</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr id="strings_size">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/tools/fidl/examples/types.test.fidl#281">strings_size</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>



