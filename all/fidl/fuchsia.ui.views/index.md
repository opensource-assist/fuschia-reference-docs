Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.views


## **PROTOCOLS**

## View {:#View}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#79)*

 A View is an interface that a component implements to offer Scenic view(s)
 to its clients.

 A Scenic view contains a tree of Scenic graph nodes which is used to render
 a graphical user interface, such as a module, shell, or on-screen keyboard.
 Other Scenic views can be embedded within this tree of nodes.  This creates
 a scene graph describing the UI of the entire system, rooted at the
 top-most view.  Different processes can contribute branches to the scene
 graph, and their content will be rendered together in a shared space.

 # Offering a View

 A component that wishes to offer a `View` can do so in one of two ways:

 1. Expose a `View` interface as a service. This is usually done by components
    that provide a single view, or have a clearly defined "main" view.
    In this case, the component may obtain relevant properties for configuring
    the view using services that may be available in its namespace, such as:
    - `fuchsia.intl.PropertyProvider`
    - `fuchsia.accessibility.PropertyProvider`

 2. Offer a domain-specific interface that provides `View`s using a
    `request<View>` parameter.  In this case, the component may obtain relevant
    properties for configuring the view using services that may be provided by its
    client as part of the request.

    For example, an encyclopedia component might offer a method to expose article views:

      GetArticleView(string article_id,
                     fuchsia.intl.PropertyProvider intl_properties,
                     fuchsia.accessibility.PropertyProvider accessibility_properties,
                     request<View> view_request);

    This latter case is probably less common, as controlling domain-specific
    views tends to be the job of the component that creates them.

 # Presenting a View

 A client of the `View` interface will:

 1. Launch (or bind to) the component that provides the interface.
 2. Connect to the component's `View` interface.
 3. Call `Present()` to give the `View` an attachment point into the scene graph
    via the `view_token`.  Subsequent calls to `Present()` will generate an error
    and cause the connection to be closed.

 When the client no longer needs the View, it should disconnect from the
 interface.

 NOTE: The client owns the `View` instance and must retain it for the
 lifetime of the UI that it displays. If the `View` instance is destroyed,
 the connection will be dropped and all UI content will be destroyed.

 # Implementing a View

 On the implementation side, a component that exposes the `View` interface
 has the following responsibilities:

 * When `Present()` is called, create a root for the `View`'s content in the
   Scenic scene graph by passing the provided `view_token`.
 * Provide graphical content for the view and attach it to the root.
 * Adjust the appearance and/or contents of the view's content based on
   relevant internationalization and/or accessibility properties as described
   above.
 * Handle user interface events such as touches, key presses, and
   `fuchsia.ui.gfx.ViewProperty` changes using other Scenic interfaces such
   as `fuchsia.ui.Scenic` and `fuchsia.ui.SessionListener`.

 See also: `fuchsia.intl.PropertyProvider`, `fuchsia.accessibility.PropertyProvider`.

 TODO(SCN-1198): Migrate all implementations of `ViewProvider` to use `View`.

### Present {:#Present}

 Provides the View with an attachment point to Scenic's scene graph.

 When `Present()` is called the View's implementation should create a
 View resource within Scenic by providing it with the `view_token` (using
 a `fuchsia.ui.gfx.CreateResourceCmd` and `fuchsia.ui.gfx.ViewArgs`).

 Then the implementation should attach its graphical content to the
 newly-created View resource using a `fuchsia.ui.gfx.AddChildCmd`.

 If the implementation already owns a View resource (because `Present()`
 had already been called before), then it should terminate the connection
 with an error.

 TODO(SCN-1271): Allow re-parenting `View`s with a new `Present()` call.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>



