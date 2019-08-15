Project: /_project.yaml
Book: /_book.yaml

# fuchsia.accessibility.semantics


## **PROTOCOLS**

## SemanticsManager {:#SemanticsManager}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#30)*

 An interface to manage connections with views for the purposes of gathering semantic information
 about their current UI state.

 The manager allows clients to register as a semantic provider for their view(s). In return the
 semantics manager supplies an interface to update, commit and delete information from the
 semantic tree for that view. If the semantic manager encounters an error, it will close the
 channel, delete any associated data and rely on the client to re-register.

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
                <code><a class='link' href='#SemanticActionListener'>SemanticActionListener</a></code>
            </td>
        </tr><tr>
            <td><code>semantic_tree_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#SemanticTree'>SemanticTree</a>&gt;</code>
            </td>
        </tr></table>



### RegisterViewForSemantics {:#RegisterViewForSemantics}


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
                <code><a class='link' href='#SemanticListener'>SemanticListener</a></code>
            </td>
        </tr><tr>
            <td><code>semantic_tree_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#SemanticTree'>SemanticTree</a>&gt;</code>
            </td>
        </tr></table>



## SemanticTree {:#SemanticTree}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#58)*

 Interface to update the semantic tree for a particular view. Nodes can be added, updated or
 deleted. Because the size of an update may exceed FIDL transfer limits, clients are responsible
 for breaking up changes into multiple update and delete calls that conform to these limits. The
 commit function must always be called at the end of a full update push to signal the end of an
 update.

 The client may make several calls to UpdateSemanticNodes(...) or DeleteSemanticNodes(...)
 before calling CommitUpdates(), and must wait for the semantics manager to reply to the
 CommitUpdates() method to know whether an update has been processed. This allows the client to
 break up a set of changes (e.g. a re-computed semantic tree) to the semantic tree into
 FIDL-compatible chunks, but commit them all at once.

 If the semantics manager ever receives inconsistent state from the client, such as an
 invalid tree or unrecognized parent node id, the server will close the channel. The client is
 responsible for reconnecting and re-sending its state from scratch.

### UpdateSemanticNodes {:#UpdateSemanticNodes}

 Sends new/updated nodes to the root to add to the cache on the next commit.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nodes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Node'>Node</a>&gt;[2048]</code>
            </td>
        </tr></table>



### DeleteSemanticNodes {:#DeleteSemanticNodes}

 Tells the root to remove nodes with node_ids from the semantic tree on the next commit.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;[2048]</code>
            </td>
        </tr></table>



### Commit {:#Commit}

 Commits pending changes to node tree associated with the view using UpdateSemanticNodes and
 DeleteSemanticNodes. Commits are processed in the order in which they are sent.
 TODO(MI4-2636): This should be removed after clients move to CommitUpdates().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### CommitUpdates {:#CommitUpdates}

 Commits pending changes to node tree associated with the view using UpdateSemanticNodes and
 DeleteSemanticNodes. Updates are processed in the order in which they are received. If the
 committed updates result in an ill-formed tree (for example a missing root node or a cycle)
 the semantic manager will close the channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SemanticActionListener {:#SemanticActionListener}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#95)*

 A semantic provider is the client-side interface that the manager can use to
 ask clients to perform accessibility actions.

### OnAccessibilityActionRequested {:#OnAccessibilityActionRequested}

 Asks the semantics provider to perform an accessibility action on the
 node with node id in the front-end.

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
                <code><a class='link' href='#Action'>Action</a></code>
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

 Asks the semantics provider to perform hit testing and return the result.

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
                <code><a class='link' href='#Hit'>Hit</a></code>
            </td>
        </tr></table>

## SemanticListener {:#SemanticListener}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#108)*

 A semantic provider is the client-side interface that the manager can use to enable or disable
 semantic updates, and to ask clients to perform accessibility actions.

### OnAccessibilityActionRequested {:#OnAccessibilityActionRequested}

 Asks the semantics provider to perform an accessibility action on the
 node with node id in the front-end.

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
                <code><a class='link' href='#Action'>Action</a></code>
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

 Asks the semantics provider to perform hit testing and return the result.

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
                <code><a class='link' href='#Hit'>Hit</a></code>
            </td>
        </tr></table>

### OnSemanticsModeChanged {:#OnSemanticsModeChanged}

 Callback telling the client whether or not to send updates to the semantic tree.
 The semantics manager will clear all state when this is called with updates_enabled = false.
 When called with updates_enabled = true, the client should sent the full state of the
 current semantic tree.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>updates_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **ENUMS**

### Action {:#Action}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#10)*

 Represents actions that can be applied to Nodes.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### Role {:#Role}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#16)*

 Represents a role of an element on a UI.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Attributes {:#Attributes}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#25)*

 An attribute is an essential property to describe an element. Unlike states, attributes do not
 change over the life of an element.
 Example: A button with a label attribute 'ok' should never change to 'cancel', as this is not
 the same element.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>label</code></td>
            <td>
                <code>string[16384]</code>
            </td>
            <td> The label for an element. If longer than MAX_LABEL_SIZE the client is responsible for
 truncating the label.
</td>
        </tr></table>

### States {:#States}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#36)*

 A state is a dynamic property of an element that may change in response to
 user action or automated processes. Thus, they are different from attributes
 in an important point, which is frequency of change.
 Example: a checkbox can be checked / unchecked, and this state can be
 altered via user input.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>checked</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the element is checked.
</td>
        </tr></table>

### Node {:#Node}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#46)*

 Node: data structure to represent semantic information about a UI element.

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
            <td> Unique ID that represents a node in a particular UI.
 Zero is assumed to be the root node and the only entry point to the tree.
 No forest is allowed.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='#Role'>Role</a></code>
            </td>
            <td> Role of this element, e.g. button, checkbox, etc.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>states</code></td>
            <td>
                <code><a class='link' href='#States'>States</a></code>
            </td>
            <td> A table of states of this object, e.g. checked, editable, etc.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#Attributes'>Attributes</a></code>
            </td>
            <td> A table of attributes of this node.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[100]</code>
            </td>
            <td> A list of actions that can be performed on this node.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>child_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;[256]</code>
            </td>
            <td> The list of child IDs of this node, in traversal order. Runtimes supplying semantic tree
 information are responsible for ensuring the tree does not contain cycles. Each node may
 have only one parent.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>location</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#BoundingBox'>BoundingBox</a></code>
            </td>
            <td> Local bounding box of this element.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/index.html#mat4'>mat4</a></code>
            </td>
            <td> Transform from parent coordinate space to local space.
</td>
        </tr></table>

### Hit {:#Hit}


*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#82)*

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
            <td> Unique ID that represents a node in a particular UI.
 Zero is assumed to be the root node and the only entry point to the tree.
 node_id will not be filled when there is no hit.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>path_from_root</code></td>
            <td>
                <code>vector&lt;uint32&gt;[256]</code>
            </td>
            <td> The ordered list of node ids which represent path from root node to the hit node.
</td>
        </tr></table>









## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#11">MAX_TREE_DEPTH</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#14">MAX_FAN_OUT</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#17">MAX_NODES_PER_UPDATE</a></td>
            <td>
                    <code>2048</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#20">MAX_LABEL_SIZE</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint64</code></td>
        </tr>
    
</table>

