Project: /_project.yaml
Book: /_book.yaml

# fuchsia.accessibility.semantics


## **PROTOCOLS**

## SemanticsManager {:#SemanticsManager}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#17)*

 An interface to manage connections with views for the purposes of gathering semantic information
 about their current UI state.

 The manager allows clients to register as a semantic provider for their view(s). In return the
 semantics manager supplies an interface to update, commit and delete information from the
 semantic tree for that view.

### RegisterView {:#RegisterView}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewRef'>ViewRef</a></code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.accessibility.semantics/index.html#SemanticActionListener'>SemanticActionListener</a></code>
            </td>
        </tr><tr>
            <td><code>semantic_tree_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.accessibility.semantics/index.html#SemanticTree'>SemanticTree</a>&gt;</code>
            </td>
        </tr></table>



## SemanticTree {:#SemanticTree}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#28)*

 Interface to update the semantic tree for a particular view. Nodes can be added, updated or
 deleted. Because the size of an update may exceed FIDL transfer limits, clients are responsible
 for breaking up changes into multiple update and delete calls that conform to these limits. The
 commit function must always be called at the end of a full update push to signal the end of an
 update.

### Commit {:#Commit}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### UpdateSemanticNodes {:#UpdateSemanticNodes}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nodes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.accessibility.semantics/index.html#Node'>Node</a>&gt;</code>
            </td>
        </tr></table>



### DeleteSemanticNodes {:#DeleteSemanticNodes}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
        </tr></table>



## SemanticActionListener {:#SemanticActionListener}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#55)*

 A semantic provider is the client-side interface that the manager can use to
 ask clients to perform accessibility actions.

### OnAccessibilityActionRequested {:#OnAccessibilityActionRequested}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='../fuchsia.accessibility.semantics/index.html#Action'>Action</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### HitTest {:#HitTest}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>local_point</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#PointF'>PointF</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.accessibility.semantics/index.html#Hit'>Hit</a></code>
            </td>
        </tr></table>





## **ENUMS**

### Action {:#Action}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#10)*

 Represents actions that can be applied to Nodes. In progress.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Role {:#Role}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#16)*

 Represents a role of an element on an UI. In progress.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Attributes {:#Attributes}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#26)*

 An attribute is an essential property to describe an element. Unlike states,
 attributes define the nature of an element, and a change in one of them
 changes the nature of the element itself.
 Example: a button with a label attribute 'ok', could have its label changed
 to 'cancel', which would alter drastically this element.  In progress.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr></table>

### States {:#States}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#36)*

  A state is a dynamic property of an element that may change in response to
 user action or automated processes. Thus, they are different from attributes
 in an important point, which is frequency of change.
 Example: a checkbox can be checked / unchecked, and this state can be
 altered via user input. In progress.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>checked</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### Node {:#Node}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#46)*

 Node: data structure to represent semantic information about an UI element.

 The Node represents a semantic element on an interface. This may
 be a button, a text field, a checkbox or any element that has a relevant
 semantic meaning so that assistive technology can understand the current UI.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='../fuchsia.accessibility.semantics/index.html#Role'>Role</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>states</code></td>
            <td>
                <code><a class='link' href='../fuchsia.accessibility.semantics/index.html#States'>States</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='../fuchsia.accessibility.semantics/index.html#Attributes'>Attributes</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.accessibility.semantics/index.html#Action'>Action</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>child_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>location</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#BoundingBox'>BoundingBox</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#mat4'>mat4</a></code>
            </td>
            <td></td>
        </tr></table>

### Hit {:#Hit}


*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#42)*

 Results of hit testing on a view's semantic tree which is implemented by
 Runtimes(like Flutter/Chrome) and sent to Accessibility.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>path_from_root</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
        </tr></table>









