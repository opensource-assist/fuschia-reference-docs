[TOC]

# fuchsia.ui.views


## **PROTOCOLS**

## View {#View}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#79)*

<p>A View is an interface that a component implements to offer Scenic view(s)
to its clients.</p>
<p>A Scenic view contains a tree of Scenic graph nodes which is used to render
a graphical user interface, such as a module, shell, or on-screen keyboard.
Other Scenic views can be embedded within this tree of nodes.  This creates
a scene graph describing the UI of the entire system, rooted at the
top-most view.  Different processes can contribute branches to the scene
graph, and their content will be rendered together in a shared space.</p>
<h1>Offering a View</h1>
<p>A component that wishes to offer a <code>View</code> can do so in one of two ways:</p>
<ol>
<li>
<p>Expose a <code>View</code> interface as a service. This is usually done by components
that provide a single view, or have a clearly defined &quot;main&quot; view.
In this case, the component may obtain relevant properties for configuring
the view using services that may be available in its namespace, such as:</p>
<ul>
<li><code>fuchsia.intl.PropertyProvider</code></li>
<li><code>fuchsia.accessibility.PropertyProvider</code></li>
</ul>
</li>
<li>
<p>Offer a domain-specific interface that provides <code>View</code>s using a
<code>request&lt;View&gt;</code> parameter.  In this case, the component may obtain relevant
properties for configuring the view using services that may be provided by its
client as part of the request.</p>
<p>For example, an encyclopedia component might offer a method to expose article views:</p>
<p>GetArticleView(string article_id,
fuchsia.intl.PropertyProvider intl_properties,
fuchsia.accessibility.PropertyProvider accessibility_properties,
request<View> view_request);</p>
<p>This latter case is probably less common, as controlling domain-specific
views tends to be the job of the component that creates them.</p>
</li>
</ol>
<h1>Presenting a View</h1>
<p>A client of the <code>View</code> interface will:</p>
<ol>
<li>Launch (or bind to) the component that provides the interface.</li>
<li>Connect to the component's <code>View</code> interface.</li>
<li>Call <code>Present()</code> to give the <code>View</code> an attachment point into the scene graph
via the <code>view_token</code>.  Subsequent calls to <code>Present()</code> will generate an error
and cause the connection to be closed.</li>
</ol>
<p>When the client no longer needs the View, it should disconnect from the
interface.</p>
<p>NOTE: The client owns the <code>View</code> instance and must retain it for the
lifetime of the UI that it displays. If the <code>View</code> instance is destroyed,
the connection will be dropped and all UI content will be destroyed.</p>
<h1>Implementing a View</h1>
<p>On the implementation side, a component that exposes the <code>View</code> interface
has the following responsibilities:</p>
<ul>
<li>When <code>Present()</code> is called, create a root for the <code>View</code>'s content in the
Scenic scene graph by passing the provided <code>view_token</code>.</li>
<li>Provide graphical content for the view and attach it to the root.</li>
<li>Adjust the appearance and/or contents of the view's content based on
relevant internationalization and/or accessibility properties as described
above.</li>
<li>Handle user interface events such as touches, key presses, and
<code>fuchsia.ui.gfx.ViewProperty</code> changes using other Scenic interfaces such
as <code>fuchsia.ui.Scenic</code> and <code>fuchsia.ui.SessionListener</code>.</li>
</ul>
<p>See also: <code>fuchsia.intl.PropertyProvider</code>, <code>fuchsia.accessibility.PropertyProvider</code>.</p>
<p>TODO(SCN-1198): Migrate all implementations of <code>ViewProvider</code> to use <code>View</code>.</p>

### Present {#Present}

