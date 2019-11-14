[TOC]

# fuchsia.ui.gfx


## **PROTOCOLS**

## SnapshotCallbackDEPRECATED {#SnapshotCallbackDEPRECATED}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#386)*


### OnData {#OnData}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/#Buffer'>Buffer</a></code>
            </td>
        </tr></table>



## PoseBufferProvider {#PoseBufferProvider}
*Defined in [fuchsia.ui.gfx/pose_buffer_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/pose_buffer_provider.fidl#9)*

<p>A minimal fidl interface to allow sourcing the contents of a PoseBuffer from another service.</p>

### SetPoseBuffer {#SetPoseBuffer}

<p>Sets the PoseBuffer and the parameters PoseBufferProvider will use to fill that PoseBuffer.
Setting this when it is already set will replace the previously set parameters with the new
parameters, which will release the provider's reference to the buffer.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>num_entries</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>base_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>time_interval</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>





## **STRUCTS**

### CreateResourceCmd {#CreateResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#103)*



<p>Instructs the compositor to create the specified <code>Resource</code>, and to register
it in a table so that it can be referenced by subsequent commands.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>An ID that is currently not used within the session.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>resource</code></td>
            <td>
                <code><a class='link' href='#ResourceArgs'>ResourceArgs</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ReleaseResourceCmd {#ReleaseResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#116)*



<p>Releases the client's reference to the resource; it is then illegal to use
the ID in subsequent Commands.  Other references to the resource may exist,
so releasing the resource does not result in its immediate destruction; it is
only destroyed once the last reference is released.  For example, the
resource may be required to render an in-progress frame, or it may be
referred to by another resource).  However, the ID will be immediately
unregistered, and may be reused to create a new resource.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>ID of the resource to be dereferenced.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ExportResourceCmd {#ExportResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#129)*



<p>Create an external reference to the specified resource, which can then be
imported into another Session by passing a handle to <code>token</code>'s peer to
ImportResourceCmd; see that comment for more details.</p>
<p>The importing client is typically in a different process than the exporter.
No specific mechanism is provided for transferring a token from an exporter
to an importer; collaborators may choose any out-of-band API they wish to do
so.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImportResourceCmd {#ImportResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#156)*



<p>Import a resource that was exported via ExportResourceCmd().  <code>token</code> is
a handle to the eventpair peer that was used to export the resource, and
<code>spec</code> describes the type of the imported resource, and the commands which
can legally be applied to it.  Afterward, <code>id</code> can be used to refer to the
resource in an Command, similarly (but not identically: see below) to a
resource that was created in the session.  For example, you can add children
to an imported EntityNode via AddChildCmd.</p>
<p>However, note that the importer does not gain full access to the imported
resource, but rather to an attenuated subset of its capabilities.  For
example, you cannot use a DetachCmd to detach an imported EntityNode from
its parent.</p>
<p>Unlike ExportResourceCmd, there is no configurable timeout.  There is an
expectation that the exported resource will become available in a short
amount of time.  TODO: this needs elaboration... e.g. we might notify via the
SessionListener when we know that the link will never be made (e.g. if the
peer of the import token is destroyed).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>token</code></td>
            <td>
                <code>handle&lt;eventpair&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>spec</code></td>
            <td>
                <code><a class='link' href='#ImportSpec'>ImportSpec</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetTagCmd {#SetTagCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#176)*



<p>Sets/clears a node's tag value.</p>
<p>A session can apply a tag value to any node to which it has access, including
imported nodes.  These tags are private to the session and cannot be read
or modified by other sessions.  When multiple sessions import the same node,
each session will only observe its own tag values.</p>
<p>Hit test results for a session only include nodes which the session has
tagged with a non-zero value.  Therefore a session can use tag values to
associate nodes with their functional purpose when picked.</p>
<p>Constraints:</p>
<ul>
<li><code>node_id</code> refs a <code>Node</code>.</li>
<li><code>tag_value</code> is the tag value to assign, or 0 to remove the tag.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tag_value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DetachCmd {#DetachCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#191)*



<p>Detaches a parentable object from its parent (e.g. a node from a parent node,
or a layer from a layer stack).  It is illegal to apply this command to a
non-parentable object.  No-op if the target object currently has no parent.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a parentable object</li>
</ul>
<p>Discussion:
For nodes, this command will detach a node from its parent, regardless of
whether it is a part or a child of its parent.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetTranslationCmd {#SetTranslationCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#199)*



<p>Sets a Resource's (typically a Node's) translation.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a Resource with the has_transform characteristic.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetScaleCmd {#SetScaleCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#208)*



<p>Sets a Resource's (typically a Node's) scale.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a Resource with the has_transform characteristic.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetRotationCmd {#SetRotationCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#217)*



<p>Sets a Resource's (typically a Node's) rotation.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a Resource with the has_transform characteristic.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#QuaternionValue'>QuaternionValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetAnchorCmd {#SetAnchorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#226)*



<p>Sets a Resource's (typically a Node's) anchor point.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a Resource with the has_transform characteristic.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetSizeCmd {#SetSizeCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#237)*



<p>Sets an object's size.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a resizeable object.</li>
<li>some objects that support this command may have additional constraints
(e.g. in some cases <code>depth</code> must be zero).</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Vector2Value'>Vector2Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetOpacityCmd {#SetOpacityCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#247)*



<p>Sets a node's opacity.</p>
<p>Constraints:</p>
<ul>
<li><code>node_id</code> refs a <code>Node</code> with the has_opacity characteristic.</li>
<li><code>opacity</code> is in the range [0, 1].</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>opacity</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SendSizeChangeHintCmdHACK {#SendSizeChangeHintCmdHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#258)*



<p>Sends a hint about a pending size change to the given node and all nodes
below. This is generally sent before an animation.</p>
<p><code>width_change_factor</code> and <code>height_change_factor</code> is how much bigger or smaller
the item is expected to be in the near future. This one number encapsulate
both changes in scale, as well as changes to layout width and height.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>width_change_factor</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height_change_factor</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddChildCmd {#AddChildCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#273)*



<p>Add a node as a child to another node.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a Node with the has_children characteristic.</li>
<li><code>child_id</code> refs any Node.</li>
</ul>
<p>Discussion:
The child node is first removed from its existing parent, as if DetachCmd
was applied first.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>child_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddPartCmd {#AddPartCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#293)*



<p>Add a node as a part of another node.  The implications of being a part
rather than a child differ based on the type of the part.  However, one
implication is constant: removing all of a node's children (e.g. via
DetachChildrenCmd) does not affect its parts.  This is similar to the
&quot;shadow DOM&quot; in a web browser: the controls of a <video> element are
implemented as using the shadow DOM, and do no show up amongst the children
of that element.</p>
<p>Constraints:</p>
<ul>
<li><code>id</code> refs a Node with the has_parts characteristic.</li>
<li><code>part_id</code> refs any Node.</li>
</ul>
<p>Discussion:
The part node is first removed from its existing parent, as if DetachCmd
was applied first.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>part_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DetachChildrenCmd {#DetachChildrenCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#299)*



<p>Detaches all of a node's children (but not its parts).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetShapeCmd {#SetShapeCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#317)*



<p>Sets/clears a node's shape.</p>
<p>Constraints:</p>
<ul>
<li><code>node_id</code> refs a <code>Node</code> with the has_shape characteristic.</li>
<li><code>shape_id</code> refs a <code>Shape</code>, or nothing.</li>
<li>if this command causes the target to have both a <code>Shape</code> and a <code>Material</code>,
then these must be compatible with each other (see README.md regarding
&quot;Shape/Material Compatibility&quot;).</li>
</ul>
<p>Discussion:
In order to be painted, a node requires both a <code>Shape</code> and a <code>Material</code>.
Without a material, a node can still participate in hit-testing and clipping.
Without a shape, a node cannot do any of the above.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>shape_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetMaterialCmd {#SetMaterialCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#336)*



<p>Sets/clears a node's material.</p>
<p>Constraints:</p>
<ul>
<li><code>node_id</code> refs a <code>Node</code> with the has_material characteristic.</li>
<li><code>material_id</code> refs a <code>Material</code>, or nothing.</li>
<li>if this command causes the target to have both a <code>Shape</code> and a <code>Material</code>,
then these must be compatible with each other (see README.md regarding
&quot;Shape/Material Compatibility&quot;).</li>
</ul>
<p>Discussion:
In order to be painted, a node requires both a <code>Shape</code> and a <code>Material</code>.
Without a material, a node can still participate in hit-testing and clipping.
Without a shape, a node cannot do any of the above.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>material_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetClipCmd {#SetClipCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#361)*



<p>Sets/clears a node's clip.  DEPRECATED: use SetClipPlanesCmd.</p>
<p>Constraints:</p>
<ul>
<li><code>node_id</code> refs a <code>Node</code> with the has_clip characteristic.</li>
<li><code>clip_id</code> a <code>Node</code> with the is_clip characteristic, or nothing.  If the
referenced node is not rooted, then it will have no effect (since its
full world-transform cannot be determined).</li>
<li><code>clip_to_self</code> If false, children are only clipped to the region specified
by <code>clip_id</code>.  If true, children are additionally clipped to the node's
shape (as determined by its ShapeNode parts).</li>
</ul>
<p>Discussion:
If a node has a clip, it will be applied to both the parts and the children
of the node.  Under some circumstances (TBD), a clip will not be applicable
to a node; in such cases it will be as though no clip has been specified for
the node.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>clip_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>clip_to_self</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetHitTestBehaviorCmd {#SetHitTestBehaviorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#372)*



<p>Sets a node's hit test behavior.</p>
<p>Discussion:
By default, hit testing is performed on the node's content, its parts,
and its children.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>hit_test_behavior</code></td>
            <td>
                <code><a class='link' href='#HitTestBehavior'>HitTestBehavior</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetViewPropertiesCmd {#SetViewPropertiesCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#381)*



<p>Sets the properties for a ViewHolder's attached View.</p>
<p>Constraints:</p>
<ul>
<li><code>view_holder_id</code> refs a <code>ViewHolder</code>.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_holder_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#ViewProperties'>ViewProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TakeSnapshotCmdDEPRECATED {#TakeSnapshotCmdDEPRECATED}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#390)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>callback</code></td>
            <td>
                <code><a class='link' href='#SnapshotCallbackDEPRECATED'>SnapshotCallbackDEPRECATED</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraCmd {#SetCameraCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#401)*



<p>Sets a renderer's camera.</p>
<p>Constraints:</p>
<ul>
<li><code>renderer_id</code> refs a <code>Renderer</code>.</li>
<li><code>camera_id</code> refs a <code>Camera</code>, or stops rendering by passing zero.</li>
<li><code>matrix</code> is a value or variable of type kMatrix4x4.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>renderer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraTransformCmd {#SetCameraTransformCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#414)*



<p>Sets a camera's view matrix.
This operation can be applied to both Cameras and StereoCameras.</p>
<p>Constraints:</p>
<ul>
<li><code>camera_id</code> refs a <code>Camera</code>.</li>
<li><code>eye_position</code> is the position of the eye.</li>
<li><code>eye_look_at</code> is the point is the scene the that eye is pointed at.</li>
<li><code>eye_up</code> defines the camera's &quot;up&quot; vector.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>eye_position</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>eye_look_at</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>eye_up</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraProjectionCmd {#SetCameraProjectionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#430)*



<p>Sets a camera's projection matrix.
This operation cannot be applied to a StereoCamera.</p>
<p>Constraints:</p>
<ul>
<li><code>camera_id</code> refs a <code>Camera</code> that is not a <code>StereoCamera</code>.</li>
<li><code>fovy</code> is the Y-axis field of view, in radians.</li>
</ul>
<p>NOTE: A default orthographic projection is specified by setting <code>fovy</code> to
zero.  In this case, the camera transform is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>fovy</code></td>
            <td>
                <code><a class='link' href='#FloatValue'>FloatValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetStereoCameraProjectionCmd {#SetStereoCameraProjectionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#445)*



<p>Sets a StereoCamera's projection matrices.
This operation can only be applied to a StereoCamera.</p>
<p>Constraints:</p>
<ul>
<li><code>camera_id</code> refs a <code>StereoCamera</code>.</li>
<li><code>left_projection</code> is the projection matrix for the left eye.</li>
<li><code>right_projection</code> is the projection matrix for the right eye.</li>
</ul>
<p>These projection matrices may also contain a transform in camera space for
their eye if needed.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>left_projection</code></td>
            <td>
                <code><a class='link' href='#Matrix4Value'>Matrix4Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>right_projection</code></td>
            <td>
                <code><a class='link' href='#Matrix4Value'>Matrix4Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraClipSpaceTransformCmd {#SetCameraClipSpaceTransformCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#457)*



<p>Sets a camera's 2D clip-space transform.</p>
<p>Constraints:</p>
<ul>
<li><code>camera_id</code> refs a <code>Camera</code>.</li>
<li><code>translation</code> is the desired translation, in Vulkan NDC.</li>
<li><code>scale</code> is the scale factor to apply on the x/y plane before translation.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>translation</code></td>
            <td>
                <code><a class='link' href='#vec2'>vec2</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scale</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraPoseBufferCmd {#SetCameraPoseBufferCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#535)*



<p>Sets the &quot;pose buffer&quot; for the camera identified by <code>camera_id</code>.
This operation can be applied to both Cameras and StereoCameras.</p>
<p>This will override any position and rotation set for the camera and will
make it take its position and rotation from the pose buffer each frame
based on the presentation time for that frame.</p>
<p>A pose buffer represents a ring buffer of poses for a fixed number of time
points in the future. Each entry in the buffer identified by <code>buffer_id</code> is
a quaternion and a position layed out as follows:</p>
<p>struct Pose {
// Quaternion
float32 a;
float32 b;
float32 c;
float32 d;</p>
<p>// Position
float32 x;
float32 y;
float32 z;</p>
<p>// Reserved/Padding
byte[4] reserved;
}</p>
<p>The buffer can be thought of as a packed array of <code>num_entries</code> Pose structs
and is required to be at least num_entries * sizeof(Pose) bytes.</p>
<p>The quaternions and positions are specified in the space of the camera's
parent node.</p>
<p><code>base_time</code> is a base time point expressed in nanoseconds in the
<code>CLOCK_MONOTONIC</code> timebase and <code>time_interval</code> is the time in nanoseconds
between entries in the buffer. <code>base_time</code> must be in the past.</p>
<p>For a given point in time <code>t</code> expressed in nanoseconds in the
<code>CLOCK_MONOTONIC</code> timebase the index of the corresponding pose in
the pose buffer can be computed as follows:</p>
<p>index(t) = ((t - base_time) / time_interval) % num_entries</p>
<p>poses[index(t)] is valid for t over the time interval (t - time_interval, t]
and should be expected to updated continuously without synchronization
for the duration of that interval. If a single pose value is needed for
multiple non-atomic operations a value should be latched and stored outside
the pose buffer.</p>
<p>Because the poses are not protected by any synchronization primitives it is
possible that when a pose is latched it will be only partially updated, and
the pose being read will contain some components from the pose before it is
updated and some components from the updated pose. The safety of using these
&quot;torn&quot; poses relies on two things:</p>
<ol>
<li>
<p>Sequential poses written to poses[index(t)] are very similar to each
other numerically, so that if some components are taken from the first and
some are taken from another the result is numerically similar to both</p>
</li>
<li>
<p>The space of positions and quaternions is locally flat at the scale of
changes between sequential updates, which guarantees that two poses which
are numerically similar also represent semantically similar poses (i.e.
there are no discontinuities which will cause a small numerical change in
the position or quaterninon to cause a large change in the encoded pose)
For positions this is guaranteed because Scenic uses a Euclidean 3-space
which is globally flat and for quaternions this is guaranteed because
quaternions encode rotation as points on a unit 4-sphere, and spheres are
locally flat. For more details on the encoding of rotations in quaterions
see https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation</p>
</li>
</ol>
<p>This commanderation is intended for late latching camera pose to support
low-latency motion-tracked rendering.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>camera_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>num_entries</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>base_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>time_interval</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetLightColorCmd {#SetLightColorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#544)*



<p>Sets the color of the Light identified by <code>light_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>color</code></td>
            <td>
                <code><a class='link' href='#ColorRgbValue'>ColorRgbValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetLightDirectionCmd {#SetLightDirectionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#550)*



<p>Sets the direction of the DirectionalLight identified by <code>light_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>direction</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddLightCmd {#AddLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#558)*



<p>DEPRECATED
Adds the light specified by <code>light_id</code> specified by <code>light_id</code> to the scene
identified by <code>scene_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scene_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DetachLightCmd {#DetachLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#565)*



<p>Detach the light specified by <code>light_id</code> from the scene that it is attached
to, if any.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DetachLightsCmd {#DetachLightsCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#570)*



<p>Detach all lights from the scene specified by <code>scene_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scene_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetTextureCmd {#SetTextureCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#583)*



<p>Sets/clears a material's texture.</p>
<p>Constraints:</p>
<ul>
<li><code>material_id</code> refs a <code>Material</code>.</li>
<li><code>texture_id</code> refs a <code>Image</code>, <code>ImagePipe</code>, or nothing.</li>
</ul>
<p>If no texture is provided (i.e. <code>texture_id</code> is zero), a solid color is used.
If a texture is provided, then the value sampled from the texture is
multiplied by the color.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>material_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>texture_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetColorCmd {#SetColorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#595)*



<p>Sets a material's color.</p>
<p>Constraints:</p>
<ul>
<li><code>material_id</code> refs a <code>Material</code>.</li>
</ul>
<p>If a texture is set on the material, then the value sampled from the texture
is multiplied by the color.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>material_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>color</code></td>
            <td>
                <code><a class='link' href='#ColorRgbaValue'>ColorRgbaValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshVertexFormat {#MeshVertexFormat}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#627)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position_type</code></td>
            <td>
                <code><a class='link' href='#ValueType'>ValueType</a></code>
            </td>
            <td><p>kVector2 or kVector3.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>normal_type</code></td>
            <td>
                <code><a class='link' href='#ValueType'>ValueType</a></code>
            </td>
            <td><p>kVector2 or kVector3 (must match position_type), or kNone.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>tex_coord_type</code></td>
            <td>
                <code><a class='link' href='#ValueType'>ValueType</a></code>
            </td>
            <td><p>kVector2 or kNone.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### BindMeshBuffersCmd {#BindMeshBuffersCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#636)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>mesh_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>index_buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>index_format</code></td>
            <td>
                <code><a class='link' href='#MeshIndexFormat'>MeshIndexFormat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>index_offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>index_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vertex_buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vertex_format</code></td>
            <td>
                <code><a class='link' href='#MeshVertexFormat'>MeshVertexFormat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vertex_offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vertex_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bounding_box</code></td>
            <td>
                <code><a class='link' href='#BoundingBox'>BoundingBox</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddLayerCmd {#AddLayerCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#655)*



<p>Add a layer to a layer stack.
Constraints:</p>
<ul>
<li><code>layer_stack_id</code> refs a <code>LayerStack</code>.</li>
<li><code>layer_id</code> refs a <code>Layer</code>.</li>
<li>The layer must not already belong to a different stack; it must first be
detached.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>layer_stack_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RemoveLayerCmd {#RemoveLayerCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#665)*



<p>Remove a layer from a layer stack.
Constraints:</p>
<ul>
<li><code>layer_stack_id</code> refs a <code>LayerStack</code>.</li>
<li><code>layer_id</code> refs a <code>Layer</code>.</li>
<li>The layer must belong to this stack.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>layer_stack_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RemoveAllLayersCmd {#RemoveAllLayersCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#673)*



<p>Remove all layers from a layer stack.
Constraints</p>
<ul>
<li><code>layer_stack_id</code> refs a <code>LayerStack</code>.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>layer_stack_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetLayerStackCmd {#SetLayerStackCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#681)*



<p>Set a compositor's layer stack, replacing the current stack (if any).
Constraints:</p>
<ul>
<li><code>compositor_id</code> refs a <code>DisplayCompositor</code> or <code>ImagePipeCompositor</code>.</li>
<li><code>layer_stack_id</code> refs a <code>LayerStack</code>.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>compositor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>layer_stack_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetRendererCmd {#SetRendererCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#690)*



<p>Set a layer's renderer, replacing the current renderer (if any).
Constraints:</p>
<ul>
<li><code>layer_id</code> refs a <code>Layer</code>.</li>
<li><code>renderer_id</code> refs a <code>Renderer</code>.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>layer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>renderer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetRendererParamCmd {#SetRendererParamCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#699)*



<p>Sets a parameter that affects how a renderer renders a scene.</p>
<p><code>renderer_id</code> refs the Renderer that is being modified.
<code>param</code> describes the parameter that should be set, and to what.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>renderer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>param</code></td>
            <td>
                <code><a class='link' href='#RendererParam'>RendererParam</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetEventMaskCmd {#SetEventMaskCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#713)*



<p>Sets which events a resource should deliver to the session listener.
This command replaces any prior event mask for the resource.</p>
<p>The initial event mask for a resource is zero, meaning no events are
reported.</p>
<p>Constraints:</p>
<ul>
<li><code>resource_id</code> is a valid resource id</li>
<li><code>event_mask</code> is zero or a combination of <code>k*EventMask</code> bits OR'ed together.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>event_mask</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetLabelCmd {#SetLabelCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#731)*



<p>Sets/clears a label to help developers identify the purpose of the resource
when using diagnostic tools.</p>
<p>The label serves no functional purpose in the scene graph.  It exists only
to help developers understand its structure.  The scene manager may truncate
or discard labels at will.</p>
<p>Constraints:</p>
<ul>
<li>The label's maximum length is <code>kLabelMaxLength</code> characters.</li>
<li>Setting the label to an empty string clears it.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetDisableClippingCmd {#SetDisableClippingCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#745)*



<p>Set whether clipping should be disabled for the specified renderer.  For a
newly-created renderer, clipping will NOT be disabled (i.e. it will be
enabled).</p>
<p>NOTE: this disables visual clipping only; objects are still clipped for the
purposes of hit-testing.</p>
<p><code>renderer_id</code> refs the target renderer.
<code>disable_clipping</code> specifies whether the clipping should be disabled.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>renderer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>disable_clipping</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetImportFocusCmdDEPRECATED {#SetImportFocusCmdDEPRECATED}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#751)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### SetClipPlanesCmd {#SetClipPlanesCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#759)*



<p>Sets the list of clip planes that apply to a Node and all of its children.  Replaces
the list set by any previous SetClipPlanesCmd.</p>
<ul>
<li><code>node_id</code> refs a <code>Node</code> with the has_clip characteristic.</li>
<li><code>clip_planes</code> is the new list of oriented clip planes.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>clip_planes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Plane3'>Plane3</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetPointLightPositionCmd {#SetPointLightPositionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#765)*



<p>Sets the position of the PointLight identified by <code>light_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>position</code></td>
            <td>
                <code><a class='link' href='#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetPointLightFalloffCmd {#SetPointLightFalloffCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#779)*



<p>Sets the falloff factor of the PointLight identified by <code>light_id</code>.
A value of 1.0 corresponds to the physically-based &quot;inverse-square law&quot;
(see Wikipedia).  Other values can be used for artistic effect, e.g. a
value of 0.0 means that the radiance of a surface is not dependant on
its distance from the light.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>falloff</code></td>
            <td>
                <code><a class='link' href='#FloatValue'>FloatValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SceneAddAmbientLightCmd {#SceneAddAmbientLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#786)*



<p>Adds the light specified by <code>light_id</code> specified by <code>light_id</code> to the scene
identified by <code>scene_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scene_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SceneAddDirectionalLightCmd {#SceneAddDirectionalLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#793)*



<p>Adds the light specified by <code>light_id</code> specified by <code>light_id</code> to the scene
identified by <code>scene_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scene_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SceneAddPointLightCmd {#SceneAddPointLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#800)*



<p>Adds the light specified by <code>light_id</code> specified by <code>light_id</code> to the scene
identified by <code>scene_id</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scene_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>light_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetDisplayColorConversionCmdHACK {#SetDisplayColorConversionCmdHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#819)*



<p>Set the color conversion applied to the compositor's display.
The conversion is applied to to each pixel according to the formula:</p>
<p>(matrix * (pixel + preoffsets)) + postoffsets</p>
<p>where pixel is a column vector consisting of the pixel's 3 components.</p>
<p><code>matrix</code> is passed in row-major order. Clients will be responsible
for passing default values, when needed.
Default values are not currently supported in fidl.
Default Values:
preoffsets = [0 0 0]
matrix = [1 0 0 0 1 0 0 0 1]
postoffsets = [0 0 0]</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>compositor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>preoffsets</code></td>
            <td>
                <code>float32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>matrix</code></td>
            <td>
                <code>float32[9]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>postoffsets</code></td>
            <td>
                <code>float32[3]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetDisplayRotationCmdHACK {#SetDisplayRotationCmdHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#837)*



<p>Depending on the device, the display might be rotated
with respect to what the lower level device controller
considers the physical orientation of pixels. The
compositors and layers must be in alignment with the
underlying physical orientation which means that for
certain operations like screenshotting, they cannot
provide results with the accurate orientation unless
they have information about how the higher-level display
is orienting the screen. The only legal values for the
rotation are 0, 90, 180, and 270, which are each
applied counterclockwise.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>compositor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rotation_degrees</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetEnableDebugViewBoundsCmd {#SetEnableDebugViewBoundsCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#845)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>enable</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetViewHolderBoundsColorCmd {#SetViewHolderBoundsColorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#852)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_holder_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>color</code></td>
            <td>
                <code><a class='link' href='#ColorRgbValue'>ColorRgbValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DisplayInfo {#DisplayInfo}
*Defined in [fuchsia.ui.gfx/display_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/display_info.fidl#8)*



<p>Provides information about a display.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width_in_px</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The size of the display, in physical pixels.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height_in_px</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MetricsEvent {#MetricsEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#42)*



<p>Provides rendering target metrics information about the specified node.</p>
<p>This event is delivered when the following conditions are true:</p>
<ul>
<li>The node is a descendant of a <code>Scene</code>.</li>
<li>The node has <code>kMetricsEventMask</code> set to an enabled state.</li>
<li>The node's metrics have changed since they were last delivered, or since
<code>kMetricsEventMask</code> transitioned from a disabled state to an enabled state.</li>
</ul>
<p>Subscribe to this event to receive information about the scale factors you
should apply when generating textures for your nodes.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code><a class='link' href='#Metrics'>Metrics</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SizeChangeHintEvent {#SizeChangeHintEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#57)*



<p>Delivered in response to a size change hint from a parent node
(SendSizeChangeHintCmd).</p>
<p>This event is delivered when the following conditions are true:</p>
<ul>
<li>The node has <code>kSizeChangeEventMask</code> set to an enabled state.</li>
<li>A parent node has sent a SendSizeChangeHintCmd.</li>
</ul>
<p>Subscribe to this event to receive information about how large textures you
will need in the near future for your nodes. The canonical use case is to
pre-allocate memory to avoid repeated re-allocations.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>node_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>width_change_factor</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height_change_factor</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImportUnboundEvent {#ImportUnboundEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#66)*



<p>Delivered when the imported resource with the given ID is no longer bound to
its host resource, or if the imported resource can not be bound because
the host resource is not available.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>resource_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewConnectedEvent {#ViewConnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#71)*



<p>Delivered to a ViewHolder's Session when its peer View is connected.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_holder_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewDisconnectedEvent {#ViewDisconnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#80)*



<p>Delivered to a ViewHolder's Session when its peer View is disconnected or
destroyed.</p>
<p>If the View is destroyed before the connection is established, then this
event will be delivered immediately when the ViewHolder attempts to connect.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_holder_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewHolderDisconnectedEvent {#ViewHolderDisconnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#89)*



<p>Delivered to a View's Session when its peer ViewHolder is disconnected or
destroyed.</p>
<p>If the ViewHolder is destroyed before the connection is established, then
this event will be delivered immediately when the View attempts to connect.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewHolderConnectedEvent {#ViewHolderConnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#97)*



<p>Delivered to a View's Session when its peer ViewHolder is connected.</p>
<p>If the ViewHolder is destroyed before the connection is established, then
this event will not be delivered.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewAttachedToSceneEvent {#ViewAttachedToSceneEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#107)*



<p>Delivered to a View's Session when the parent ViewHolder for the given View
becomes a part of a Scene.</p>
<p>A ViewHolder is considered to be part of a Scene if there is an unbroken
chain of parent-child relationships between the Scene node and the
ViewHolder node.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#ViewProperties'>ViewProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewDetachedFromSceneEvent {#ViewDetachedFromSceneEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#121)*



<p>Delivered to a View's Session when the parent ViewHolder for the given View
is no longer part of a scene.</p>
<p>This can happen if the ViewHolder is detached directly from the scene, or
if one of its parent nodes is.</p>
<p>A ViewHolder is considered to be part of a Scene if there is an unbroken
chain of parent-child relationships between the Scene node and the
ViewHolder node.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewPropertiesChangedEvent {#ViewPropertiesChangedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#127)*



<p>Delivered when the parent ViewHolder for the given View makes a change to
the View's properties.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>properties</code></td>
            <td>
                <code><a class='link' href='#ViewProperties'>ViewProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewStateChangedEvent {#ViewStateChangedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#133)*



<p>Delivered to a ViewHolder's Session when its peer View's state has changed.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>view_holder_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#ViewState'>ViewState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Hit {#Hit}
*Defined in [fuchsia.ui.gfx/hit.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/hit.fidl#16)*



<p>Describes where a hit occurred within the content of a node tagged
by this session.</p>
<p>To compute the point of intersection within the node's local coordinate
system, perform the following calculation using the ray which was
originally passed to <code>Session.HitTest()</code>.</p>
<p>hit_point = ray.origin + (hit.distance * ray.direction)
local_point = hit.inverse_transform * hit_point</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>tag_value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The node's tag value.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ray_origin</code></td>
            <td>
                <code><a class='link' href='#vec4'>vec4</a></code>
            </td>
            <td><p>The origin of the ray that was used for the hit test, in the hit
node's coordinate system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ray_direction</code></td>
            <td>
                <code><a class='link' href='#vec4'>vec4</a></code>
            </td>
            <td><p>The direction of the ray that was used for the hit test, in the hit
node's coordinate system.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>inverse_transform</code></td>
            <td>
                <code><a class='link' href='#mat4'>mat4</a></code>
            </td>
            <td><p>The inverse transformation matrix which maps the coordinate system of
the node at which the hit test was initiated into the local coordinate
system of the node which was hit.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>distance</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The distance from the ray's origin to the closest point of intersection
in multiples of the ray's direction vector.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ShapeNodeArgs {#ShapeNodeArgs}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#32)*



<p>Characteristics:</p>
<ul>
<li>has_parent</li>
<li>has_shape</li>
<li>has_material</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>unused</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### ClipNodeArgs {#ClipNodeArgs}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#41)*



<p>Characteristics:</p>
<ul>
<li>has_parent</li>
<li>is_clip</li>
<li>has_parts</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>unused</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### OpacityNodeArgsHACK {#OpacityNodeArgsHACK}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#52)*



<p>Characteristics:</p>
<ul>
<li>has_transform</li>
<li>has_parent</li>
<li>has_children</li>
<li>has_parts</li>
<li>has_opacity</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>unused</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### EntityNodeArgs {#EntityNodeArgs}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#62)*



<p>Characteristics:</p>
<ul>
<li>has_transform</li>
<li>has_children</li>
<li>has_parent</li>
<li>has_parts</li>
<li>has_clip</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>unused</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### ImagePipeArgs {#ImagePipeArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#67)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image_pipe_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImagePipe'>ImagePipe</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImagePipe2Args {#ImagePipe2Args}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#72)*



<p><code>ImagePipe2</code> is a <code>Resource</code> that can be used as a <code>Texture</code> for a <code>Material</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image_pipe_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImagePipe2'>ImagePipe2</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MemoryArgs {#MemoryArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#79)*



<p><code>Memory</code> is a <code>Resource</code> that wraps a client-provided Zircon vmo to register
it with Scenic.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>allocation_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>memory_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#MemoryType'>MemoryType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImageArgs {#ImageArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#93)*



<p>An image mapped to a range of a <code>Memory</code> resource.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImageInfo'>ImageInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>memory_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>memory_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BufferArgs {#BufferArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#101)*



<p>A buffer mapped to a range of <code>Memory</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>memory_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>memory_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>num_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewArgs {#ViewArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#118)*



<p>Represents the root of a subgraph within a larger scene graph.  Nodes can be
attached to the <code>View</code> as children, and these Nodes will have the <code>View</code>s'
coordinate transform applied to their own, in addition to being clipped to
the <code>View</code>s' bounding box.
See <code>ViewProperties</code>.</p>
<p>Each <code>View</code> is linked to a paired <code>ViewHolder</code> via a shared token pair.</p>
<p>Usually the <code>View</code> and its associated <code>ViewHolder</code> exist in separate
processes.  By combining them, the UI for an entire system can be built
using content contributed from many different processes.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewToken'>ViewToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewArgs2 {#ViewArgs2}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#123)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewToken'>ViewToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewArgs3 {#ViewArgs3}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#145)*



<p>Represents the root of a subgraph within a larger scene graph.  Nodes can be
attached to the |View| as children, and these Nodes will have the |View|s'
coordinate transform applied to their own, in addition to being clipped to
the |View|s' bounding box.
See |ViewProperties|.</p>
<p>Each |View| is linked to a paired |ViewHolder| via a shared token pair.</p>
<p>Usually the |View| and its associated |ViewHolder| exist in separate
processes.  By combining them, the UI for an entire system can be built
using content contributed from many different processes.</p>
<p>Clients self-identify their |View| with a |ViewRef|, which is a stable
identifier that may be cloned and passed to other components in a
feed-forward style. It is accompanied by a |ViewRefControl|, which Scenic
uses to signal |View| destruction across the system; the |ViewRefControl|
must be unique - do not clone it.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewToken'>ViewToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>control_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewRefControl'>ViewRefControl</a></code>
            </td>
            <td><p>|control_ref.reference| must have full rights (i.e., with signaling).</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewRef'>ViewRef</a></code>
            </td>
            <td><p>|view_ref.reference| must have basic rights (i.e., no signaling).</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewHolderArgs {#ViewHolderArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#163)*



<p>Represents an attachment point for a subgraph within a larger scene graph.
The <code>ViewHolder</code> can be attached to a Node as a child, and the contents of
the linked <code>View</code> will become a child of the Node as well.</p>
<p>Each <code>ViewHolder</code> is linked to a paired <code>View</code> via a shared token pair.</p>
<p>Usually the <code>ViewHolder</code> and its associated <code>View</code> exist in separate
processes.  By combining them, the UI for an entire system can be built
using content contributed from many different processes.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewHolderArgs2 {#ViewHolderArgs2}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#168)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>debug_name</code></td>
            <td>
                <code>string?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CompositorArgs {#CompositorArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#176)*



<p>A Compositor draws its <code>LayerStack</code> into a framebuffer provided by its
attached <code>Display</code>, if any.  If no display is attached, nothing is rendered.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### DisplayCompositorArgs {#DisplayCompositorArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#183)*



<p>A DisplayCompositor draws its attached <code>LayerStack</code> into an image that is
presented on a display.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### ImagePipeCompositorArgs {#ImagePipeCompositorArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#190)*



<p>An ImagePipeCompositor draws its attached <code>LayerStack</code> into an image that is
presented on an image-pipe.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/#ImagePipe'>ImagePipe</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LayerStackArgs {#LayerStackArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#201)*



<p>A LayerStack is a stack of layers that are attached to a Compositor, which
draws them in order of increasing Z-order (or rather, presents the illusion
of drawing them in that order: it may apply any optimizations that don't
affect the output).</p>
<p>Supported commands:</p>
<ul>
<li>AddLayer</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### LayerArgs {#LayerArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#220)*



<p>A Layer is a 2-dimensional image that is drawn by a Compositor.  The
contents of each Layer in a Layerstack are independent of each other.
A layer is not drawn unless it has a camera, texture, or color.</p>
<p>Supported commands:</p>
<ul>
<li>Detach</li>
<li>SetCamera</li>
<li>SetColor</li>
<li>SetTexture</li>
<li>SetSize (depth must be zero)</li>
<li>SetSize</li>
<li>SetTranslation (z component determines the relative Z-ordering of layers)</li>
<li>SetRotation (must rotate around Z-axis)</li>
<li>SetScale</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### SceneArgs {#SceneArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#231)*



<p>A Scene is the root of a scene-graph, and defines the rendering environment
(lighting, etc.) for the tree of nodes beneath it.</p>
<p>Supported commands:</p>
<ul>
<li>Add/RemoveLight</li>
<li>AddChild</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### CameraArgs {#CameraArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#243)*



<p>A Camera is used to render a Scene from a particular viewpoint.  This is
achieved by setting a Renderer to use the camera.</p>
<p>The following commands may be applied to a Camera:</p>
<ul>
<li>SetCameraTransform</li>
<li>SetCameraProjection</li>
<li>SetCameraPoseBuffer</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scene_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StereoCameraArgs {#StereoCameraArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#254)*



<p>A StereoCamera is a Camera that renders the scene in side-by-side stereo.</p>
<p>Any command which can be applied to a Camera can also be applied to a
StereoCamera.
Additional supported commands:</p>
<ul>
<li>SetStereoCameraProjection</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scene_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RendererArgs {#RendererArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#264)*



<p>A Renderer renders a Scene via a Camera.</p>
<p>Supported commands:</p>
<ul>
<li>SetCamera</li>
<li>SetRendererParam</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### AmbientLightArgs {#AmbientLightArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#274)*



<p>An AmbientLight is a Light that is is assumed to be everywhere in the scene,
in all directions.</p>
<p>Supported commands:</p>
<ul>
<li>SetLightColor</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### DirectionalLightArgs {#DirectionalLightArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#289)*



<p>A DirectionalLight is a Light that is emitted from a point at infinity.</p>
<p>Although the light is directional, the light has some amount of angular
dispersion (i.e., the light is not fully columnated). For simplicity, we
assume the dispersion of the light source is symmetric about the light's
primary direction.</p>
<p>Supported commands:</p>
<ul>
<li>SetLightColor</li>
<li>SetLightDirection</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### PointLightArgs {#PointLightArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#303)*



<p>A PointLight is a Light that emits light in all directions.  By default, the
intensity of the light falls off according to the physically based
&quot;inverse-square law&quot; (see Wikipedia), although it can be adjusted to other
values for artistic effect.</p>
<p>Supported commands:</p>
<ul>
<li>SetLightColor</li>
<li>SetPointLightPosition</li>
<li>SetPointLightFalloff</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### MaterialArgs {#MaterialArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#314)*



<p>Simple texture-mapped material.</p>
<p>Supported commands:</p>
<ul>
<li>SetTextureCmd: sets the texture, or it can be left as zero (no texture).
The texture can be an Image or ImagePipe.</li>
<li>SetColorCmd: sets the color.</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dummy</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### VariableArgs {#VariableArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#320)*



<p>Describes a typed, client-modifiable value.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#ValueType'>ValueType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>initial_value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RectangleArgs {#RectangleArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#11)*



<p>Rectangle centered at (0,0).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RoundedRectangleArgs {#RoundedRectangleArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#23)*



<p>RoundedRectangle centered at (0,0).  Legal parameter values must satisfy the
constraint that the flat sides of the rectangle have non-negative length.
In other words, the following constraints must hold:</p>
<ul>
<li>top_left_radius + top_right_radius &lt;= width</li>
<li>bottom_left_radius + bottom_right_radius &lt;= width</li>
<li>top_left_radius + bottom_left_radius &lt;= height</li>
<li>top_right_radius + bottom_right_radius &lt;= height</li>
</ul>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CircleArgs {#CircleArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>radius</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshArgs {#MeshArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#38)*



<p>A Mesh cannot be rendered until it has been bound to vertex/index buffers;
see BindMeshBuffersCmd.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ImportToken {#ImportToken}
*Defined in [fuchsia.ui.gfx/tokens.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/tokens.fidl#18)*



<p>Token that uniquely identifies an attachment point for a subgraph in the
global scene graph.  Each <code>ImportToken</code> has exactly one corresponding
<code>ExportToken</code>.</p>
<p>A Scenic client can reference contents from another client by creating a
typed resource using this token.  The other client must also create a
correspondingly typed resource using the corresponding <code>ExportToken</code>.</p>
<p>The exact nature of the inter-client reference depends on the specific
resources created from the tokens.  For example, creating a <code>ViewHolder</code>
resource from this token allows a client to embed another client's <code>View</code>.</p>


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

### ExportToken {#ExportToken}
*Defined in [fuchsia.ui.gfx/tokens.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/tokens.fidl#34)*



<p>Token that uniquely identifies a root point for a subgraph in the global
scene graph. Each <code>ExportToken</code> has exactly one corresponding <code>ImportToken</code>.</p>
<p>A Scenic client can have its contents referenced from another client by
creating a typed resource using this token.  The other client must also
create a correspondingly typed resource using the corresponding
<code>ImportToken</code>.</p>
<p>The exact nature of the inter-client reference depends on the specific
resources created from the tokens.  For example, creating a <code>View</code>
resource from this token allows everything attached to the <code>View</code> to be
embedded in another clients <code>ViewHolder</code>.</p>


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

### vec2 {#vec2}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#7)*





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

### vec3 {#vec3}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#12)*





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
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### vec4 {#vec4}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#18)*





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
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>w</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### mat4 {#mat4}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>matrix</code></td>
            <td>
                <code>float32[16]</code>
            </td>
            <td><p>Column major order.</p>
</td>
            <td>No default</td>
        </tr>
</table>

### ColorRgba {#ColorRgba}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#31)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>red</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>green</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>blue</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>alpha</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ColorRgb {#ColorRgb}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#38)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>red</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>green</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>blue</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Quaternion {#Quaternion}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#44)*





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
        </tr><tr>
            <td><code>z</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>w</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Plane3 {#Plane3}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#53)*



<p>Oriented plane described by a normal vector and a distance
from the origin along that vector.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dir</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>dist</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FactoredTransform {#FactoredTransform}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#58)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>translation</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scale</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>anchor</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td><p>Point around which rotation and scaling occur.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rotation</code></td>
            <td>
                <code><a class='link' href='#Quaternion'>Quaternion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FloatValue {#FloatValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#87)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a float32, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Vector2Value {#Vector2Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#96)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a vec2, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#vec2'>vec2</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Vector3Value {#Vector3Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#105)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a vec3, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Vector4Value {#Vector4Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#114)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a vec4, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#vec4'>vec4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Matrix4Value {#Matrix4Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#123)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a vec4, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#mat4'>mat4</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ColorRgbValue {#ColorRgbValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#132)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a ColorRgb, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#ColorRgb'>ColorRgb</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ColorRgbaValue {#ColorRgbaValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#141)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a ColorRgba, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#ColorRgba'>ColorRgba</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### QuaternionValue {#QuaternionValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#150)*



<p>A value that is specified explicitly by <code>value</code> if <code>variable_id</code> is zero,
or is the value produced by the resource identified by <code>variable_id</code>, e.g.
an animation or expression.  In the latter case, the value produced by the
resource must be a Quaternion, and <code>value</code> is ignored.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Quaternion'>Quaternion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Metrics {#Metrics}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#179)*



<p>Rendering target metrics associated with a node.
See also <code>MetricsEvent</code>.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scale_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>The ratio between the size of one logical pixel within the node's local
coordinate system and the size of one physical pixel of the rendering
target.</p>
<p>This scale factors change in relation to the resolution of the rendering
target and the scale transformations applied by containing nodes.
They are always strictly positive and non-zero.</p>
<p>For example, suppose the rendering target is a high resolution display
with a device pixel ratio of 2.0 meaning that each logical pixel
within the model corresponds to two physical pixels of the display.
Assuming no scale transformations affect the node, then its metrics event
will report a scale factor of 2.0.</p>
<p>Building on this example, if instead the node's parent applies a
scale transformation of 0.25 to the node, then the node's metrics event
will report a scale factor of 0.5 indicating that the node should render
its content at a reduced resolution and level of detail since a smaller
area of physical pixels (half the size in each dimension) will be rendered.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>scale_y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scale_z</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BoundingBox {#BoundingBox}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#207)*



<p>Represents an axis-aligned bounding box.  If any of the dimensions has a
negative extent (e.g. max.x &lt; min.x) then the bounding box is treated as
empty.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewProperties {#ViewProperties}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#213)*



<p>Represents the properties for a View.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bounding_box</code></td>
            <td>
                <code><a class='link' href='#BoundingBox'>BoundingBox</a></code>
            </td>
            <td><p>The View's bounding box extents can be defined as:
{ bounding_box.min + inset_from_min, bounding_box.max - inset_from_max }
Content contained within the View is clipped to this bounding box.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>inset_from_min</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td><p><code>insets_from_min</code> and <code>insets_from_max</code> specify the distances between the
view's bounding box and that of its parent.</p>
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>inset_from_max</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>focus_change</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether the View can receive a focus event; default is true.  When
false, and this View is eligible to receive a focus event, no
focus/unfocus event is actually sent to any View.</p>
</td>
            <td>true</td>
        </tr><tr>
            <td><code>downward_input</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether the View allows geometrically underlying Views to receive input;
default is true. When false, Scenic does not send input events to
underlying Views.</p>
</td>
            <td>true</td>
        </tr>
</table>

### ViewState {#ViewState}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#240)*



<p>Represents the state of a View in Scenic.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>is_rendering</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>Whether the View is rendering. Default is false. Delivered to the View's
corresponding ViewHolder after the View's first frame render request.</p>
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### MeshIndexFormat {#MeshIndexFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#621)*

<p>Set a mesh's indices and vertices.</p>
<p><code>mesh_id</code> refs the Mesh to be updated.
<code>index_buffer_id</code> refs a Buffer that contains the mesh indices.
<code>index_format</code> defines how the index buffer data is to be interpreted.
<code>index_offset</code> number of bytes from the start of the index Buffer.
<code>index_count</code> number of indices.
<code>vertex_buffer_id</code> refs a Buffer that contains the mesh vertices.
<code>vertex_format</code> defines how the vertex buffer data is to be interpreted.
<code>vertex_offset</code> number of bytes from the start of the vertex Buffer.
<code>vertex_count</code> number of vertices.
<code>bounding_box</code> must contain all vertices within the specified range.</p>
<p>The MeshVertexFormat defines which per-vertex attributes are provided by the
mesh, and the size of each attribute (and therefore the size of each vertex).
The attributes are ordered within the vertex in the same order that they
appear within the MeshVertexFormat struct.  For example, if the values are
kVector3, kNone and kVector2, then:</p>
<ul>
<li>each vertex has a position and UV-coordinates, but no surface normal.</li>
<li>the 3D position occupies bytes 0-11 (3 dimensions * 4 bytes per float32).</li>
<li>the UV coords occupy bytes 12-19, since no surface normal is provided.</li>
</ul>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kUint16</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kUint32</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### ShadowTechnique {#ShadowTechnique}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/renderer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/renderer.fidl#17)*

<p>Represents the shadow algorithm that the <code>Renderer</code> should use when lighting
the scene.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSHADOWED</code></td>
            <td><code>0</code></td>
            <td><p>No shadows.</p>
</td>
        </tr><tr>
            <td><code>SCREEN_SPACE</code></td>
            <td><code>1</code></td>
            <td><p>Default.  Screen-space, depth-buffer based shadows; SSDO-ish.</p>
</td>
        </tr><tr>
            <td><code>SHADOW_MAP</code></td>
            <td><code>2</code></td>
            <td><p>Basic shadow map.</p>
</td>
        </tr><tr>
            <td><code>MOMENT_SHADOW_MAP</code></td>
            <td><code>3</code></td>
            <td><p>Moment shadow map (see http:///momentsingraphics.de).</p>
</td>
        </tr><tr>
            <td><code>STENCIL_SHADOW_VOLUME</code></td>
            <td><code>4</code></td>
            <td><p>Stencil shadow volume.</p>
</td>
        </tr></table>

### RenderFrequency {#RenderFrequency}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/renderer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/renderer.fidl#30)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>WHEN_REQUESTED</code></td>
            <td><code>0</code></td>
            <td><p>Render only on when requested (i.e. when something triggers it).
Default behavior.</p>
</td>
        </tr><tr>
            <td><code>CONTINUOUSLY</code></td>
            <td><code>1</code></td>
            <td><p>Render one frame after another regardless of it it's needed.</p>
</td>
        </tr></table>

### ImportSpec {#ImportSpec}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#330)*

<p>Describes an exported resource that is to be imported by an
ImportResourceCmd.</p>
<p>NOTE: Currently just an enum of importable resource types, but may later be
expanded to express concepts like &quot;meshes with a particular vertex format&quot;.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NODE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### ValueType {#ValueType}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#155)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kNone</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>kVector1</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>kVector2</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>kVector3</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>kVector4</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>kMatrix4</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>kColorRgb</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>kColorRgba</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>kQuaternion</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>kFactoredTransform</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr></table>

### HitTestBehavior {#HitTestBehavior}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#169)*

<p>Describes how nodes interact with hit testings.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kDefault</code></td>
            <td><code>0</code></td>
            <td><p>Apply hit testing to the node's content, its parts, and its children.</p>
</td>
        </tr><tr>
            <td><code>kSuppress</code></td>
            <td><code>1</code></td>
            <td><p>Suppress hit testing of the node and everything it contains.</p>
</td>
        </tr></table>





## **UNIONS**

### Command {#Command}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#10)*

<p>Commands that are used to modify the state of a <code>Session</code>.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>create_resource</code></td>
            <td>
                <code><a class='link' href='#CreateResourceCmd'>CreateResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>release_resource</code></td>
            <td>
                <code><a class='link' href='#ReleaseResourceCmd'>ReleaseResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>export_resource</code></td>
            <td>
                <code><a class='link' href='#ExportResourceCmd'>ExportResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>import_resource</code></td>
            <td>
                <code><a class='link' href='#ImportResourceCmd'>ImportResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_tag</code></td>
            <td>
                <code><a class='link' href='#SetTagCmd'>SetTagCmd</a></code>
            </td>
            <td><p>Tagging commands.</p>
</td>
        </tr><tr>
            <td><code>detach</code></td>
            <td>
                <code><a class='link' href='#DetachCmd'>DetachCmd</a></code>
            </td>
            <td><p>Grouping commands.</p>
</td>
        </tr><tr>
            <td><code>set_translation</code></td>
            <td>
                <code><a class='link' href='#SetTranslationCmd'>SetTranslationCmd</a></code>
            </td>
            <td><p>Spatial commands.</p>
</td>
        </tr><tr>
            <td><code>set_scale</code></td>
            <td>
                <code><a class='link' href='#SetScaleCmd'>SetScaleCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_rotation</code></td>
            <td>
                <code><a class='link' href='#SetRotationCmd'>SetRotationCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_anchor</code></td>
            <td>
                <code><a class='link' href='#SetAnchorCmd'>SetAnchorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_size</code></td>
            <td>
                <code><a class='link' href='#SetSizeCmd'>SetSizeCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_opacity</code></td>
            <td>
                <code><a class='link' href='#SetOpacityCmd'>SetOpacityCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>send_size_change_hint_hack</code></td>
            <td>
                <code><a class='link' href='#SendSizeChangeHintCmdHACK'>SendSizeChangeHintCmdHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>add_child</code></td>
            <td>
                <code><a class='link' href='#AddChildCmd'>AddChildCmd</a></code>
            </td>
            <td><p>Node-specific commands.</p>
</td>
        </tr><tr>
            <td><code>add_part</code></td>
            <td>
                <code><a class='link' href='#AddPartCmd'>AddPartCmd</a></code>
            </td>
            <td><p>re-parenting?</p>
</td>
        </tr><tr>
            <td><code>detach_children</code></td>
            <td>
                <code><a class='link' href='#DetachChildrenCmd'>DetachChildrenCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_shape</code></td>
            <td>
                <code><a class='link' href='#SetShapeCmd'>SetShapeCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_material</code></td>
            <td>
                <code><a class='link' href='#SetMaterialCmd'>SetMaterialCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_clip</code></td>
            <td>
                <code><a class='link' href='#SetClipCmd'>SetClipCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_hit_test_behavior</code></td>
            <td>
                <code><a class='link' href='#SetHitTestBehaviorCmd'>SetHitTestBehaviorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_view_properties</code></td>
            <td>
                <code><a class='link' href='#SetViewPropertiesCmd'>SetViewPropertiesCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>take_snapshot_cmd</code></td>
            <td>
                <code><a class='link' href='#TakeSnapshotCmdDEPRECATED'>TakeSnapshotCmdDEPRECATED</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_camera</code></td>
            <td>
                <code><a class='link' href='#SetCameraCmd'>SetCameraCmd</a></code>
            </td>
            <td><p>Camera and lighting commands.</p>
</td>
        </tr><tr>
            <td><code>set_camera_transform</code></td>
            <td>
                <code><a class='link' href='#SetCameraTransformCmd'>SetCameraTransformCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_camera_projection</code></td>
            <td>
                <code><a class='link' href='#SetCameraProjectionCmd'>SetCameraProjectionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_stereo_camera_projection</code></td>
            <td>
                <code><a class='link' href='#SetStereoCameraProjectionCmd'>SetStereoCameraProjectionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_camera_pose_buffer</code></td>
            <td>
                <code><a class='link' href='#SetCameraPoseBufferCmd'>SetCameraPoseBufferCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_light_color</code></td>
            <td>
                <code><a class='link' href='#SetLightColorCmd'>SetLightColorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_light_direction</code></td>
            <td>
                <code><a class='link' href='#SetLightDirectionCmd'>SetLightDirectionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>add_light</code></td>
            <td>
                <code><a class='link' href='#AddLightCmd'>AddLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>detach_light</code></td>
            <td>
                <code><a class='link' href='#DetachLightCmd'>DetachLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>detach_lights</code></td>
            <td>
                <code><a class='link' href='#DetachLightsCmd'>DetachLightsCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_texture</code></td>
            <td>
                <code><a class='link' href='#SetTextureCmd'>SetTextureCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_color</code></td>
            <td>
                <code><a class='link' href='#SetColorCmd'>SetColorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bind_mesh_buffers</code></td>
            <td>
                <code><a class='link' href='#BindMeshBuffersCmd'>BindMeshBuffersCmd</a></code>
            </td>
            <td><p>Mesh commands.</p>
</td>
        </tr><tr>
            <td><code>add_layer</code></td>
            <td>
                <code><a class='link' href='#AddLayerCmd'>AddLayerCmd</a></code>
            </td>
            <td><p>Layer and renderer commands.</p>
</td>
        </tr><tr>
            <td><code>remove_layer</code></td>
            <td>
                <code><a class='link' href='#RemoveLayerCmd'>RemoveLayerCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>remove_all_layers</code></td>
            <td>
                <code><a class='link' href='#RemoveAllLayersCmd'>RemoveAllLayersCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_layer_stack</code></td>
            <td>
                <code><a class='link' href='#SetLayerStackCmd'>SetLayerStackCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_renderer</code></td>
            <td>
                <code><a class='link' href='#SetRendererCmd'>SetRendererCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_renderer_param</code></td>
            <td>
                <code><a class='link' href='#SetRendererParamCmd'>SetRendererParamCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_event_mask</code></td>
            <td>
                <code><a class='link' href='#SetEventMaskCmd'>SetEventMaskCmd</a></code>
            </td>
            <td><p>Events.</p>
</td>
        </tr><tr>
            <td><code>set_label</code></td>
            <td>
                <code><a class='link' href='#SetLabelCmd'>SetLabelCmd</a></code>
            </td>
            <td><p>Diagnostic commands.</p>
</td>
        </tr><tr>
            <td><code>set_disable_clipping</code></td>
            <td>
                <code><a class='link' href='#SetDisableClippingCmd'>SetDisableClippingCmd</a></code>
            </td>
            <td><p>Debugging commands.</p>
</td>
        </tr><tr>
            <td><code>set_import_focus</code></td>
            <td>
                <code><a class='link' href='#SetImportFocusCmdDEPRECATED'>SetImportFocusCmdDEPRECATED</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_clip_planes</code></td>
            <td>
                <code><a class='link' href='#SetClipPlanesCmd'>SetClipPlanesCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_point_light_position</code></td>
            <td>
                <code><a class='link' href='#SetPointLightPositionCmd'>SetPointLightPositionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_point_light_falloff</code></td>
            <td>
                <code><a class='link' href='#SetPointLightFalloffCmd'>SetPointLightFalloffCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene__add_ambient_light</code></td>
            <td>
                <code><a class='link' href='#SceneAddAmbientLightCmd'>SceneAddAmbientLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene__add_directional_light</code></td>
            <td>
                <code><a class='link' href='#SceneAddDirectionalLightCmd'>SceneAddDirectionalLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene__add_point_light</code></td>
            <td>
                <code><a class='link' href='#SceneAddPointLightCmd'>SceneAddPointLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_display_color_conversion</code></td>
            <td>
                <code><a class='link' href='#SetDisplayColorConversionCmdHACK'>SetDisplayColorConversionCmdHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_display_rotation</code></td>
            <td>
                <code><a class='link' href='#SetDisplayRotationCmdHACK'>SetDisplayRotationCmdHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_enable_view_debug_bounds</code></td>
            <td>
                <code><a class='link' href='#SetEnableDebugViewBoundsCmd'>SetEnableDebugViewBoundsCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_view_holder_bounds_color</code></td>
            <td>
                <code><a class='link' href='#SetViewHolderBoundsColorCmd'>SetViewHolderBoundsColorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_camera_clip_space_transform</code></td>
            <td>
                <code><a class='link' href='#SetCameraClipSpaceTransformCmd'>SetCameraClipSpaceTransformCmd</a></code>
            </td>
            <td></td>
        </tr></table>

### Event {#Event}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#14)*

<p>These are all of the types of events which can be reported by a <code>Session</code>.
Use <code>SetEventMaskCmd</code> to enable event delivery for a resource.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code><a class='link' href='#MetricsEvent'>MetricsEvent</a></code>
            </td>
            <td><p>Events which are controlled by a mask.</p>
</td>
        </tr><tr>
            <td><code>size_change_hint</code></td>
            <td>
                <code><a class='link' href='#SizeChangeHintEvent'>SizeChangeHintEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>import_unbound</code></td>
            <td>
                <code><a class='link' href='#ImportUnboundEvent'>ImportUnboundEvent</a></code>
            </td>
            <td><p>Events which are always delivered, regardless of mask.</p>
</td>
        </tr><tr>
            <td><code>view_connected</code></td>
            <td>
                <code><a class='link' href='#ViewConnectedEvent'>ViewConnectedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_disconnected</code></td>
            <td>
                <code><a class='link' href='#ViewDisconnectedEvent'>ViewDisconnectedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder_disconnected</code></td>
            <td>
                <code><a class='link' href='#ViewHolderDisconnectedEvent'>ViewHolderDisconnectedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_attached_to_scene</code></td>
            <td>
                <code><a class='link' href='#ViewAttachedToSceneEvent'>ViewAttachedToSceneEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_detached_from_scene</code></td>
            <td>
                <code><a class='link' href='#ViewDetachedFromSceneEvent'>ViewDetachedFromSceneEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_properties_changed</code></td>
            <td>
                <code><a class='link' href='#ViewPropertiesChangedEvent'>ViewPropertiesChangedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_state_changed</code></td>
            <td>
                <code><a class='link' href='#ViewStateChangedEvent'>ViewStateChangedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder_connected</code></td>
            <td>
                <code><a class='link' href='#ViewHolderConnectedEvent'>ViewHolderConnectedEvent</a></code>
            </td>
            <td></td>
        </tr></table>

### RendererParam {#RendererParam}
*Defined in [fuchsia.ui.gfx/renderer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/renderer.fidl#9)*

<p>These are all of the types of parameters that can be set to configure a
<code>Renderer</code>.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>shadow_technique</code></td>
            <td>
                <code><a class='link' href='#ShadowTechnique'>ShadowTechnique</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>render_frequency</code></td>
            <td>
                <code><a class='link' href='#RenderFrequency'>RenderFrequency</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>enable_debugging</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### ResourceArgs {#ResourceArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#12)*

<p>These are all of the types of resources that can be created within a
<code>Session</code>. Add new fields only to the bottom of the list.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>memory</code></td>
            <td>
                <code><a class='link' href='#MemoryArgs'>MemoryArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>image</code></td>
            <td>
                <code><a class='link' href='#ImageArgs'>ImageArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>image_pipe</code></td>
            <td>
                <code><a class='link' href='#ImagePipeArgs'>ImagePipeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='#BufferArgs'>BufferArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view</code></td>
            <td>
                <code><a class='link' href='#ViewArgs'>ViewArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder</code></td>
            <td>
                <code><a class='link' href='#ViewHolderArgs'>ViewHolderArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>rectangle</code></td>
            <td>
                <code><a class='link' href='#RectangleArgs'>RectangleArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>rounded_rectangle</code></td>
            <td>
                <code><a class='link' href='#RoundedRectangleArgs'>RoundedRectangleArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>circle</code></td>
            <td>
                <code><a class='link' href='#CircleArgs'>CircleArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>mesh</code></td>
            <td>
                <code><a class='link' href='#MeshArgs'>MeshArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>shape_node</code></td>
            <td>
                <code><a class='link' href='#ShapeNodeArgs'>ShapeNodeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>clip_node</code></td>
            <td>
                <code><a class='link' href='#ClipNodeArgs'>ClipNodeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>entity_node</code></td>
            <td>
                <code><a class='link' href='#EntityNodeArgs'>EntityNodeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>opacity_node</code></td>
            <td>
                <code><a class='link' href='#OpacityNodeArgsHACK'>OpacityNodeArgsHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>material</code></td>
            <td>
                <code><a class='link' href='#MaterialArgs'>MaterialArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>compositor</code></td>
            <td>
                <code><a class='link' href='#CompositorArgs'>CompositorArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>display_compositor</code></td>
            <td>
                <code><a class='link' href='#DisplayCompositorArgs'>DisplayCompositorArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>image_pipe_compositor</code></td>
            <td>
                <code><a class='link' href='#ImagePipeCompositorArgs'>ImagePipeCompositorArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>layer_stack</code></td>
            <td>
                <code><a class='link' href='#LayerStackArgs'>LayerStackArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>layer</code></td>
            <td>
                <code><a class='link' href='#LayerArgs'>LayerArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene</code></td>
            <td>
                <code><a class='link' href='#SceneArgs'>SceneArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>camera</code></td>
            <td>
                <code><a class='link' href='#CameraArgs'>CameraArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>stereo_camera</code></td>
            <td>
                <code><a class='link' href='#StereoCameraArgs'>StereoCameraArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>renderer</code></td>
            <td>
                <code><a class='link' href='#RendererArgs'>RendererArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>ambient_light</code></td>
            <td>
                <code><a class='link' href='#AmbientLightArgs'>AmbientLightArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>directional_light</code></td>
            <td>
                <code><a class='link' href='#DirectionalLightArgs'>DirectionalLightArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variable</code></td>
            <td>
                <code><a class='link' href='#VariableArgs'>VariableArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>point_light</code></td>
            <td>
                <code><a class='link' href='#PointLightArgs'>PointLightArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view2</code></td>
            <td>
                <code><a class='link' href='#ViewArgs2'>ViewArgs2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder2</code></td>
            <td>
                <code><a class='link' href='#ViewHolderArgs2'>ViewHolderArgs2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view3</code></td>
            <td>
                <code><a class='link' href='#ViewArgs3'>ViewArgs3</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>image_pipe2</code></td>
            <td>
                <code><a class='link' href='#ImagePipe2Args'>ImagePipe2Args</a></code>
            </td>
            <td></td>
        </tr></table>

### Value {#Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#66)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>vector1</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector2</code></td>
            <td>
                <code><a class='link' href='#vec2'>vec2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector3</code></td>
            <td>
                <code><a class='link' href='#vec3'>vec3</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector4</code></td>
            <td>
                <code><a class='link' href='#vec4'>vec4</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>matrix4x4</code></td>
            <td>
                <code><a class='link' href='#mat4'>mat4</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>color_rgba</code></td>
            <td>
                <code><a class='link' href='#ColorRgba'>ColorRgba</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>color_rgb</code></td>
            <td>
                <code><a class='link' href='#ColorRgb'>ColorRgb</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>degrees</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>Degrees of counter-clockwise rotation in the XY plane.</p>
</td>
        </tr><tr>
            <td><code>quaternion</code></td>
            <td>
                <code><a class='link' href='#Quaternion'>Quaternion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='#FactoredTransform'>FactoredTransform</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>ID of a value-producing resource (an animation or an expression).
The type of this value matches the type produced by the named resource.</p>
</td>
        </tr></table>







## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#719">kLabelMaxLength</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Maximum length for a resource label.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#9">kMetricsEventMask</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>Reports metrics information.
This event type is only reported for node resources.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#10">kSizeChangeHintEventMask</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    
</table>

