[TOC]

# fuchsia.ledger.testing




## **STRUCTS**

### TestMessage2 {#TestMessage2}
*Defined in [fuchsia.ledger.testing/testing.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/lib/encoding/testing.test.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>test_enum</code></td>
            <td>
                <code>[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### TestEnum {#TestEnum}
Type: <code>uint32</code>

*Defined in [fuchsia.ledger.testing/testing.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/lib/encoding/testing.test.fidl#13)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>A</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>B</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>C</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### TestMessage1 {#TestMessage1}


*Defined in [fuchsia.ledger.testing/testing.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/lib/encoding/testing.test.fidl#9)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16]</code>
            </td>
            <td></td>
        </tr></table>

### TestStruct {#TestStruct}


*Defined in [fuchsia.ledger.testing/testing.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/lib/encoding/testing.test.fidl#29)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>some_string</code></td>
            <td>
                <code>string[32]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>some_int</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>some_float</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>test_union</code></td>
            <td>
                <code><a class='link' href='#TestUnion'>TestUnion</a></code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### TestUnion {#TestUnion}
*Defined in [fuchsia.ledger.testing/testing.test.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/ledger/lib/encoding/testing.test.fidl#23)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>message_1</code></td>
            <td>
                <code><a class='link' href='#TestMessage1'>TestMessage1</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>message_2</code></td>
            <td>
                <code><a class='link' href='#TestMessage2'>TestMessage2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>message_3</code></td>
            <td>
                <code>string[35]</code>
            </td>
            <td></td>
        </tr></table>





