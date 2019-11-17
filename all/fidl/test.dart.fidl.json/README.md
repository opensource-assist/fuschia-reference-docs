[TOC]

# test.dart.fidl.json




## **STRUCTS**

### ExampleStruct {#ExampleStruct}
*Defined in [test.dart.fidl.json/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/dart_fidl_json/test/fidl/dart.fidl.json.test/types.test.fidl#3)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>structs</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ExampleStruct2'>ExampleStruct2</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vals</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>integers</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ExampleStruct2 {#ExampleStruct2}
*Defined in [test.dart.fidl.json/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/dart_fidl_json/test/fidl/dart.fidl.json.test/types.test.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>baz</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ExampleEnum {#ExampleEnum}
Type: <code>uint32</code>

*Defined in [test.dart.fidl.json/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/dart_fidl_json/test/fidl/dart.fidl.json.test/types.test.fidl#26)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>val1</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>val2</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>val3</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ExampleTable {#ExampleTable}


*Defined in [test.dart.fidl.json/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/dart_fidl_json/test/fidl/dart.fidl.json.test/types.test.fidl#32)*



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
            <td><code></code></td>
            <td>
                <code></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### ExampleUnion {#ExampleUnion}
*Defined in [test.dart.fidl.json/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/dart_fidl_json/test/fidl/dart.fidl.json.test/types.test.fidl#15)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>struct1</code></td>
            <td>
                <code><a class='link' href='#ExampleStruct'>ExampleStruct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>struct2</code></td>
            <td>
                <code><a class='link' href='#ExampleStruct2'>ExampleStruct2</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### ExampleXUnion {#ExampleXUnion}
*Defined in [test.dart.fidl.json/types.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/topaz/bin/dart_fidl_json/test/fidl/dart.fidl.json.test/types.test.fidl#20)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>struct1</code></td>
            <td>
                <code><a class='link' href='#ExampleStruct'>ExampleStruct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>struct2</code></td>
            <td>
                <code><a class='link' href='#ExampleStruct2'>ExampleStruct2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>





