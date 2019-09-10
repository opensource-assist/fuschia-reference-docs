Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.scenic.internal


## **PROTOCOLS**

## Flatland {:#Flatland}
*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#13)*

 All functions in this protocol are feed-forward.
 They are not executed until Present() is called.

### Present {:#Present}

 Execute all feed-forward operations.

 If executing a command produces an error (e.g., CreateTransform(0)), Present() will return
 an error. Commands that produce errors are ignored. Future commands are still executed.

 TODO(36166): Present should stop execution, and kill the channel, when some errors are
 detected.

 The client may only Present() a fixed number of times before it must wait for this function
 to return. This number or presents remaining is the return value of this method. The number of /// presents remaining will never drop without a corresponding call to Present() by the client,
 however, it may stay the same, or even increase, with each call to Present().

 num_presents_remaining will always be >= 1

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
 in the linked parent Graph (see LinkGraph()). Any parents of the Root Transform in this
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

*Defined in [fuchsia.ui.scenic.internal/flatland.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.scenic.internal/flatland.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BAD_OPERATION</code></td>
            <td><code>0</code></td>
            <td></td>
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







