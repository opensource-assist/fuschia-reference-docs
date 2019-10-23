[TOC]

# fuchsia.data




## **STRUCTS**

### Vector {#Vector}
*Defined in [fuchsia.data/data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.data/data.fidl#19)*



 A vector is a sequence of values.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Value'>Value</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Dictionary {#Dictionary}
*Defined in [fuchsia.data/data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.data/data.fidl#25)*



 A dictionary is a sequence of key/value pairs.
 Keys must be unique and sorted in lexicographically increasing order.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>entries</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Entry'>Entry</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Entry {#Entry}
*Defined in [fuchsia.data/data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.data/data.fidl#30)*



 A key/value pair in a `Dictionary`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Value {#Value}
*Defined in [fuchsia.data/data.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.data/data.fidl#8)*

 A value is a boolean, integer, float, string, vector, or dictionary.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>bit</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>inum</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>fnum</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>str</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vec</code></td>
            <td>
                <code><a class='link' href='#Vector'>Vector</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>dict</code></td>
            <td>
                <code><a class='link' href='#Dictionary'>Dictionary</a></code>
            </td>
            <td></td>
        </tr></table>