## View {:#View}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#79)*

 A View is an interface that a component implements to offer Scenic view(s)
 to its clients.

 A Scenic view contains a tree of Scenic graph nodes which is used to render
 a graphical user interface, such as a module, shell, or on-screen keyboard.
 Other Scenic views can be embedded within this tree of nodes.  This creates
 a scene graph describing the UI of the entire system, rooted at the
 top-most view.  Different processes can contribute branches to the scene
 graph, and their content will be rendered together in a shared space.

 # Offering a View

 A component that wishes to offer a `View` can do so in one of two ways:

 1. Expose a `View` interface as a service. This is usually done by components
    that provide a single view, or have a clearly defined "main" view.
    In this case, the component may obtain relevant properties for configuring
    the view using services that may be available in its namespace, such as:
    - `fuchsia.intl.PropertyProvider`
    - `fuchsia.accessibility.PropertyProvider`

 2. Offer a domain-specific interface that provides `View`s using a
    `request<View>` parameter.  In this case, the component may obtain relevant
    properties for configuring the view using services that may be provided by its
    client as part of the request.

    For example, an encyclopedia component might offer a method to expose article views:

      GetArticleView(string article_id,
                     fuchsia.intl.PropertyProvider intl_properties,
                     fuchsia.accessibility.PropertyProvider accessibility_properties,
                     request<View> view_request);

    This latter case is probably less common, as controlling domain-specific
    views tends to be the job of the component that creates them.

 # Presenting a View

 A client of the `View` interface will:

 1. Launch (or bind to) the component that provides the interface.
 2. Connect to the component's `View` interface.
 3. Call `Present()` to give the `View` an attachment point into the scene graph
    via the `view_token`.  Subsequent calls to `Present()` will generate an error
    and cause the connection to be closed.

 When the client no longer needs the View, it should disconnect from the
 interface.

 NOTE: The client owns the `View` instance and must retain it for the
 lifetime of the UI that it displays. If the `View` instance is destroyed,
 the connection will be dropped and all UI content will be destroyed.

 # Implementing a View

 On the implementation side, a component that exposes the `View` interface
 has the following responsibilities:

 * When `Present()` is called, create a root for the `View`'s content in the
   Scenic scene graph by passing the provided `view_token`.
 * Provide graphical content for the view and attach it to the root.
 * Adjust the appearance and/or contents of the view's content based on
   relevant internationalization and/or accessibility properties as described
   above.
 * Handle user interface events such as touches, key presses, and
   `fuchsia.ui.gfx.ViewProperty` changes using other Scenic interfaces such
   as `fuchsia.ui.Scenic` and `fuchsia.ui.SessionListener`.

 See also: `fuchsia.intl.PropertyProvider`, `fuchsia.accessibility.PropertyProvider`.

 TODO(SCN-1198): Migrate all implementations of `ViewProvider` to use `View`.

