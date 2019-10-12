Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.scenic.internal


## **PROTOCOLS**

## GraphLink {:#GraphLink}
*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#34)*

 A protocol that provides information about a particular Link to the child client. Each Flatland
 instance may only specify a single root transform, so other objects in the graph can only be 
 children of a single GraphLink. However, more than one GraphLink protocol may be active at a
 time for a particular Flatland instance. Specifically, when a Flatland instance is transitioning
 from using one Link to another, each Link will have a separate protocol instance, and more than
 one protocol may receive certain updates.

### GetLayout {:#GetLayout}

 A hanging get for receiving layout information. Clients may receive layout information
 before the GraphLink operation has been presented. This allows children to layout their
 content before their first call to Present(). In transition cases where two GraphLink
 channels exist at the same time, both protocol instances will be receiving different layout
 information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='#LayoutInfo'>LayoutInfo</a></code>
            </td>
        </tr></table>

## ContentLink {:#ContentLink}
*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#52)*

 A protocol that provides information about a particular Link to the parent client. Flatland
 instances may contain any number of ContentLinks, each of which may or may not be attached to
 the Root Transform. Each ContentLink has its own protocol instance.

### GetStatus {:#GetStatus}

 A hanging get for receiving the status of a Link. This provides information to the parent,
 such as whether or not the child has successfully presented content through this Link.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#ContentLinkStatus'>ContentLinkStatus</a></code>
            </td>
        </tr></table>

## Flatland {:#Flatland}
*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#94)*

 Each Flatland instance contains a Graph, which consists of a set of objects, and the
 relationships between those objects. The client can specify a subset of those objects
 (specifically, the directed acyclic graph starting at the root transform) to be presented as
 content to some kind of output -- usually, a display.

 Flatland Graphs are both hierarchical, and distributed. Graphs from different Flatland instances
 may be linked together, allowing multiple processes to be involved in authoring content for a
 particular output.

 All functions in this protocol are feed-forward. The operations they represent are not fully
 executed until Present() is called.

### Present {:#Present}

 Complete execution of all feed-forward operations.

 If executing an operation produces an error (e.g., CreateTransform(0)), Present() will
 return an error. Operations that produce errors are ignored. Future operations are still
 executed.

 TODO(36166): Present should stop execution, and kill the channel, when irrecoverable errors
 are detected.

 The client may only call Present() a certain number of times before it must wait for this
 function to return. This number or presents remaining is the return value of this function.
 The number of presents remaining will never drop without a corresponding call to Present()
 by the client. However, it may stay the same, or even increase, with each return from
 Present().

 num_presents_remaining will always be >= 1. Present() will not return until the client is
 allowed to call Present() again.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Flatland_Present_Result'>Flatland_Present_Result</a></code>
            </td>
        </tr></table>

### LinkToParent {:#LinkToParent}

 A Link is a connection between the objects authored in this Graph, and the objects in
 the Graph of another process. The parent process has control over how the linked content is
 integrated into their Graph.

 A link is formed by creating an event pair, passing one end to the parent (which calls
 CreateLink()) and the other end to the child (which calls LinkToParent()).

 Only nodes connected to the Root Transform in this Flatland instance will be rendered as
 part of the parent's Graph.

 Calling LinkToParent() a second time will disconnect the Root Transform from the existing
 parent's Graph, and attach it to a new parent's Graph.

 This function is feed-forward, meaning that the Root Transform will not be attached to the
 parent Graph until Present() is called. However, Clients will receive information through
 their GraphLinkListener (e.g., LayoutInfo) immediately after calling this function, even if
 they have not called Present() or SetRoot(). This allows clients to wait for layout
 information from their parent before calling Present(), if they wish.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#GraphLinkToken'>GraphLinkToken</a></code>
            </td>
        </tr><tr>
            <td><code>graph_link</code></td>
            <td>
                <code>request&lt;<a class='link' href='#GraphLink'>GraphLink</a>&gt;</code>
            </td>
        </tr></table>



