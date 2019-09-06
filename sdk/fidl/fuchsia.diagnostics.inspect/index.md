Project: /_project.yaml
Book: /_book.yaml

# fuchsia.diagnostics.inspect








## **TABLES**

### TreeSelector {:#TreeSelector}


*Defined in [fuchsia.diagnostics.inspect/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/selector.fidl#45)*

 TreeSelector represents a selection request on a nested structure where each
 nested node has properties that can be retrieved. The node_path specifies which
 nodes we search through, and the target_properties specify which properties to
 look for on the matched nodes.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_path</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.diagnostics/index.html'>fuchsia.diagnostics</a>/<a class='link' href='../fuchsia.diagnostics/index.html#PathSelectionNode'>PathSelectionNode</a>&gt;[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>target_properties</code></td>
            <td>
                <code><a class='link' href='#PropertySelector'>PropertySelector</a></code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### PropertySelector {:#PropertySelector}
*Defined in [fuchsia.diagnostics.inspect/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics.inspect/selector.fidl#36)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>string_pattern</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>wildcard</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>





