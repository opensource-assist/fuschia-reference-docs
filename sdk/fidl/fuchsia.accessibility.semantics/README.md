[TOC]

# fuchsia.accessibility.semantics


## **PROTOCOLS**

## SemanticsManager {#SemanticsManager}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#33)*

<p>An interface to manage connections with views for the purposes of gathering semantic information
about their current UI state.</p>
<p>The manager allows clients to register as a semantic provider for their view(s). In return the
semantics manager supplies an interface to update, commit and delete information from the
semantic tree for that view. If the semantic manager encounters an error, it will close the
channel, delete any associated data and rely on the client to re-register.</p>

### RegisterViewForSemantics {#RegisterViewForSemantics}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewRef'>ViewRef</a></code>
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



## SemanticTree {#SemanticTree}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#54)*

<p>Interface to update the semantic tree for a particular view. Nodes can be added, updated or
deleted. Because the size of an update may exceed FIDL transfer limits, clients are responsible
for breaking up changes into multiple update and delete calls that conform to these limits. The
commit function must always be called at the end of a full update push to signal the end of an
update.</p>
<p>The client may make several calls to UpdateSemanticNodes(...) or DeleteSemanticNodes(...)
before calling CommitUpdates(), and must wait for the semantics manager to reply to the
CommitUpdates() method to know whether an update has been processed. This allows the client to
break up a set of changes (e.g. a re-computed semantic tree) to the semantic tree into
FIDL-compatible chunks, but commit them all at once.</p>
<p>If the semantics manager ever receives inconsistent state from the client, such as an
invalid tree or unrecognized parent node id, the server will close the channel. The client is
responsible for reconnecting and re-sending its state from scratch.</p>

### UpdateSemanticNodes {#UpdateSemanticNodes}

<p>Sends new/updated nodes to the root to add to the cache on the next commit.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>nodes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Node'>Node</a>&gt;[2048]</code>
            </td>
        </tr></table>



### DeleteSemanticNodes {#DeleteSemanticNodes}

<p>Tells the root to remove nodes with node_ids from the semantic tree on the next commit.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>node_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;[2048]</code>
            </td>
        </tr></table>



### CommitUpdates {#CommitUpdates}

<p>Commits pending changes to node tree associated with the view using UpdateSemanticNodes and
DeleteSemanticNodes. Updates are processed in the order in which they are received. If the
committed updates result in an ill-formed tree (for example a missing root node or a cycle)
the semantic manager will close the channel.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## SemanticListener {#SemanticListener}
*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#83)*

<p>A semantic provider is the client-side interface that the manager can use to enable or disable
semantic updates, and to ask clients to perform accessibility actions.</p>

### OnAccessibilityActionRequested {#OnAccessibilityActionRequested}

<p>Asks the semantics provider to perform an accessibility action on the
node with node id in the front-end.</p>

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

### HitTest {#HitTest}

<p>Asks the semantics provider to perform hit testing and return the result.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>local_point</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/#PointF'>PointF</a></code>
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

### OnSemanticsModeChanged {#OnSemanticsModeChanged}

<p>Callback telling the client whether or not to send updates to the semantic tree.
The semantics manager will clear all state when this is called with updates_enabled = false.
When called with updates_enabled = true, the client should sent the full state of the
current semantic tree.</p>

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

### Action {#Action}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#10)*

<p>Represents actions that can be applied to Nodes.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DEFAULT</code></td>
            <td><code>1</code></td>
            <td><p>The default action associated with the element.</p>
</td>
        </tr><tr>
            <td><code>SECONDARY</code></td>
            <td><code>2</code></td>
            <td><p>The secondary action associated with the element. This may correspond to a long press
(touchscreens) or right click (mouse).</p>
</td>
        </tr><tr>
            <td><code>SET_FOCUS</code></td>
            <td><code>3</code></td>
            <td><p>Set (input/non-accessibility) focus on this element.</p>
</td>
        </tr><tr>
            <td><code>SET_VALUE</code></td>
            <td><code>4</code></td>
            <td><p>Set the element's value.</p>
</td>
        </tr><tr>
            <td><code>SHOW_ON_SCREEN</code></td>
            <td><code>5</code></td>
            <td><p>Scroll node to make it visible.</p>
</td>
        </tr></table>

### Role {#Role}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#25)*

<p>Represents a role of an element on a UI.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td><p>Role used to represent elements which role is not currently supported.</p>
</td>
        </tr><tr>
            <td><code>BUTTON</code></td>
            <td><code>2</code></td>
            <td><p>Something on screen that can be clicked/activated, that has a single function.</p>
</td>
        </tr><tr>
            <td><code>HEADER</code></td>
            <td><code>3</code></td>
            <td><p>Header text, e.g. something tagged <h1> in HTML.</p>
</td>
        </tr><tr>
            <td><code>IMAGE</code></td>
            <td><code>4</code></td>
            <td><p>An image or graphic.</p>
</td>
        </tr><tr>
            <td><code>TEXT_FIELD</code></td>
            <td><code>5</code></td>
            <td><p>A field containing text that is not a header.</p>
</td>
        </tr></table>

### CheckedState {#CheckedState}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#56)*

