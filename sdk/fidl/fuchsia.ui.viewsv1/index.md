Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.viewsv1


## **PROTOCOLS**

## ViewContainer {:#ViewContainer}
*Defined in [fuchsia.ui.viewsv1/view_containers.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_containers.fidl#49)*

 A view container is an interface exposed by `View` and `ViewTree` to
 manage their child views.  Although `View` may have any number of children,
 a `ViewTree` can have at most one (its root view).

 EMBEDDING

 The following steps are required to embed another view as a child:

 1. Obtain the `ViewOwner` belonging to the view you would like to embed.
    The means for doing this is not specified by the view system.
    You might create another view of your own to embed or connect to
    another application using a mechanism such as `ViewProvider` (or
    any suitable agreed-upon protocol) to create the view to embed.

 2. Call `AddChild()` to add the view you would like to embed and assign
    it a unique key.

 3. Call `SetChildProperties()` to provide layout parameters and other
    properties for the new child using the same key that was provided
    to `AddChild()`.

 4. Watch for the child becoming unavailable, as reported by
    `OnChildUnavailable()`, which indicates that the child is no longer
    in a usable state (perhaps the application which provided it has
    stopped).  When this happens, you are still responsible for calling
    `RemoveChild()` to remove the child and discard any state that your
    view has associated with it.

 VIEW PROPERTIES AND LAYOUT

 The container controls the presentation of its children by setting
 `ViewProperties` for each of them.  View properties include layout
 information and other parameters the child needs to know to participate
 in the view hierarchy.

 The container must set properties for each of its children after adding
 them, as otherwise the children cannot be rendered (since they lack enough
 context to know what to draw).

### SetListener {:#SetListener}

 Sets the view container listener, or null to remove.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#ViewContainerListener'>ViewContainerListener</a>?</code>
            </td>
        </tr></table>



### AddChild {:#AddChild}

 Adds the view referenced by `child_view_owner` as a child and assigns
 it the provided `child_key` to identify it among its children.
 The container may remove the child later by passing the same `child_key`
 to `RemoveChild()`.

 This method takes ownership of the view.

 It is important for the container to choose locally unique values for
 `child_key` to ensure that each child can be distinguished even as
 more children are added or removed.  We recommend using a simple
 counter which is incremented on each (re-)addition.

 If the child becomes unavailable at any time prior to being removed
 then an `OnChildUnavailable()` message will be sent.

 If `child_view_owner` refers to a view which is already unavailable or
 if adding the view would create a cycle in the view tree then the
 call proceeds as if it succeeded but an `OnChildUnavailable()` message
 will be sent.

 If `child_view_owner` refers to a view which already has a container or is
 the root of a view tree then an `OnChildUnavailable()` message will
 be sent to its old container or root and the view will be
 (re-)added to its new container as usual.  This special case also
 applies when the specified view is already a child of this view, in which
 case the behavior is similar to the view having been transferred to
 some other container and then back again.

 Note that an unavailable child will remain in its container's list of
 children until its container explicitly calls `RemoveChild()` to remove
 it.

 `host_import_token` is an import token which the view manager will
 use to import the node to which the child view's content should
 be attached.

 To establish the graphical embedding relation, the container view
 must create an event pair, bind one endpoint to an `ExportResourceOp`
 associated with the node to which the child's content nodes will be
 attached as descendants, and pass the other endpoint to this method as
 `host_import_token`.

 It is an error to add a view whose `child_key` already appears
 in the view's list of children; the connection will be closed.

 It is an error to add more than one child to a `ViewTree`'s container;
 it can only have at most one child (its root).

 This method is deprecated in favor of the eventpair-based one below.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>child_view_owner</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.viewsv1token/index.html'>fuchsia.ui.viewsv1token</a>/<a class='link' href='../fuchsia.ui.viewsv1token/index.html#ViewOwner'>ViewOwner</a></code>
            </td>
        </tr><tr>
            <td><code>host_import_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>



### AddChild2 {:#AddChild2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr><tr>
            <td><code>host_import_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>



### RemoveChild {:#RemoveChild}

 Removes the view referenced by `child_key` from the view's
 list of children.

 If `transferred_view_owner` is not null, associates it with the
 previously added child to allow it to be transferred elsewhere or
 closes the `transferred_view_owner` channel if there was none.

 It is an error to remove a view whose `child_key` does not appear
 in the container's list of children; the connection will be closed.

 This method is deprecated in favor of the eventpair-based one below.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>transferred_view_owner</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.viewsv1token/index.html'>fuchsia.ui.viewsv1token</a>/<a class='link' href='../fuchsia.ui.viewsv1token/index.html#ViewOwner'>ViewOwner</a>&gt;?</code>
            </td>
        </tr></table>



### RemoveChild2 {:#RemoveChild2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>transferred_view_holder_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;?</code>
            </td>
        </tr></table>



### SetChildProperties {:#SetChildProperties}

 Sets view properties for the child, such as layout constraints.

 This method must be called at least once after a child is added to
 set the view's properties before it can be rendered.  Rendering for
 children without properties is blocked until properties are set.

 The `child_view_properties` specifies the properties for the child, or
 null to remove the properties from the child which will cause rendering
 of the child's scene to be blocked until new properties are set.

 It is an error to specify a `child_key` that does not appear in
 the container's list of children; the connection will be closed.

 It is an error to specify malformed `child_view_properties` such
 as invalid layout properties; the connection will be closed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>child_view_properties</code></td>
            <td>
                <code><a class='link' href='#ViewProperties'>ViewProperties</a>?</code>
            </td>
        </tr></table>



### SendSizeChangeHintHACK {:#SendSizeChangeHintHACK}

 WIP API
 Sends a hint about a pending size change to the given node and all nodes
 below. This is generally sent before an animation.

 `width_change_factor` and `height_change_factor` is how much bigger or smaller
 the item is expected to be in the near future. This one number encapsulate
 both changes in scale, as well as changes to layout width and height.

 It is an error to specify a `child_key` that does not appear in
 the container's list of children; the connection will be closed.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>width_change_factor</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>height_change_factor</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### RequestSnapshotHACK {:#RequestSnapshotHACK}

 Request the snapshot of the child view.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>

## ViewContainerListener {:#ViewContainerListener}
*Defined in [fuchsia.ui.viewsv1/view_containers.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_containers.fidl#165)*

 An interface clients may implement to receive events from a view container.

### OnChildAttached {:#OnChildAttached}

 Called when a child view is attached along with embedding information.

 This method will be called at most once after the child is added.

 The implementation should invoke the callback once the event has
 been handled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>child_view_info</code></td>
            <td>
                <code><a class='link' href='#ViewInfo'>ViewInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnChildUnavailable {:#OnChildUnavailable}

 Called when a child view has become unavailable.

 A child may become unavailable for many reasons such being unregistered
 by its application, abnormal termination of its application, or
 cycles being introduced in the view tree.

 To complete removal of an unavailable child, this view component must
 call RemoveChild() on its view with `child_key`.

 The implementation should invoke the callback once the event has
 been handled.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>child_key</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## ViewManager {:#ViewManager}
*Defined in [fuchsia.ui.viewsv1/view_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_manager.fidl#25)*

 The view manager manages trees of views which represent user interface
 components.

 Applications create views to describe user interface components
 to present content to the user and support user interaction.

 The system creates a view tree to hold the root of a view hierarchy
 containing views from various applications.

 Refer to `View` and `ViewTree` for more information about these objects.

### GetScenic {:#GetScenic}

 Gets the scenic instance associated with this view manager.
 All graphical content for this view manager's views and view trees
 must come from sessions created by this `scenic` instance.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>scenic</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.scenic/index.html'>fuchsia.ui.scenic</a>/<a class='link' href='../fuchsia.ui.scenic/index.html#Scenic'>Scenic</a>&gt;</code>
            </td>
        </tr></table>



### CreateView {:#CreateView}

 Creates a view.

 The `view` is used to configure the view and interact with its
 local environment.

 The `view_owner` is used as a transferable reference which can
 be passed to the view's intended container as part of a request to
 add the view as a child.  The view manager itself does not describe
 how this interaction should take place, only that ownership should
 eventually be passed back through the container's view interface
 as an argument to `View.AddChild()`.

 The `view_listener` is used to receive events from the view.

 The `label` is an optional name to associate with the view for
 diagnostic purposes.  The label will be truncated if it is longer
 than `kLabelMaxLength`.

 `parent_export_token` is an export token which the view manager
 will use to export the node to which the view's content should be
 attached.

 To present graphical content, the view must obtain a `Session` from
 `Scenic`, create an event pair, bind one endpoint to an
 `ImportResourceOp` using `ImportSpec.NODE`, attach its content nodes as
 descendants of the imported node, and pass the other endpoint of the
 event pair to this method as `parent_export_token`.

 To destroy the view and cause it to be removed from the view tree,
 simply close the `view`, `view_listener`, or `view_owner` channels.

 This method is deprecated in favor of the eventpair-based one below.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view</code></td>
            <td>
                <code>request&lt;<a class='link' href='#View'>View</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_owner</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.viewsv1token/index.html'>fuchsia.ui.viewsv1token</a>/<a class='link' href='../fuchsia.ui.viewsv1token/index.html#ViewOwner'>ViewOwner</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_listener</code></td>
            <td>
                <code><a class='link' href='#ViewListener'>ViewListener</a></code>
            </td>
        </tr><tr>
            <td><code>parent_export_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



### CreateView2 {:#CreateView2}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view</code></td>
            <td>
                <code>request&lt;<a class='link' href='#View'>View</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_listener</code></td>
            <td>
                <code><a class='link' href='#ViewListener'>ViewListener</a></code>
            </td>
        </tr><tr>
            <td><code>parent_export_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



### CreateViewTree {:#CreateViewTree}

 Creates a view tree.

 The `view_tree` is used to configure the view tree and interact
 with the views it contains.

 The `view_tree_listener` is used to receive events from the view tree.

 The `label` is an optional name to associate with the view tree for
 diagnostic purposes.  The label will be truncated if it is longer
 than `kLabelMaxLength`.

 To destroy the view tree simply close the `view_tree` or
 `view_tree_listener` channels.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_tree</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ViewTree'>ViewTree</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>view_tree_listener</code></td>
            <td>
                <code><a class='link' href='#ViewTreeListener'>ViewTreeListener</a></code>
            </td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string?</code>
            </td>
        </tr></table>



## ViewProvider {:#ViewProvider}
*Defined in [fuchsia.ui.viewsv1/view_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_provider.fidl#15)*

 Provides a View upon request.

 Applications should implement and expose this service so that they can
 expose views to be embedded into other applications.

### CreateView {:#CreateView}

 Creates and registers a view with the view manager and returns its
 view owner which may subsequently be passed to `View.AddChild()`
 to attach the view to a view hierarchy.

 Implementors of this interface are responsible for creating the view
 and forwarding the `view_owner` interface request to
 `ViewManager.CreateView()`.

 The caller may request services from the created view via the `services`
 service provider.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_owner</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.ui.viewsv1token/index.html'>fuchsia.ui.viewsv1token</a>/<a class='link' href='../fuchsia.ui.viewsv1token/index.html#ViewOwner'>ViewOwner</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>services</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a>&gt;?</code>
            </td>
        </tr></table>



## ViewSnapshot {:#ViewSnapshot}
*Defined in [fuchsia.ui.viewsv1/view_snapshot.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_snapshot.fidl#11)*

 Defines an interface to take view snapshots.

### TakeSnapshot {:#TakeSnapshot}

 Takes a snapshot of a view and returns it in a callback.

 The `view_koid` identifies the view whose snapshot needs to be taken.

 The callback is invoked with the VMO buffer containing the snapshot.
 If successful, the buffer size is non-zero, otherwise it is 0.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>snapshot</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>

## ViewTree {:#ViewTree}
*Defined in [fuchsia.ui.viewsv1/view_trees.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_trees.fidl#47)*

 A view tree is a top-level container for a hierarchy of views.
 Each view is intended to operate independently from others and will
 generally correspond to discrete interactive spaces such as separate
 displays or isolated environments in a multi-user system.

 Within a view tree, certain global invariants may be enforced such as
 ensuring that only one view has focus at a time.

 View trees will typically be created by system components responsible
 for managing the overall user interface rather than end-user applications.

 LIFECYCLE

 Use `ViewManager.CreateViewTree()` to create a view tree.  The client
 uses the `ViewTree` interface to manage the view tree's content
 and implements the `ViewTreeListener` interface to handle events.

 To destroy a view tree, simply close the `ViewTree` channel.

 SETTING A ROOT VIEW

 Use `GetContainer()` to obtain an interface for manipulating the root view.

 See `ViewContainer` for more information.

 GETTING SERVICES

 The view tree's `fuchsia::sys::ServiceProvider` offers access to many services
 which are not directly expressed by the `ViewTree` interface itself, such
 as input, accessiblity, and editing capabilities.

 For example, perform the following actions to dispatch input events:

 1. Call `GetServiceProvider()` to obtain the view's service provider.

 2. Ask the service provider for its `InputDispatcher`.

 3. Send input events to the dispatcher for delivery to views.

### GetToken {:#GetToken}

 Gets the view tree's token.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='#ViewTreeToken'>ViewTreeToken</a></code>
            </td>
        </tr></table>

### GetServiceProvider {:#GetServiceProvider}

 Gets a service provider to access services which are associated with
 the view tree such as input, accessibility and editing capabilities.
 The view tree service provider is private to the view tree and should
 not be shared with anyone else.

 See `InputDispatcher`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr></table>



### GetContainer {:#GetContainer}

 Gets an interface for managing the view tree's root.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>container</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ViewContainer'>ViewContainer</a>&gt;</code>
            </td>
        </tr></table>



## ViewTreeListener {:#ViewTreeListener}
*Defined in [fuchsia.ui.viewsv1/view_trees.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_trees.fidl#64)*

 An interface clients may implement to receive events from a view tree.

## View {:#View}
*Defined in [fuchsia.ui.viewsv1/views.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/views.fidl#31)*

 A view is a graphical user interface component which is responsible
 for drawing and supporting user interactions in the area of the screen
 that it occupies.

 A view may also act as a container for other views (known as the
 view's children) which it may freely layout and position anywhere
 within its bounds to form a composite user interface.  The hierarchy
 of views thus formed is called a view tree.

 LIFECYCLE

 Use `ViewManager.CreateView()` to create a view.  The application
 uses the `View` interface to manage the view's content and implements
 the `ViewListener` interface to handle events.

 To destroy a view, simply close the `View` channel.

 ADDING CHILD VIEWS

 Use `GetContainer()` to obtain an interface for manipulating child views.

 See `ViewContainer` for more information.

### GetServiceProvider {:#GetServiceProvider}

 Gets a service provider to access services which are associated with
 the view.
 The view service provider is private to the view and should not be
 shared with anyone else.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a>&gt;</code>
            </td>
        </tr></table>



### OfferServiceProvider {:#OfferServiceProvider}

 This is a way for an app to offer services that are associated with a
 particular view. Used to expose services to the compositor

 In particular this should be used to let know which view is implementing
 the ability to show an IME

 `service_names` should contain a list of service names as defined with the
 FIDL syntax [Discoverable]

 The list of services will be used by the compositor to filter service
 providers when looking for a particular service.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>service_provider</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a></code>
            </td>
        </tr><tr>
            <td><code>service_names</code></td>
            <td>
                <code>vector&lt;string&gt;</code>
            </td>
        </tr></table>



### GetContainer {:#GetContainer}

 Gets an interface for managing the view's children.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>container</code></td>
            <td>
                <code>request&lt;<a class='link' href='#ViewContainer'>ViewContainer</a>&gt;</code>
            </td>
        </tr></table>



## ViewListener {:#ViewListener}
*Defined in [fuchsia.ui.viewsv1/views.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/views.fidl#57)*

 An interface clients may implement to receive events from a view.

### OnPropertiesChanged {:#OnPropertiesChanged}

 Called when the view receives new properties from its ancestors.
 Initially the view has no properties so this method will be called
 as soon as properties first become available and whenever they change
 thereafter.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#ViewProperties'>ViewProperties</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## **STRUCTS**

### ViewInfo {:#ViewInfo}
*Defined in [fuchsia.ui.viewsv1/view_containers.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_containers.fidl#195)*



 Provides embedding information about a view for use by its container.

 This information is valid until the container removes the view.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ViewProperties {:#ViewProperties}
*Defined in [fuchsia.ui.viewsv1/view_properties.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_properties.fidl#13)*



 Parameters and contextual information for a view provided by its container.

 When a container sets properties for its children, any properties which
 are set to null are inherited from the container's own ancestors.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_layout</code></td>
            <td>
                <code><a class='link' href='#ViewLayout'>ViewLayout</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>custom_focus_behavior</code></td>
            <td>
                <code><a class='link' href='#CustomFocusBehavior'>CustomFocusBehavior</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CustomFocusBehavior {:#CustomFocusBehavior}
*Defined in [fuchsia.ui.viewsv1/view_properties.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_properties.fidl#18)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>allow_focus</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>true</td>
        </tr>
</table>

### ViewLayout {:#ViewLayout}
*Defined in [fuchsia.ui.viewsv1/view_properties.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_properties.fidl#27)*



 Provides layout constraints for a view.



<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#SizeF'>SizeF</a></code>
            </td>
            <td> The size of the view in logical pixels.
 Must be non-negative.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>inset</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#InsetF'>InsetF</a></code>
            </td>
            <td> The inset of the view in logical pixels.
 Must be non-negative.
</td>
            <td>No default</td>
        </tr>
</table>

### ViewTreeToken {:#ViewTreeToken}
*Defined in [fuchsia.ui.viewsv1/view_tree_token.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_tree_token.fidl#18)*



 A view tree token is an opaque transferable reference to a view tree.

 The ViewManager provides each view tree with a unique view tree token when
 it is registered.  The token can subsequently be passed to other
 applications and used as a way to refer to the tree.

 View tree tokens should be kept secret and should only be shared with
 trusted services.



<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.viewsv1/view_manager.fidl#11">kLabelMaxLength</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