<p>Provides the View with an attachment point to Scenic's scene graph.</p>
<p>When <code>Present()</code> is called the View's implementation should create a
View resource within Scenic by providing it with the <code>view_token</code> (using
a <code>fuchsia.ui.gfx.CreateResourceCmd</code> and <code>fuchsia.ui.gfx.ViewArgs</code>).</p>
<p>Then the implementation should attach its graphical content to the
newly-created View resource using a <code>fuchsia.ui.gfx.AddChildCmd</code>.</p>
<p>If the implementation already owns a View resource (because <code>Present()</code>
had already been called before), then it should terminate the connection
with an error.</p>
<p>TODO(SCN-1271): Allow re-parenting <code>View</code>s with a new <code>Present()</code> call.</p>

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

### ViewRef {#ViewRef}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#120)*



<p>A ViewRef is a handle to a kernel object which identifies a unique View
across the system. Two ViewRefs to the same View have the same KOID.</p>
<p>Clients use a ViewRef to identify a View, to validate a View, and to
receive a View invalidation signal.</p>
<p>As part of View creation, the client creates a linked
ViewRef/ViewRefControl pair and hands the pair to Scenic (ViewRefControl is
described below).  The client must remove the ViewRef's signal
capabilities; otherwise the View is not created.</p>
<p>The client may freely clone its ViewRef and share it, even before sending
it to Scenic.</p>
<p>Example 1. Accessibility accepts a ViewRef from a client to group the
semantic nodes, and semantic operations, associated with a client's View.
It must validate a client's ViewRef with Scenic.</p>
<p>Example 2. We use ViewRefs to create a FocusChain, which identifies Views
considered as &quot;in-focus&quot; down the View hierarchy. When a View is destroyed,
Scenic signals to all FocusChain holders that the ViewRef is now invalid.</p>


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

### ViewRefControl {#ViewRefControl}
*Defined in [fuchsia.ui.views/view.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view.fidl#138)*



<p>A ViewRefControl is the peer to a ViewRef. Their <code>reference</code>s are linked.</p>
<p>Like ViewRef, a ViewRefControl is a typed handle to an eventpair.  Unlike
ViewRef, a ViewRefControl's handle is unique. Scenic uses this property
when it ties a ViewRefControl to a View, arranged to share fate.  When a
View is destroyed, the associated destruction of its ViewRefControl
triggers an automatic <code>ZX_ERR_PEER_CLOSED</code> signal sent to all ViewRef
holders; hence ViewRef holders may track View lifetime.</p>
<p>As part of View creation, the client creates a linked
ViewRef/ViewRefControl pair and hands the pair to Scenic (ViewRef is
described above).  The client must not clone the ViewRefControl. It must
not remove or modify the ViewRefControl's capabilities; otherwise the View
is not created.</p>


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

### ViewHolderToken {#ViewHolderToken}
*Defined in [fuchsia.ui.views/view_token.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view_token.fidl#14)*



<p>Token that uniquely identifies an attachment point for a <code>View</code> in the
global scene graph.  Each <code>ViewHolderToken</code> has exactly one corresponding
<code>ViewToken</code>.</p>
<p>A Scenic client can reference contents from another client by creating a
<code>ViewHolder</code> resource using this token.  The other client must also create
a <code>View</code> resource using the corresponding <code>ViewToken</code>.</p>


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

### ViewToken {#ViewToken}
*Defined in [fuchsia.ui.views/view_token.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/view_token.fidl#25)*



<p>Token that uniquely identifies a <code>View</code>, which is the root point for a
subgraph in the global scene graph. Each <code>ViewToken</code> has exactly one
corresponding <code>ViewHolderToken</code>.</p>
<p>A Scenic client can have its contents referenced from another client by
creating a <code>View</code> resource using this token.  The other client must also
create a <code>ViewHolder</code> resource using the corresponding <code>ViewHolderToken</code>.</p>


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

### Command {#Command}
*Defined in [fuchsia.ui.views/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.views/commands.fidl#10)*

<p>DO NOT USE - Retained for ABI stability in fuchsia.ui.scenic.Command</p>
<p>DO NOT USE</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>empty</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
        </tr></table>