### Present {:#Present}

 Provides the View with an attachment point to Scenic's scene graph.

 When `Present()` is called the View's implementation should create a
 View resource within Scenic by providing it with the `view_token` (using
 a `fuchsia.ui.gfx.CreateResourceCmd` and `fuchsia.ui.gfx.ViewArgs`).

 Then the implementation should attach its graphical content to the
 newly-created View resource using a `fuchsia.ui.gfx.AddChildCmd`.

 If the implementation already owns a View resource (because `Present()`
 had already been called before), then it should terminate the connection
 with an error.

 TODO(SCN-1271): Allow re-parenting `View`s with a new `Present()` call.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code><a class='link' href='#ViewToken'>ViewToken</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### ViewRef {:#ViewRef}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#120)*



 A ViewRef is a handle to a kernel object which identifies a unique View
 across the system. Two ViewRefs to the same View have the same KOID.

 Clients use a ViewRef to identify a View, to validate a View, and to
 receive a View invalidation signal.

 As part of View creation, the client creates a linked
 ViewRef/ViewRefControl pair and hands the pair to Scenic (ViewRefControl is
 described below).  The client must remove the ViewRef's signal
 capabilities; otherwise the View is not created.

 The client may freely clone its ViewRef and share it, even before sending
 it to Scenic.

 Example 1. Accessibility accepts a ViewRef from a client to group the
 semantic nodes, and semantic operations, associated with a client's View.
 It must validate a client's ViewRef with Scenic.

 Example 2. We use ViewRefs to create a FocusChain, which identifies Views
 considered as "in-focus" down the View hierarchy. When a View is destroyed,
 Scenic signals to all FocusChain holders that the ViewRef is now invalid.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reference</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewRefControl {:#ViewRefControl}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#138)*



 A ViewRefControl is the peer to a ViewRef. Their `reference`s are linked.

 Like ViewRef, a ViewRefControl is a typed handle to an eventpair.  Unlike
 ViewRef, a ViewRefControl's handle is unique. Scenic uses this property
 when it ties a ViewRefControl to a View, arranged to share fate.  When a
 View is destroyed, the associated destruction of its ViewRefControl
 triggers an automatic `ZX_ERR_PEER_CLOSED` signal sent to all ViewRef
 holders; hence ViewRef holders may track View lifetime.

 As part of View creation, the client creates a linked
 ViewRef/ViewRefControl pair and hands the pair to Scenic (ViewRef is
 described above).  The client must not clone the ViewRefControl. It must
 not remove or modify the ViewRefControl's capabilities; otherwise the View
 is not created.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reference</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewHolderToken {:#ViewHolderToken}
*Defined in [fuchsia.ui.views/view_token.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view_token.fidl#14)*



 Token that uniquely identifies an attachment point for a `View` in the
 global scene graph.  Each `ViewHolderToken` has exactly one corresponding
 `ViewToken`.

 A Scenic client can reference contents from another client by creating a
 `ViewHolder` resource using this token.  The other client must also create
 a `View` resource using the corresponding `ViewToken`.


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

### ViewToken {:#ViewToken}
*Defined in [fuchsia.ui.views/view_token.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view_token.fidl#25)*



 Token that uniquely identifies a `View`, which is the root point for a
 subgraph in the global scene graph. Each `ViewToken` has exactly one
 corresponding `ViewHolderToken`.

 A Scenic client can have its contents referenced from another client by
 creating a `View` resource using this token.  The other client must also
 create a `ViewHolder` resource using the corresponding `ViewHolderToken`.


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

### ViewRef {:#ViewRef}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#120)*



 A ViewRef is a handle to a kernel object which identifies a unique View
 across the system. Two ViewRefs to the same View have the same KOID.

 Clients use a ViewRef to identify a View, to validate a View, and to
 receive a View invalidation signal.

 As part of View creation, the client creates a linked
 ViewRef/ViewRefControl pair and hands the pair to Scenic (ViewRefControl is
 described below).  The client must remove the ViewRef's signal
 capabilities; otherwise the View is not created.

 The client may freely clone its ViewRef and share it, even before sending
 it to Scenic.

 Example 1. Accessibility accepts a ViewRef from a client to group the
 semantic nodes, and semantic operations, associated with a client's View.
 It must validate a client's ViewRef with Scenic.

 Example 2. We use ViewRefs to create a FocusChain, which identifies Views
 considered as "in-focus" down the View hierarchy. When a View is destroyed,
 Scenic signals to all FocusChain holders that the ViewRef is now invalid.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reference</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewRefControl {:#ViewRefControl}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#138)*



 A ViewRefControl is the peer to a ViewRef. Their `reference`s are linked.

 Like ViewRef, a ViewRefControl is a typed handle to an eventpair.  Unlike
 ViewRef, a ViewRefControl's handle is unique. Scenic uses this property
 when it ties a ViewRefControl to a View, arranged to share fate.  When a
 View is destroyed, the associated destruction of its ViewRefControl
 triggers an automatic `ZX_ERR_PEER_CLOSED` signal sent to all ViewRef
 holders; hence ViewRef holders may track View lifetime.

 As part of View creation, the client creates a linked
 ViewRef/ViewRefControl pair and hands the pair to Scenic (ViewRef is
 described above).  The client must not clone the ViewRefControl. It must
 not remove or modify the ViewRefControl's capabilities; otherwise the View
 is not created.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reference</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewHolderToken {:#ViewHolderToken}
*Defined in [fuchsia.ui.views/view_token.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view_token.fidl#14)*



 Token that uniquely identifies an attachment point for a `View` in the
 global scene graph.  Each `ViewHolderToken` has exactly one corresponding
 `ViewToken`.

 A Scenic client can reference contents from another client by creating a
 `ViewHolder` resource using this token.  The other client must also create
 a `View` resource using the corresponding `ViewToken`.


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

### ViewToken {:#ViewToken}
*Defined in [fuchsia.ui.views/view_token.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view_token.fidl#25)*



 Token that uniquely identifies a `View`, which is the root point for a
 subgraph in the global scene graph. Each `ViewToken` has exactly one
 corresponding `ViewHolderToken`.

 A Scenic client can have its contents referenced from another client by
 creating a `View` resource using this token.  The other client must also
 create a `ViewHolder` resource using the corresponding `ViewHolderToken`.


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







## **UNIONS**

### Command {:#Command}
*Defined in [fuchsia.ui.views/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/commands.fidl#10)*

 DO NOT USE - Retained for ABI stability in fuchsia.ui.scenic.Command

 DO NOT USE

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>empty</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>

### Command {:#Command}
*Defined in [fuchsia.ui.views/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/commands.fidl#10)*

 DO NOT USE - Retained for ABI stability in fuchsia.ui.scenic.Command

 DO NOT USE

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>empty</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>







