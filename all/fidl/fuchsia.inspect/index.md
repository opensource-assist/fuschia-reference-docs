Project: /_project.yaml
Book: /_book.yaml

# fuchsia.inspect


## **PROTOCOLS**

## Inspect {:#Inspect}
*Defined in [fuchsia.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/inspect.fidl#41)*


### ReadData {:#ReadData}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>object</code></td>
            <td>
                <code><a class='link' href='../fuchsia.inspect/index.html#Object'>Object</a></code>
            </td>
        </tr></table>

### ListChildren {:#ListChildren}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>children_names</code></td>
            <td>
                <code>vector&lt;string&gt;?</code>
            </td>
        </tr></table>

### OpenChild {:#OpenChild}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr><tr>
            <td><code>child_channel</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.inspect/index.html#Inspect'>Inspect</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## **STRUCTS**

### Property {:#Property}
*Defined in [fuchsia.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/inspect.fidl#13)*





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
                <code><a class='link' href='../fuchsia.inspect/index.html#PropertyValue'>PropertyValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Metric {:#Metric}
*Defined in [fuchsia.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/inspect.fidl#26)*





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
                <code><a class='link' href='../fuchsia.inspect/index.html#MetricValue'>MetricValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Object {:#Object}
*Defined in [fuchsia.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/inspect.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.inspect/index.html#Property'>Property</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.inspect/index.html#Metric'>Metric</a>&gt;?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### PropertyValue {:#PropertyValue}
*Defined in [fuchsia.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/inspect.fidl#7)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>str</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>

### MetricValue {:#MetricValue}
*Defined in [fuchsia.inspect/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect/inspect.fidl#19)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>int_value</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint_value</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>double_value</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr></table>







