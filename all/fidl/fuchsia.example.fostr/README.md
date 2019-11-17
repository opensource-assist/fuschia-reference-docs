[TOC]

# fuchsia.example.fostr




## **STRUCTS**

### MyStruct {#MyStruct}
*Defined in [fuchsia.example.fostr/fostr.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fostr/test/fuchsia.example.fostr/fostr.test.fidl#14)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>nums</code></td>
            <td>
                <code>vector&lt;int32&gt;[10]?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>foo</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bar</code></td>
            <td>
                <code><a class='link' href='#MyXunion'>MyXunion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### ExampleEnum {#ExampleEnum}
Type: <code>uint32</code>

*Defined in [fuchsia.example.fostr/fostr.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fostr/test/fuchsia.example.fostr/fostr.test.fidl#9)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FOO</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>BAR_BAZ</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### SimpleTable {#SimpleTable}


*Defined in [fuchsia.example.fostr/fostr.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fostr/test/fuchsia.example.fostr/fostr.test.fidl#30)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>x</code></td>
            <td>
                <code>bool</code>
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
            <td><code>y</code></td>
            <td>
                <code><a class='link' href='#MyStruct'>MyStruct</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>z</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### MyUnion {#MyUnion}
*Defined in [fuchsia.example.fostr/fostr.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fostr/test/fuchsia.example.fostr/fostr.test.fidl#25)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
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

### MyXunion {#MyXunion}
*Defined in [fuchsia.example.fostr/fostr.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/garnet/public/lib/fostr/test/fuchsia.example.fostr/fostr.test.fidl#20)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>i</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>b</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>



## **BITS**

### ExampleBits {#ExampleBits}
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
        </tr></table>