### ClearGraph {:#ClearGraph}

 This function will reset all state on this interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### CreateTransform {:#CreateTransform}

 Creates a new Transform node. Transforms are a hierarchical piece of a Flatland graph. They
 can have children, and can reference Content. A sub-graph represented by a Transform and its
 descendants can be rendered to a display.

 Transforms are kept alive, even when released, as long as they are children of either an
 unreleased Transform, or the Root Transform.

 Each Transform can have a single piece of attached Content. Common types of Content include
 bitmaps, asynchronous streams of images, and links to Transforms in other processes.

 Transforms have attributes. Child Transforms inherit the combined attributes of their
 parents. Content attached to a Transform is also affected by that Transform's attributes.

 When a sub-graph of Transforms is rendered, Content will be rendered back-to-front, starting
 with the Content on the root transform, and continuing recursively through all of its child
 Transforms in the order the children were added. See AddChild() for more information.

 Zero is not a valid transform id. All other values are valid, assuming they are not already
 in use (see ReleaseTransform() for more details).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>transform_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### AddChild {:#AddChild}

 Adds a child Transform to a parent Transform. The new child Transform, and any Content
 attached to it or its children, will be rendered on top of the parent’s Content, as well as
 any previously added children.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>parent_transform_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>child_transform_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### RemoveChild {:#RemoveChild}

 Removes a child Transform from a parent Transform.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>parent_transform_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>child_transform_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### SetRootTransform {:#SetRootTransform}

 Sets the Root Transform for the graph.

 The sub-graph defined by the Root Transform and its children will be rendered as Content
 in the linked parent Graph (see LinkToParent()). Any parents of the Root Transform in this
 Graph will be ignored.

 The Root Transform, and all children of the Root Transform, are kept alive if they are
 released (see ReleaseTransform() for more details).

 There is only ever one Root. Since 0 is not a valid transform id (see CreateTransform()),
 calling SetRootTransform(0) clears the current Root, destroying any previously released
 objects that are not referenced by the new root.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>transform_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CreateLink {:#CreateLink}

 A Link is a connection between the objects authored in this Graph, and the objects in
 another process. The parent process has control over how the linked content is integrated
 into their Graph through this Link object, and the object's associated Link properties.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>link_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#ContentLinkToken'>ContentLinkToken</a></code>
            </td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#LinkProperties'>LinkProperties</a></code>
            </td>
        </tr><tr>
            <td><code>content_link</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ContentLink'>ContentLink</a>&gt;</code>
            </td>
        </tr></table>



### SetLinkProperties {:#SetLinkProperties}

 Transforms are usually sufficient to change how content is presented. Links, however, have
 special properties that are not part of the Transform hierarchy. Those properties can be set
 using this function.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>link_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#LinkProperties'>LinkProperties</a></code>
            </td>
        </tr></table>



### ReleaseTransform {:#ReleaseTransform}

 Released Transforms and Content will be garbage collected by the system once they are no
 longer necessary for rendering (i.e., there is no path from the Root Transform to the
 object, all pending rendering has completed, and new Content is available).

 However, once released, the id immediately goes out of scope for future function calls, and
 can be reused by the client when creating new Transforms and Content.

 It is an error to call Graph functions on a released id (unless that id has been reused to
 construct a new object).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>transform_id</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## Snapshot {:#Snapshot}
*Defined in [fuchsia.ui.scenic.internal/snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/snapshot.fidl#20)*

 Defines an internal interface to take snapshots of the entire scene graph. This
 is only to be used by trusted clients.

### TakeSnapshot {:#TakeSnapshot}

 Takes a snapshot of the entire scene-graph, starting with the first
 compositor found. A separate buffer is returned for each compositor,
 with an empty array being returned if no compositors were found at all.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>snapshots</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SnapshotResult'>SnapshotResult</a>&gt;</code>
            </td>
        </tr></table>



## **STRUCTS**

### Flatland_Present_Response {:#Flatland_Present_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>num_presents_remaining</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Vec2 {:#Vec2}
*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#13)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### GraphLinkToken {:#GraphLinkToken}
*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#59)*



 A typed wrapper for an eventpair, representing the child endpoint of a Link.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ContentLinkToken {:#ContentLinkToken}
*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#64)*



 A typed wrapper for an eventpair, representing the parent endpoint of a Link.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SnapshotResult {:#SnapshotResult}
*Defined in [fuchsia.ui.scenic.internal/snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/snapshot.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### Error {:#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#8)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BAD_OPERATION</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### ContentLinkStatus {:#ContentLinkStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#43)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONTENT_HAS_PRESENTED</code></td>
            <td><code>0</code></td>
            <td> The underlying Graph has connected its Link, called Present(), and the acquisition fences of
 the Present() call have all be reached.
</td>
        </tr></table>



## **TABLES**

### LayoutInfo {:#LayoutInfo}


*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#22)*

 The return type of GraphLink::GetLayout(). This table contains most of the information necessary
 for a client to decide how to layout their content in a Flatland instance. This data may be
 provided to the client before the command that creates the Link is presented, so that the client
 may lay out content properly before their first call to Present().


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>logical_size</code></td>
            <td>
                <code><a class='link' href='#Vec2'>Vec2</a></code>
            </td>
            <td> The layout size of a Graph in logical pixels, defined by the parent’s call to
 SetLinkProperties(). Clients should re-layout their content when this value changes.
</td>
        </tr></table>

### LinkProperties {:#LinkProperties}


*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#70)*

 The properties of a Link as defined by the parent. This data, along with the set of attached
 Transforms, will be used to compute the LayoutInfo for the child of the Link.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>logical_size</code></td>
            <td>
                <code><a class='link' href='#Vec2'>Vec2</a></code>
            </td>
            <td> The size of the Link in logical pixels. This maps directly to the logical_size field in
 LayoutInfo.
</td>
        </tr></table>



## **UNIONS**

### Flatland_Present_Result {:#Flatland_Present_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Flatland_Present_Response'>Flatland_Present_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







