[TOC]

# fuchsia.ui.app


## **PROTOCOLS**

## View {#View}
*Defined in [fuchsia.ui.app/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.app/view.fidl#45)*

<p>A View is an interface that a component implements to offer a Scenic
view to its clients.  A Scenic view is container of Scenic graph nodes,
which, when rendered, might display a graphical user interface, such
as a module, shell, or on-screen keyboard.</p>
<p>A client of the <code>View</code> interface will:</p>
<ol>
<li>Launch (or bind to) the component that provides the interface.</li>
<li>Connect to the component's <code>View</code> interface.</li>
<li>Call <code>SetConfig()</code> at least once to configure the view's presentation
parameters.</li>
<li>Call <code>AttachView()</code> to ask the <code>View</code> to attach its graphical
content to the Scenic scene graph using the provided <code>view_token</code>.</li>
<li>Optionally, while the View is attached, call <code>SetConfig()</code> again to
modify any presentation parameters as needed.</li>
</ol>
<p>When the client no longer needs the View, it should disconnect from
the interface and terminate (or unbind) from the component.</p>
<p>NOTE: Unlike with <code>ViewProvider</code>, the client owns the <code>View</code> instance and
must retain it for the lifetime of the UI that it displays. If the <code>View</code>
instance is destroyed, the connection will be dropped.</p>
<p>On the implementation side, a component that exposes the
<code>View</code> interface has the following responsibilities:</p>
<ul>
<li>Initialize and attach the View's content to the Scenic scene graph
using the <code>fuchsia.ui.view.CreateViewCmd</code> and passing the provided
<code>view_token</code>.</li>
<li>Adjust the appearance and/or contents of the view's content whenever
its <code>ViewConfig</code> changes.</li>
<li>Provide graphical content for the view and handle user interface
events such as touches, key presses, and <code>fuchsia.ui.view.ViewProperty</code>
changes using other Scenic interfaces such as <code>fuchsia.ui.Scenic</code>
and <code>fuchsia.ui.SessionListener</code>.</li>
</ul>
<p>TODO(SCN-1198): Migrate all implementations of <code>ViewProvider</code> to use <code>View</code>.</p>

### SetConfig {#SetConfig}

<p>Updates the View's configuration.</p>
<p>To prevent triggering UI changes shortly after a client starts up, the
View's client should set the configuration prior to calling
<code>AttachView()</code> unless the default is adequate.</p>
<p>May be called again at any time to modify the view's configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>config</code></td>
            <td>
                <code><a class='link' href='#ViewConfig'>ViewConfig</a></code>
            </td>
        </tr></table>



### Attach {#Attach}

<p>Attaches the View to Scenic's scene graph. Must only be called once per
<code>View</code> lifetime.</p>
<p>The View's implementation should pass the <code>view_token</code> to Scenic
using a <code>fuchsia.ui.view.CreateViewCmd</code>.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
        </tr></table>



## ViewProvider {#ViewProvider}
*Defined in [fuchsia.ui.app/view_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.app/view_provider.fidl#19)*

<p>ViewProvider is the standard mechanism for two modules to each obtain half
of a shared eventpair token.  The shared token is a capability allowing the
modules to ask Scenic to create a ViewHolder/View pair.  The resulting
View and ViewHolder are linked together until either one is destroyed.</p>
<p>Modules are free to use any other mechanism to agree upon the shared
eventpair token, and use this to create the linked ViewHolder/View.
ViewProvider is given for the convenience of clients that don't require
a more complex implementation.</p>

### CreateView {#CreateView}

<p>Creates a new View under the control of the ViewProvider.</p>
<p><code>token</code> is one half of the shared eventpair which will bind the new View
to its associated ViewHolder.  The ViewProvider will use <code>token</code> to
create its internal View representation.  The caller is expected to use
its half to create corresponding ViewHolder object.</p>
<p><code>incoming_services</code> allows clients to request services from the
ViewProvider implementation.  <code>outgoing_services</code> allows clients to
provide services of their own to the ViewProvider implementation.</p>
<p>Clients can embed a ViewHolder (and by proxy the paired View) into their
scene graph by using <code>Node.AddChild()</code>.  The ViewHolder cannot itself
have any children. A ViewProvider implementation can nest scene objects
within its View by using <code>View.AddChild()</code>.  The View itself
cannot be a child of anything.</p>
<p>Modules can use these mechanisms to establish a distributed,
inter-process scene graph.</p>

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
                <code>request&lt;<a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#ServiceProvider'>ServiceProvider</a>&gt;?</code>
            </td>
        </tr><tr>
            <td><code>outgoing_services</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sys/'>fuchsia.sys</a>/<a class='link' href='../fuchsia.sys/#ServiceProvider'>ServiceProvider</a>?</code>
            </td>
        </tr></table>





## **STRUCTS**

### ViewConfig {#ViewConfig}
*Defined in [fuchsia.ui.app/view_config.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.app/view_config.fidl#12)*



<p>Collection of properties that provide affect the rendering of a view's
contents. This might include internationalization settings, font scaling,
night mode, high contrast mode, etc.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>intl_profile</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#Profile'>Profile</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>













