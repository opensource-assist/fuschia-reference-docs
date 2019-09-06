Project: /_project.yaml
Book: /_book.yaml

# fuchsia.diagnostics






## **ENUMS**

### PatternMatcher {:#PatternMatcher}
Type: <code>uint32</code>

*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#6)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>WILDCARD</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>GLOB</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### ComponentSelector {:#ComponentSelector}


*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#54)*

 ComponentSelector encodes path to a component that is being selected for.
 The component_hierarchy_path specifies the components or realms that we will
 search for our target component, and target_component_node specifies the
 component within the nodes matched by component_hierarchy_path that we want
 to retrieve as our data source.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>component_hierarchy_path</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PathSelectionNode'>PathSelectionNode</a>&gt;[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>target_component_node</code></td>
            <td>
                <code><a class='link' href='#PathSelectionNode'>PathSelectionNode</a></code>
            </td>
            <td></td>
        </tr></table>





## **XUNIONS**

### PathSelectionNode {:#PathSelectionNode}
*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#44)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>string_pattern</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>pattern_matcher</code></td>
            <td>
                <code><a class='link' href='#PatternMatcher'>PatternMatcher</a></code>
            </td>
            <td></td>
        </tr></table>





