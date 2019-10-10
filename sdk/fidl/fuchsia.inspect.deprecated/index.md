Project: /_project.yaml
Book: /_book.yaml

# fuchsia.inspect.deprecated


## **PROTOCOLS**

## Inspect {:#Inspect}
*Defined in [fuchsia.inspect.deprecated/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#49)*


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
                <code><a class='link' href='#Object'>Object</a></code>
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
                <code>vector&lt;string&gt;[256]</code>
            </td>
        </tr></table>

### OpenChild {:#OpenChild}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
        </tr><tr>
            <td><code>child_channel</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Inspect'>Inspect</a>&gt;</code>
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
*Defined in [fuchsia.inspect.deprecated/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#21)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#PropertyValue'>PropertyValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Metric {:#Metric}
*Defined in [fuchsia.inspect.deprecated/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#34)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>key</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#MetricValue'>MetricValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Object {:#Object}
*Defined in [fuchsia.inspect.deprecated/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#40)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Property'>Property</a>&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Metric'>Metric</a>&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### PropertyValue {:#PropertyValue}
*Defined in [fuchsia.inspect.deprecated/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#15)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>str</code></td>
            <td>
                <code>string[16384]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16384]</code>
            </td>
            <td></td>
        </tr></table>

### MetricValue {:#MetricValue}
*Defined in [fuchsia.inspect.deprecated/inspect.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#27)*


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







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#10">MAX_KEY_LENGTH</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#11">MAX_VALUE_LENGTH</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#12">MAX_VALUE_COUNT</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/zircon/system/fidl/fuchsia-inspect-deprecated/inspect.fidl#13">MAX_CHILDREN_COUNT</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint16</code></td>
            <td></td>
        </tr>
    
</table>

