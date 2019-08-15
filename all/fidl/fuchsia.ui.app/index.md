Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.app


## **PROTOCOLS**

## View {:#View}
*Defined in [fuchsia.ui.app/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.app/view.fidl#45)*

 A View is an interface that a component implements to offer a Scenic
 view to its clients.  A Scenic view is container of Scenic graph nodes,
 which, when rendered, might display a graphical user interface, such
 as a module, shell, or on-screen keyboard.

 A client of the `View` interface will:

 1. Launch (or bind to) the component that provides the interface.
 2. Connect to the component's `View` interface.
 3. Call `SetConfig()` at least once to configure the view's presentation
    parameters.
 4. Call `AttachView()` to ask the `View` to attach its graphical
    content to the Scenic scene graph using the provided `view_token`.
 5. Optionally, while the View is attached, call `SetConfig()` again to
    modify any presentation parameters as needed.

 When the client no longer needs the View, it should disconnect from
 the interface and terminate (or unbind) from the component.

 NOTE: Unlike with `ViewProvider`, the client owns the `View` instance and
 must retain it for the lifetime of the UI that it displays. If the `View`
 instance is destroyed, the connection will be dropped.

 On the implementation side, a component that exposes the
 `View` interface has the following responsibilities:

 * Initialize and attach the View's content to the Scenic scene graph
   using the `fuchsia.ui.view.CreateViewCmd` and passing the provided
   `view_token`.
 * Adjust the appearance and/or contents of the view's content whenever
   its `ViewConfig` changes.
 * Provide graphical content for the view and handle user interface
   events such as touches, key presses, and `fuchsia.ui.view.ViewProperty`
   changes using other Scenic interfaces such as `fuchsia.ui.Scenic`
   and `fuchsia.ui.SessionListener`.

  TODO(SCN-1198): Migrate all implementations of `ViewProvider` to use `View`.

### SetConfig {:#SetConfig}

 Updates the View's configuration.

 To prevent triggering UI changes shortly after a client starts up, the
 View's client should set the configuration prior to calling
 `AttachView()` unless the default is adequate.

 May be called again at any time to modify the view's configuration.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#ViewConfig'>ViewConfig</a></code>
            </td>
        </tr></table>



### Attach {:#Attach}

 Attaches the View to Scenic's scene graph. Must only be called once per
 `View` lifetime.

 The View's implementation should pass the `view_token` to Scenic
 using a `fuchsia.ui.view.CreateViewCmd`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>



## ViewProvider {:#ViewProvider}
*Defined in [fuchsia.ui.app/view_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.app/view_provider.fidl#19)*

 ViewProvider is the standard mechanism for two modules to each obtain half
 of a shared eventpair token.  The shared token is a capability allowing the
 modules to ask Scenic to create a ViewHolder/View pair.  The resulting
 View and ViewHolder are linked together until either one is destroyed.

 Modules are free to use any other mechanism to agree upon the shared
 eventpair token, and use this to create the linked ViewHolder/View.
 ViewProvider is given for the convenience of clients that don't require
 a more complex implementation.

### CreateView {:#CreateView}

 Creates a new View under the control of the ViewProvider.

 `token` is one half of the shared eventpair which will bind the new View
 to its associated ViewHolder.  The ViewProvider will use `token` to
 create its internal View representation.  The caller is expected to use
 its half to create corresponding ViewHolder object.

 `incoming_services` allows clients to request services from the
 ViewProvider implementation.  `outgoing_services` allows clients to
 provide services of their own to the ViewProvider implementation.

 Clients can embed a ViewHolder (and by proxy the paired View) into their
 scene graph by using `Node.AddChild()`.  The ViewHolder cannot itself
 have any children. A ViewProvider implementation can nest scene objects
 within its View by using `View.AddChild()`.  The View itself
 cannot be a child of anything.

 Modules can use these mechanisms to establish a distributed,
 inter-process scene graph.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr><tr>
            <td><code>incoming_services</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a>&gt;?</code>
            </td>
        </tr><tr>
            <td><code>outgoing_services</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/index.html'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/index.html#ServiceProvider'>ServiceProvider</a>?</code>
            </td>
        </tr></table>





## **STRUCTS**

### ViewConfig {:#ViewConfig}
*Defined in [fuchsia.ui.app/view_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.app/view_config.fidl#12)*



 Collection of properties that provide affect the rendering of a view's
 contents. This might include internationalization settings, font scaling,
 night mode, high contrast mode, etc.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>intl_profile</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#Profile'>Profile</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













