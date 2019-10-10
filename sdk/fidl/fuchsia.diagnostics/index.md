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


*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#52)*

 ComponentSelector encodes path to a component that is being selected for.
 The `component_moniker` specifies a pattern of component absolute monikers which
 identify components being selected for.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>component_moniker</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#PathSelectionNode'>PathSelectionNode</a>&gt;[1024]</code>
            </td>
            <td> Vector encoding the absolute moniker of a component being selected for.

 There must be at least one path selection node provided, which
 specifies the component names that are matched by
 the current selector. With only the component name
 present, we treat the `component_moniker` as selecting for all monikers
 that end in the specified name.
</td>
        </tr></table>





## **XUNIONS**

### PathSelectionNode {:#PathSelectionNode}
*Defined in [fuchsia.diagnostics/selector.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.diagnostics/selector.fidl#44)*

 The set of states that a selection node can exist in. A selection-node
 is a matcher of a container in a nested hierarchy, such as
 a match of nested components at a location in the component hierarchy
 or a match of nodes in an Inspect tree.

 string_pattern: This is a provided string that defines a pattern to
   match against at the current location in a nested hierarchy. The
   parser treats wildcards (*) and backslashes (\) as special characters.
   If you wish to match against literal wildcards, it must be escaped.
   If you wish to match against literal backslashes, they must be escaped.

   eg: <curr_node>/abc will match any node contained within curr_node
       with the exact name "abc".
   eg: <curr_node>/a\* will match any node contained within curr_node
       with the exact name "a*".
   eg: <curr_node>/a\\* will match any node contained within curr_node
       that starts with exactly "a\".
   eg: <curr_node>/a* will match any node contained within curr_node
       that starts with "a".
   eg: <curr_node>/a*b will match any node contained within curr_node
       that starts with a and ends with b.
   eg: <curr_node>/*b will match any node contained within curr_node
       that ends with b.

 pattern_matcher: This is either a wild-card or a glob.

   wildcard: will match all nodes at the current location in the
      component hierarchy. These PathSelectionNode types are a result of the
      only text provided in the selector-node spot being an escaped star.

   glob: will match all nodes at or below the current location in the
      component hierarchy. These PathSelectionNode types are a result of
      the only text provided in the selector-node spot being two escaped stars.

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