<p>Represents the state of a UI checkbox.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td><p>Used when no data is entered or the element is not a check box.</p>
</td>
        </tr><tr>
            <td><code>TRUE</code></td>
            <td><code>2</code></td>
            <td><p>True</p>
</td>
        </tr><tr>
            <td><code>FALSE</code></td>
            <td><code>3</code></td>
            <td><p>False</p>
</td>
        </tr><tr>
            <td><code>MIXED</code></td>
            <td><code>4</code></td>
            <td><p>Indeterminate state</p>
</td>
        </tr></table>



## **TABLES**

### Attributes {#Attributes}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#42)*

<p>An attribute is an essential property to describe an element. Unlike states, attributes do not
change over the life of an element.
Example: A button with a label attribute 'ok' should never change to 'cancel', as this is not
the same element.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>label</code></td>
            <td>
                <code>string[16384]</code>
            </td>
            <td><p>The primary label for an element. If longer than MAX_LABEL_SIZE the client is responsible
for truncating the label.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>secondary_label</code></td>
            <td>
                <code>string[16384]</code>
            </td>
            <td><p>The secondary label for an element. If longer than MAX_LABEL_SIZE the client is responsible
for truncating the label.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>secondary_action_description</code></td>
            <td>
                <code>string[16384]</code>
            </td>
            <td><p>A description of what the secondary action on a node (equivalent to long press or right click) should do.</p>
</td>
        </tr></table>

### States {#States}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#70)*

<p>A state is a dynamic property of an element that may change in response to
user action or automated processes. Thus, they are different from attributes
in an important point, which is frequency of change.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>checked</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>DEPRECATED</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>checked_state</code></td>
            <td>
                <code><a class='link' href='#CheckedState'>CheckedState</a></code>
            </td>
            <td><p>State of a checkbox.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>selected</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether the element is currently selected.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>hidden</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether the element is currently hidden or marked invisible by the framework.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>value</code></td>
            <td>
                <code>string[16384]</code>
            </td>
            <td><p>The user-entered value of the element, if applicable. If longer than MAX_VALUE_SIZE the
client is responsible for truncating.</p>
</td>
        </tr></table>

### Node {#Node}


*Defined in [fuchsia.accessibility.semantics/node.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/node.fidl#91)*

<p>The Node represents a semantic element on an interface. This may
be a button, a text field, a checkbox or any element that has a relevant
semantic meaning so that assistive technology can understand the current UI.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Unique ID that represents a node in a particular UI.
Zero is assumed to be the root node and the only entry point to the tree.
No forest is allowed.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>role</code></td>
            <td>
                <code><a class='link' href='#Role'>Role</a></code>
            </td>
            <td><p>Role of this element, e.g. button, checkbox, etc.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>states</code></td>
            <td>
                <code><a class='link' href='#States'>States</a></code>
            </td>
            <td><p>A table of states of this object, e.g. checked, editable, etc.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>attributes</code></td>
            <td>
                <code><a class='link' href='#Attributes'>Attributes</a></code>
            </td>
            <td><p>A table of attributes of this node.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>actions</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Action'>Action</a>&gt;[100]</code>
            </td>
            <td><p>A list of actions that can be performed on this node.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>child_ids</code></td>
            <td>
                <code>vector&lt;uint32&gt;[20000]</code>
            </td>
            <td><p>The list of child IDs of this node, in traversal order. Runtimes supplying semantic tree
information are responsible for ensuring the tree does not contain cycles. Each node may
have only one parent.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>location</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#BoundingBox'>BoundingBox</a></code>
            </td>
            <td><p>Local bounding box of this element.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#mat4'>mat4</a></code>
            </td>
            <td><p>Transform from parent coordinate space to local space. 4x4 for compatibility with scenic.</p>
</td>
        </tr></table>

### Hit {#Hit}


*Defined in [fuchsia.accessibility.semantics/semantics_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#71)*

<p>Results of hit testing on a view's semantic tree which is implemented by
Runtimes(like Flutter/Chrome) and sent to Accessibility.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Unique ID that represents a node in a particular UI.
Zero is assumed to be the root node and the only entry point to the tree.
node_id will not be filled when there is no hit.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>path_from_root</code></td>
            <td>
                <code>vector&lt;uint32&gt;[256]</code>
            </td>
            <td><p>The ordered list of node ids which represent path from root node to the hit node.</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MAX_TREE_DEPTH">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#11">MAX_TREE_DEPTH</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Maximum depth of the semantic tree.</p>
</td>
        </tr>
    <tr id="MAX_FAN_OUT">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#14">MAX_FAN_OUT</a></td>
            <td>
                    <code>20000</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Maximum number of children for a node in the semantic tree.</p>
</td>
        </tr>
    <tr id="MAX_NODES_PER_UPDATE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#17">MAX_NODES_PER_UPDATE</a></td>
            <td>
                    <code>2048</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Maximum number of semantic nodes that may be sent in a single update.</p>
</td>
        </tr>
    <tr id="MAX_LABEL_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#20">MAX_LABEL_SIZE</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Maximum size of a label string, in bytes.</p>
</td>
        </tr>
    <tr id="MAX_VALUE_SIZE">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility.semantics/semantics_manager.fidl#23">MAX_VALUE_SIZE</a></td>
            <td>
                    <code>16384</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>Maximum size of a value string, in bytes.</p>
</td>
        </tr>
    
</table>



