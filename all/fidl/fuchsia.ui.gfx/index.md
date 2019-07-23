Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.gfx


## **PROTOCOLS**

## SnapshotCallbackHACK {:#SnapshotCallbackHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#384)*


### OnData {:#OnData}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='../fuchsia.mem/index.html'>fuchsia.mem</a>/<a class='link' href='../fuchsia.mem/index.html#Buffer'>Buffer</a></code>
            </td>
        </tr></table>



## PoseBufferProvider {:#PoseBufferProvider}
*Defined in [fuchsia.ui.gfx/pose_buffer_provider.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/pose_buffer_provider.fidl#9)*

 A minimal fidl interface to allow sourcing the contents of a PoseBuffer from another service.

### SetPoseBuffer {:#SetPoseBuffer}

 Sets the PoseBuffer and the parameters PoseBufferProvider will use to fill that PoseBuffer.
 Setting this when it is already set will replace the previously set parameters with the new
 parameters, which will release the provider's reference to the buffer.

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

### CreateResourceCmd {:#CreateResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#101)*



 Instructs the compositor to create the specified `Resource`, and to register
 it in a table so that it can be referenced by subsequent commands.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> An ID that is currently not used within the session.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>resource</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ResourceArgs'>ResourceArgs</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ReleaseResourceCmd {:#ReleaseResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#114)*



 Releases the client's reference to the resource; it is then illegal to use
 the ID in subsequent Commands.  Other references to the resource may exist,
 so releasing the resource does not result in its immediate destruction; it is
 only destroyed once the last reference is released.  For example, the
 resource may be required to render an in-progress frame, or it may be
 referred to by another resource).  However, the ID will be immediately
 unregistered, and may be reused to create a new resource.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> ID of the resource to be dereferenced.
</td>
            <td>No default</td>
        </tr>
</table>

### ExportResourceCmd {:#ExportResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#127)*



 Create an external reference to the specified resource, which can then be
 imported into another Session by passing a handle to `token`'s peer to
 ImportResourceCmd; see that comment for more details.

 The importing client is typically in a different process than the exporter.
 No specific mechanism is provided for transferring a token from an exporter
 to an importer; collaborators may choose any out-of-band API they wish to do
 so.


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

### ImportResourceCmd {:#ImportResourceCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#154)*



 Import a resource that was exported via ExportResourceCmd().  `token` is
 a handle to the eventpair peer that was used to export the resource, and
 `spec` describes the type of the imported resource, and the commands which
 can legally be applied to it.  Afterward, `id` can be used to refer to the
 resource in an Command, similarly (but not identically: see below) to a
 resource that was created in the session.  For example, you can add children
 to an imported EntityNode via AddChildCmd.

 However, note that the importer does not gain full access to the imported
 resource, but rather to an attenuated subset of its capabilities.  For
 example, you cannot use a DetachCmd to detach an imported EntityNode from
 its parent.

 Unlike ExportResourceCmd, there is no configurable timeout.  There is an
 expectation that the exported resource will become available in a short
 amount of time.  TODO: this needs elaboration... e.g. we might notify via the
 SessionListener when we know that the link will never be made (e.g. if the
 peer of the import token is destroyed).



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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ImportSpec'>ImportSpec</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetTagCmd {:#SetTagCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#174)*



 Sets/clears a node's tag value.

 A session can apply a tag value to any node to which it has access, including
 imported nodes.  These tags are private to the session and cannot be read
 or modified by other sessions.  When multiple sessions import the same node,
 each session will only observe its own tag values.

 Hit test results for a session only include nodes which the session has
 tagged with a non-zero value.  Therefore a session can use tag values to
 associate nodes with their functional purpose when picked.

 Constraints:
 - `node_id` refs a `Node`.
 - `tag_value` is the tag value to assign, or 0 to remove the tag.


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

### DetachCmd {:#DetachCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#189)*



 Detaches a parentable object from its parent (e.g. a node from a parent node,
 or a layer from a layer stack).  It is illegal to apply this command to a
 non-parentable object.  No-op if the target object currently has no parent.

 Constraints:
 - `id` refs a parentable object

 Discussion:
 For nodes, this command will detach a node from its parent, regardless of
 whether it is a part or a child of its parent.


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

### SetTranslationCmd {:#SetTranslationCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#197)*



 Sets a Resource's (typically a Node's) translation.

 Constraints:
 - `id` refs a Resource with the has_transform characteristic.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetScaleCmd {:#SetScaleCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#206)*



 Sets a Resource's (typically a Node's) scale.

 Constraints:
 - `id` refs a Resource with the has_transform characteristic.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetRotationCmd {:#SetRotationCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#215)*



 Sets a Resource's (typically a Node's) rotation.

 Constraints:
 - `id` refs a Resource with the has_transform characteristic.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#QuaternionValue'>QuaternionValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetAnchorCmd {:#SetAnchorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#224)*



 Sets a Resource's (typically a Node's) anchor point.

 Constraints:
 - `id` refs a Resource with the has_transform characteristic.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetSizeCmd {:#SetSizeCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#235)*



 Sets an object's size.

 Constraints:
 - `id` refs a resizeable object.
 - some objects that support this command may have additional constraints
   (e.g. in some cases `depth` must be zero).


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector2Value'>Vector2Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetOpacityCmd {:#SetOpacityCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#245)*



 Sets a node's opacity.

 Constraints:
 - `node_id` refs a `Node` with the has_opacity characteristic.
 - `opacity` is in the range [0, 1].


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

### SendSizeChangeHintCmdHACK {:#SendSizeChangeHintCmdHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#256)*



 Sends a hint about a pending size change to the given node and all nodes
 below. This is generally sent before an animation.

 `width_change_factor` and `height_change_factor` is how much bigger or smaller
 the item is expected to be in the near future. This one number encapsulate
 both changes in scale, as well as changes to layout width and height.


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

### AddChildCmd {:#AddChildCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#271)*



 Add a node as a child to another node.

 Constraints:
 - `id` refs a Node with the has_children characteristic.
 - `child_id` refs any Node.

 Discussion:
 The child node is first removed from its existing parent, as if DetachCmd
 was applied first.


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

### AddPartCmd {:#AddPartCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#291)*



 Add a node as a part of another node.  The implications of being a part
 rather than a child differ based on the type of the part.  However, one
 implication is constant: removing all of a node's children (e.g. via
 DetachChildrenCmd) does not affect its parts.  This is similar to the
 "shadow DOM" in a web browser: the controls of a <video> element are
 implemented as using the shadow DOM, and do no show up amongst the children
 of that element.

 Constraints:
 - `id` refs a Node with the has_parts characteristic.
 - `part_id` refs any Node.

 Discussion:
 The part node is first removed from its existing parent, as if DetachCmd
 was applied first.


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

### DetachChildrenCmd {:#DetachChildrenCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#297)*



 Detaches all of a node's children (but not its parts).


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

### SetShapeCmd {:#SetShapeCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#315)*



 Sets/clears a node's shape.

 Constraints:
 - `node_id` refs a `Node` with the has_shape characteristic.
 - `shape_id` refs a `Shape`, or nothing.
 - if this command causes the target to have both a `Shape` and a `Material`,
   then these must be compatible with each other (see README.md regarding
   "Shape/Material Compatibility").

 Discussion:
 In order to be painted, a node requires both a `Shape` and a `Material`.
 Without a material, a node can still participate in hit-testing and clipping.
 Without a shape, a node cannot do any of the above.


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

### SetMaterialCmd {:#SetMaterialCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#334)*



 Sets/clears a node's material.

 Constraints:
 - `node_id` refs a `Node` with the has_material characteristic.
 - `material_id` refs a `Material`, or nothing.
 - if this command causes the target to have both a `Shape` and a `Material`,
   then these must be compatible with each other (see README.md regarding
   "Shape/Material Compatibility").

 Discussion:
 In order to be painted, a node requires both a `Shape` and a `Material`.
 Without a material, a node can still participate in hit-testing and clipping.
 Without a shape, a node cannot do any of the above.


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

### SetClipCmd {:#SetClipCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#359)*



 Sets/clears a node's clip.  DEPRECATED: use SetClipPlanesCmd.

 Constraints:
 - `node_id` refs a `Node` with the has_clip characteristic.
 - `clip_id` a `Node` with the is_clip characteristic, or nothing.  If the
   referenced node is not rooted, then it will have no effect (since its
   full world-transform cannot be determined).
 - `clip_to_self` If false, children are only clipped to the region specified
   by `clip_id`.  If true, children are additionally clipped to the node's
   shape (as determined by its ShapeNode parts).

 Discussion:
 If a node has a clip, it will be applied to both the parts and the children
 of the node.  Under some circumstances (TBD), a clip will not be applicable
 to a node; in such cases it will be as though no clip has been specified for
 the node.


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

### SetHitTestBehaviorCmd {:#SetHitTestBehaviorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#370)*



 Sets a node's hit test behavior.

 Discussion:
 By default, hit testing is performed on the node's content, its parts,
 and its children.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#HitTestBehavior'>HitTestBehavior</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetViewPropertiesCmd {:#SetViewPropertiesCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#379)*



 Sets the properties for a ViewHolder's attached View.

 Constraints:
 - `view_holder_id` refs a `ViewHolder`.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewProperties'>ViewProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TakeSnapshotCmdHACK {:#TakeSnapshotCmdHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#388)*





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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SnapshotCallbackHACK'>SnapshotCallbackHACK</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraCmd {:#SetCameraCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#399)*



 Sets a renderer's camera.

 Constraints:
 - `renderer_id` refs a `Renderer`.
 - `camera_id` refs a `Camera`, or stops rendering by passing zero.
 - `matrix` is a value or variable of type kMatrix4x4.


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

### SetCameraTransformCmd {:#SetCameraTransformCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#412)*



 Sets a camera's view matrix.
 This operation can be applied to both Cameras and StereoCameras.

 Constraints:
 - `camera_id` refs a `Camera`.
 - `eye_position` is the position of the eye.
 - `eye_look_at` is the point is the scene the that eye is pointed at.
 - `eye_up` defines the camera's "up" vector.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>eye_look_at</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>eye_up</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraProjectionCmd {:#SetCameraProjectionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#428)*



 Sets a camera's projection matrix.
 This operation cannot be applied to a StereoCamera.

 Constraints:
 - `camera_id` refs a `Camera` that is not a `StereoCamera`.
 - `fovy` is the Y-axis field of view, in radians.

 NOTE: A default orthographic projection is specified by setting `fovy` to
 zero.  In this case, the camera transform is ignored.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#FloatValue'>FloatValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetStereoCameraProjectionCmd {:#SetStereoCameraProjectionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#443)*



 Sets a StereoCamera's projection matrices.
 This operation can only be applied to a StereoCamera.

 Constraints:
 - `camera_id` refs a `StereoCamera`.
 - `left_projection` is the projection matrix for the left eye.
 - `right_projection` is the projection matrix for the right eye.

 These projection matrices may also contain a transform in camera space for
 their eye if needed.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Matrix4Value'>Matrix4Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>right_projection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Matrix4Value'>Matrix4Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetCameraPoseBufferCmd {:#SetCameraPoseBufferCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#521)*



 Sets the "pose buffer" for the camera identified by `camera_id`.
 This operation can be applied to both Cameras and StereoCameras.

 This will override any position and rotation set for the camera and will
 make it take its position and rotation from the pose buffer each frame
 based on the presentation time for that frame.

 A pose buffer represents a ring buffer of poses for a fixed number of time
 points in the future. Each entry in the buffer identified by `buffer_id` is
 a quaternion and a position layed out as follows:

 struct Pose {
   // Quaternion
   float32 a;
   float32 b;
   float32 c;
   float32 d;

   // Position
   float32 x;
   float32 y;
   float32 z;

   // Reserved/Padding
   byte[4] reserved;
 }

 The buffer can be thought of as a packed array of `num_entries` Pose structs
 and is required to be at least num_entries * sizeof(Pose) bytes.

 The quaternions and positions are specified in the space of the camera's
 parent node.

 `base_time` is a base time point expressed in nanoseconds in the
 `CLOCK_MONOTONIC` timebase and `time_interval` is the time in nanoseconds
 between entries in the buffer. `base_time` must be in the past.

 For a given point in time `t` expressed in nanoseconds in the
 `CLOCK_MONOTONIC` timebase the index of the corresponding pose in
 the pose buffer can be computed as follows:

 index(t) = ((t - base_time) / time_interval) % num_entries

 poses[index(t)] is valid for t over the time interval (t - time_interval, t]
 and should be expected to updated continuously without synchronization
 for the duration of that interval. If a single pose value is needed for
 multiple non-atomic operations a value should be latched and stored outside
 the pose buffer.

 Because the poses are not protected by any synchronization primitives it is
 possible that when a pose is latched it will be only partially updated, and
 the pose being read will contain some components from the pose before it is
 updated and some components from the updated pose. The safety of using these
 "torn" poses relies on two things:

 1) Sequential poses written to poses[index(t)] are very similar to each
 other numerically, so that if some components are taken from the first and
 some are taken from another the result is numerically similar to both

 2) The space of positions and quaternions is locally flat at the scale of
 changes between sequential updates, which guarantees that two poses which
 are numerically similar also represent semantically similar poses (i.e.
 there are no discontinuities which will cause a small numerical change in
 the position or quaterninon to cause a large change in the encoded pose)
 For positions this is guaranteed because Scenic uses a Euclidean 3-space
 which is globally flat and for quaternions this is guaranteed because
 quaternions encode rotation as points on a unit 4-sphere, and spheres are
 locally flat. For more details on the encoding of rotations in quaterions
 see https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation

 This commanderation is intended for late latching camera pose to support
 low-latency motion-tracked rendering.


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

### SetLightColorCmd {:#SetLightColorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#530)*



 Sets the color of the Light identified by `light_id`.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ColorRgbValue'>ColorRgbValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetLightDirectionCmd {:#SetLightDirectionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#536)*



 Sets the direction of the DirectionalLight identified by `light_id`.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddLightCmd {:#AddLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#544)*



 DEPRECATED
 Adds the light specified by `light_id` specified by `light_id` to the scene
 identified by `scene_id`.


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

### DetachLightCmd {:#DetachLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#551)*



 Detach the light specified by `light_id` from the scene that it is attached
 to, if any.


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

### DetachLightsCmd {:#DetachLightsCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#556)*



 Detach all lights from the scene specified by `scene_id`.


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

### SetTextureCmd {:#SetTextureCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#569)*



 Sets/clears a material's texture.

 Constraints:
 - `material_id` refs a `Material`.
 - `texture_id` refs a `Image`, `ImagePipe`, or nothing.

 If no texture is provided (i.e. `texture_id` is zero), a solid color is used.
 If a texture is provided, then the value sampled from the texture is
 multiplied by the color.


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

### SetColorCmd {:#SetColorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#581)*



 Sets a material's color.

 Constraints:
 - `material_id` refs a `Material`.

 If a texture is set on the material, then the value sampled from the texture
 is multiplied by the color.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ColorRgbaValue'>ColorRgbaValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshVertexFormat {:#MeshVertexFormat}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#613)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>position_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ValueType'>ValueType</a></code>
            </td>
            <td> kVector2 or kVector3.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>normal_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ValueType'>ValueType</a></code>
            </td>
            <td> kVector2 or kVector3 (must match position_type), or kNone.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>tex_coord_type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ValueType'>ValueType</a></code>
            </td>
            <td> kVector2 or kNone.
</td>
            <td>No default</td>
        </tr>
</table>

### BindMeshBuffersCmd {:#BindMeshBuffersCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#622)*





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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#MeshIndexFormat'>MeshIndexFormat</a></code>
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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#MeshVertexFormat'>MeshVertexFormat</a></code>
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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#BoundingBox'>BoundingBox</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AddLayerCmd {:#AddLayerCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#641)*



 Add a layer to a layer stack.
 Constraints:
 - `layer_stack_id` refs a `LayerStack`.
 - `layer_id` refs a `Layer`.
 - The layer must not already belong to a different stack; it must first be
   detached.


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

### RemoveLayerCmd {:#RemoveLayerCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#651)*



 Remove a layer from a layer stack.
 Constraints:
 - `layer_stack_id` refs a `LayerStack`.
 - `layer_id` refs a `Layer`.
 - The layer must belong to this stack.


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

### RemoveAllLayersCmd {:#RemoveAllLayersCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#659)*



 Remove all layers from a layer stack.
 Constraints
 - `layer_stack_id` refs a `LayerStack`.


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

### SetLayerStackCmd {:#SetLayerStackCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#667)*



 Set a compositor's layer stack, replacing the current stack (if any).
 Constraints:
 - `compositor_id` refs a `DisplayCompositor` or `ImagePipeCompositor`.
 - `layer_stack_id` refs a `LayerStack`.


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

### SetRendererCmd {:#SetRendererCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#676)*



 Set a layer's renderer, replacing the current renderer (if any).
 Constraints:
 - `layer_id` refs a `Layer`.
 - `renderer_id` refs a `Renderer`.


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

### SetRendererParamCmd {:#SetRendererParamCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#685)*



 Sets a parameter that affects how a renderer renders a scene.

 `renderer_id` refs the Renderer that is being modified.
 `param` describes the parameter that should be set, and to what.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#RendererParam'>RendererParam</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetEventMaskCmd {:#SetEventMaskCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#699)*



 Sets which events a resource should deliver to the session listener.
 This command replaces any prior event mask for the resource.

 The initial event mask for a resource is zero, meaning no events are
 reported.

 Constraints:
 - `resource_id` is a valid resource id
 - `event_mask` is zero or a combination of `k*EventMask` bits OR'ed together.


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

### SetLabelCmd {:#SetLabelCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#717)*



 Sets/clears a label to help developers identify the purpose of the resource
 when using diagnostic tools.

 The label serves no functional purpose in the scene graph.  It exists only
 to help developers understand its structure.  The scene manager may truncate
 or discard labels at will.

 Constraints:
 - The label's maximum length is `kLabelMaxLength` characters.
 - Setting the label to an empty string clears it.


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

### SetDisableClippingCmd {:#SetDisableClippingCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#731)*



 Set whether clipping should be disabled for the specified renderer.  For a
 newly-created renderer, clipping will NOT be disabled (i.e. it will be
 enabled).

 NOTE: this disables visual clipping only; objects are still clipped for the
 purposes of hit-testing.

 `renderer_id` refs the target renderer.
 `disable_clipping` specifies whether the clipping should be disabled.


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

### SetImportFocusCmdDEPRECATED {:#SetImportFocusCmdDEPRECATED}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#737)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### SetClipPlanesCmd {:#SetClipPlanesCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#745)*



 Sets the list of clip planes that apply to a Node and all of its children.  Replaces
 the list set by any previous SetClipPlanesCmd.

 - `node_id` refs a `Node` with the has_clip characteristic.
 - `clip_planes` is the new list of oriented clip planes.


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
                <code>vector&lt;<a class='link' href='../fuchsia.ui.gfx/index.html#Plane3'>Plane3</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetPointLightPositionCmd {:#SetPointLightPositionCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#751)*



 Sets the position of the PointLight identified by `light_id`.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Vector3Value'>Vector3Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetPointLightFalloffCmd {:#SetPointLightFalloffCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#765)*



 Sets the falloff factor of the PointLight identified by `light_id`.
 A value of 1.0 corresponds to the physically-based "inverse-square law"
 (see Wikipedia).  Other values can be used for artistic effect, e.g. a
 value of 0.0 means that the radiance of a surface is not dependant on
 its distance from the light.



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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#FloatValue'>FloatValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SceneAddAmbientLightCmd {:#SceneAddAmbientLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#772)*



 Adds the light specified by `light_id` specified by `light_id` to the scene
 identified by `scene_id`.


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

### SceneAddDirectionalLightCmd {:#SceneAddDirectionalLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#779)*



 Adds the light specified by `light_id` specified by `light_id` to the scene
 identified by `scene_id`.


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

### SceneAddPointLightCmd {:#SceneAddPointLightCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#786)*



 Adds the light specified by `light_id` specified by `light_id` to the scene
 identified by `scene_id`.


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

### SetDisplayColorConversionCmdHACK {:#SetDisplayColorConversionCmdHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#805)*



 Set the color conversion applied to the compositor's display.
 The conversion is applied to to each pixel according to the formula:

 (matrix * (pixel + preoffsets)) + postoffsets

 where pixel is a column vector consisting of the pixel's 3 components.

 `matrix` is passed in row-major order. Clients will be responsible
 for passing default values, when needed.
 Default values are not currently supported in fidl.
 Default Values:
   preoffsets = [0 0 0]
   matrix = [1 0 0 0 1 0 0 0 1]
   postoffsets = [0 0 0]


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

### SetDisplayRotationCmdHACK {:#SetDisplayRotationCmdHACK}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#823)*



 Depending on the device, the display might be rotated
 with respect to what the lower level device controller
 considers the physical orientation of pixels. The
 compositors and layers must be in alignment with the
 underlying physical orientation which means that for
 certain operations like screenshotting, they cannot
 provide results with the accurate orientation unless
 they have information about how the higher-level display
 is orienting the screen. The only legal values for the
 rotation are 0, 90, 180, and 270, which are each
  applied counterclockwise.


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

### SetEnableDebugViewBoundsCmd {:#SetEnableDebugViewBoundsCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#831)*





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

### SetViewHolderBoundsColorCmd {:#SetViewHolderBoundsColorCmd}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#838)*





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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ColorRgbValue'>ColorRgbValue</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DisplayInfo {:#DisplayInfo}
*Defined in [fuchsia.ui.gfx/display_info.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/display_info.fidl#8)*



 Provides information about a display.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width_in_px</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The size of the display, in physical pixels.
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

### MetricsEvent {:#MetricsEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#42)*



 Provides rendering target metrics information about the specified node.

 This event is delivered when the following conditions are true:
 - The node is a descendant of a `Scene`.
 - The node has `kMetricsEventMask` set to an enabled state.
 - The node's metrics have changed since they were last delivered, or since
   `kMetricsEventMask` transitioned from a disabled state to an enabled state.

 Subscribe to this event to receive information about the scale factors you
 should apply when generating textures for your nodes.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Metrics'>Metrics</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SizeChangeHintEvent {:#SizeChangeHintEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#57)*



 Delivered in response to a size change hint from a parent node
 (SendSizeChangeHintCmd).

 This event is delivered when the following conditions are true:
 - The node has `kSizeChangeEventMask` set to an enabled state.
 - A parent node has sent a SendSizeChangeHintCmd.

 Subscribe to this event to receive information about how large textures you
 will need in the near future for your nodes. The canonical use case is to
 pre-allocate memory to avoid repeated re-allocations.


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

### ImportUnboundEvent {:#ImportUnboundEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#66)*



 Delivered when the imported resource with the given ID is no longer bound to
 its host resource, or if the imported resource can not be bound because
 the host resource is not available.


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

### ViewConnectedEvent {:#ViewConnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#71)*



 Delivered to a ViewHolder's Session when its peer View is connected.


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

### ViewDisconnectedEvent {:#ViewDisconnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#80)*



 Delivered to a ViewHolder's Session when its peer View is disconnected or
 destroyed.

 If the View is destroyed before the connection is established, then this
 event will be delivered immediately when the ViewHolder attempts to connect.


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

### ViewHolderDisconnectedEvent {:#ViewHolderDisconnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#89)*



 Delivered to a View's Session when its peer ViewHolder is disconnected or
 destroyed.

 If the ViewHolder is destroyed before the connection is established, then
 this event will be delivered immediately when the View attempts to connect.


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

### ViewHolderConnectedEvent {:#ViewHolderConnectedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#97)*



 Delivered to a View's Session when its peer ViewHolder is connected.

 If the ViewHolder is destroyed before the connection is established, then
 this event will not be delivered.


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

### ViewAttachedToSceneEvent {:#ViewAttachedToSceneEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#107)*



 Delivered to a View's Session when the parent ViewHolder for the given View
 becomes a part of a Scene.

 A ViewHolder is considered to be part of a Scene if there is an unbroken
 chain of parent-child relationships between the Scene node and the
 ViewHolder node.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewProperties'>ViewProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewDetachedFromSceneEvent {:#ViewDetachedFromSceneEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#121)*



 Delivered to a View's Session when the parent ViewHolder for the given View
 is no longer part of a scene.

 This can happen if the ViewHolder is detached directly from the scene, or
 if one of its parent nodes is.

 A ViewHolder is considered to be part of a Scene if there is an unbroken
 chain of parent-child relationships between the Scene node and the
 ViewHolder node.


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

### ViewPropertiesChangedEvent {:#ViewPropertiesChangedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#127)*



 Delivered when the parent ViewHolder for the given View makes a change to
 the View's properties.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewProperties'>ViewProperties</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewStateChangedEvent {:#ViewStateChangedEvent}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#133)*



 Delivered to a ViewHolder's Session when its peer View's state has changed.


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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewState'>ViewState</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Hit {:#Hit}
*Defined in [fuchsia.ui.gfx/hit.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/hit.fidl#16)*



 Describes where a hit occurred within the content of a node tagged
 by this session.

 To compute the point of intersection within the node's local coordinate
 system, perform the following calculation using the ray which was
 originally passed to `Session.HitTest()`.

   hit_point = ray.origin + (hit.distance * ray.direction)
   local_point = hit.inverse_transform * hit_point


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>tag_value</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The node's tag value.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ray_origin</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec4'>vec4</a></code>
            </td>
            <td> The origin of the ray that was used for the hit test, in the hit
 node's coordinate system.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>ray_direction</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec4'>vec4</a></code>
            </td>
            <td> The direction of the ray that was used for the hit test, in the hit
 node's coordinate system.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>inverse_transform</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#mat4'>mat4</a></code>
            </td>
            <td> The inverse transformation matrix which maps the coordinate system of
 the node at which the hit test was initiated into the local coordinate
 system of the node which was hit.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>distance</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The distance from the ray's origin to the closest point of intersection
 in multiples of the ray's direction vector.
</td>
            <td>No default</td>
        </tr>
</table>

### ShapeNodeArgs {:#ShapeNodeArgs}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#32)*



 These are the types of nodes that can be created within a Scenic `Session`.

 All nodes have an associated transform, which distinguishes them from mere
 resources.  Nodes may also have one or more node Characteristics:

 These are characteristics that each type of `Node` either has or doesn't.
 These constrain operations that reference nodes; violations will cause the
 `Session` connection to be closed.  For example, `NodeAddChildOp` must target
 a node with the "has_children" characteristic.  These characteristics are not
 explicitly reflected in the Session API; instead, they must be enforced by
 implementations of the API.
 - has_children: The node can contain other nodes as children.
 - has_parent: The node can be a child of another node.  If this is false,
   the node can only be a direct descendant of its containing scene.
 - has_parts:  The node can contain other nodes as parts.  All parts must be
   from the same session as their parent.
 - has_clip:  The node can contain a clip node as a child.
 - is_clip:  The node can clip other nodes.
 - has_shape: The node can contain ShapeNodes as children.
 - has_material:  The node can have a Material resource applied to it.
 Characteristics:
 - has_parent
 - has_shape
 - has_material


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

### ClipNodeArgs {:#ClipNodeArgs}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#41)*



 Characteristics:
 - has_parent
 - is_clip
 - has_parts


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

### OpacityNodeArgsHACK {:#OpacityNodeArgsHACK}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#52)*



 Characteristics:
 - has_transform
 - has_parent
 - has_children
 - has_parts
 - has_opacity


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

### EntityNodeArgs {:#EntityNodeArgs}
*Defined in [fuchsia.ui.gfx/nodes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/nodes.fidl#62)*



 Characteristics:
 - has_transform
 - has_children
 - has_parent
 - has_parts
 - has_clip


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

### ImagePipeArgs {:#ImagePipeArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#66)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image_pipe_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#ImagePipe'>ImagePipe</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MemoryArgs {:#MemoryArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#73)*



 `Memory` is a `Resource` that wraps a client-provided Zircon vmo to register
 it with Scenic.


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
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#MemoryType'>MemoryType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ImageArgs {:#ImageArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#87)*



 An image mapped to a range of a `Memory` resource.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>info</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#ImageInfo'>ImageInfo</a></code>
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

### BufferArgs {:#BufferArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#95)*



 A buffer mapped to a range of `Memory`.


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

### ViewArgs {:#ViewArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#112)*



 Represents the root of a subgraph within a larger scene graph.  Nodes can be
 attached to the `View` as children, and these Nodes will have the `View`s'
 coordinate transform applied to their own, in addition to being clipped to
 the `View`s' bounding box.
 See `ViewProperties`.

 Each `View` is linked to a paired `ViewHolder` via a shared token pair.

 Usually the `View` and its associated `ViewHolder` exist in separate
 processes.  By combining them, the UI for an entire system can be built
 using content contributed from many different processes.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
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

### ViewArgs2 {:#ViewArgs2}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#117)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
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

### ViewArgs3 {:#ViewArgs3}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#139)*



 Represents the root of a subgraph within a larger scene graph.  Nodes can be
 attached to the |View| as children, and these Nodes will have the |View|s'
 coordinate transform applied to their own, in addition to being clipped to
 the |View|s' bounding box.
 See |ViewProperties|.

 Each |View| is linked to a paired |ViewHolder| via a shared token pair.

 Usually the |View| and its associated |ViewHolder| exist in separate
 processes.  By combining them, the UI for an entire system can be built
 using content contributed from many different processes.

 Clients self-identify their |View| with a |ViewRef|, which is a stable
 identifier that may be cloned and passed to other components in a
 feed-forward style. It is accompanied by a |ViewRefControl|, which Scenic
 uses to signal |View| destruction across the system; the |ViewRefControl|
 must be unique - do not clone it.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewToken'>ViewToken</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>control_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewRefControl'>ViewRefControl</a></code>
            </td>
            <td> |control_ref.reference| must have full rights (i.e., with signaling).
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>view_ref</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewRef'>ViewRef</a></code>
            </td>
            <td> |view_ref.reference| must have basic rights (i.e., no signaling).
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

### ViewHolderArgs {:#ViewHolderArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#157)*



 Represents an attachment point for a subgraph within a larger scene graph.
 The `ViewHolder` can be attached to a Node as a child, and the contents of
 the linked `View` will become a child of the Node as well.

 Each `ViewHolder` is linked to a paired `View` via a shared token pair.

 Usually the `ViewHolder` and its associated `View` exist in separate
 processes.  By combining them, the UI for an entire system can be built
 using content contributed from many different processes.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
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

### ViewHolderArgs2 {:#ViewHolderArgs2}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#162)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/index.html'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/index.html#ViewHolderToken'>ViewHolderToken</a></code>
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

### CompositorArgs {:#CompositorArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#170)*



 A Compositor draws its `LayerStack` into a framebuffer provided by its
 attached `Display`, if any.  If no display is attached, nothing is rendered.


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

### DisplayCompositorArgs {:#DisplayCompositorArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#177)*



 A DisplayCompositor draws its attached `LayerStack` into an image that is
 presented on a display.


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

### ImagePipeCompositorArgs {:#ImagePipeCompositorArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#184)*



 An ImagePipeCompositor draws its attached `LayerStack` into an image that is
 presented on an image-pipe.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>target</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#ImagePipe'>ImagePipe</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### LayerStackArgs {:#LayerStackArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#195)*



 A LayerStack is a stack of layers that are attached to a Compositor, which
 draws them in order of increasing Z-order (or rather, presents the illusion
 of drawing them in that order: it may apply any optimizations that don't
 affect the output).

 Supported commands:
 - AddLayer


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

### LayerArgs {:#LayerArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#214)*



 A Layer is a 2-dimensional image that is drawn by a Compositor.  The
 contents of each Layer in a Layerstack are independent of each other.
 A layer is not drawn unless it has a camera, texture, or color.

 Supported commands:
 - Detach
 - SetCamera
 - SetColor
 - SetTexture
 - SetSize (depth must be zero)
 - SetSize
 - SetTranslation (z component determines the relative Z-ordering of layers)
 - SetRotation (must rotate around Z-axis)
 - SetScale


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

### SceneArgs {:#SceneArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#225)*



 A Scene is the root of a scene-graph, and defines the rendering environment
 (lighting, etc.) for the tree of nodes beneath it.

 Supported commands:
 - Add/RemoveLight
 - AddChild


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

### CameraArgs {:#CameraArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#237)*



 A Camera is used to render a Scene from a particular viewpoint.  This is
 achieved by setting a Renderer to use the camera.

 The following commands may be applied to a Camera:
 - SetCameraTransform
 - SetCameraProjection
 - SetCameraPoseBuffer


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

### StereoCameraArgs {:#StereoCameraArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#248)*



 A StereoCamera is a Camera that renders the scene in side-by-side stereo.

 Any command which can be applied to a Camera can also be applied to a
 StereoCamera.
 Additional supported commands:
 - SetStereoCameraProjection


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

### RendererArgs {:#RendererArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#258)*



 A Renderer renders a Scene via a Camera.

 Supported commands:
 - SetCamera
 - SetRendererParam


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

### AmbientLightArgs {:#AmbientLightArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#268)*



 An AmbientLight is a Light that is is assumed to be everywhere in the scene,
 in all directions.

 Supported commands:
 - SetLightColor


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

### DirectionalLightArgs {:#DirectionalLightArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#283)*



 A DirectionalLight is a Light that is emitted from a point at infinity.

 Although the light is directional, the light has some amount of angular
 dispersion (i.e., the light is not fully columnated). For simplicity, we
 assume the dispersion of the light source is symmetric about the light's
 primary direction.

 Supported commands:
 - SetLightColor
 - SetLightDirection


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

### PointLightArgs {:#PointLightArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#297)*



 A PointLight is a Light that emits light in all directions.  By default, the
 intensity of the light falls off according to the physically based
 "inverse-square law" (see Wikipedia), although it can be adjusted to other
 values for artistic effect.

 Supported commands:
 - SetLightColor
 - SetPointLightPosition
 - SetPointLightFalloff


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

### MaterialArgs {:#MaterialArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#308)*



 Simple texture-mapped material.

 Supported commands:
 - SetTextureCmd: sets the texture, or it can be left as zero (no texture).
   The texture can be an Image or ImagePipe.
 - SetColorCmd: sets the color.


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

### VariableArgs {:#VariableArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#314)*



 Describes a typed, client-modifiable value.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ValueType'>ValueType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>initial_value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RectangleArgs {:#RectangleArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#11)*



 The shapes defined in this file can be used to define the rendered shape of
 an `ObjectNode`, and to define the clip region of a `ClipNode`.
 Rectangle centered at (0,0).


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RoundedRectangleArgs {:#RoundedRectangleArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#23)*



 RoundedRectangle centered at (0,0).  Legal parameter values must satisfy the
 constraint that the flat sides of the rectangle have non-negative length.
 In other words, the following constraints must hold:
   - top_left_radius + top_right_radius <= width
   - bottom_left_radius + bottom_right_radius <= width
   - top_left_radius + bottom_left_radius <= height
   - top_right_radius + bottom_right_radius <= height


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>width</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_left_radius</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>top_right_radius</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_right_radius</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bottom_left_radius</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### CircleArgs {:#CircleArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#32)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>radius</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MeshArgs {:#MeshArgs}
*Defined in [fuchsia.ui.gfx/shapes.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/shapes.fidl#38)*



 A Mesh cannot be rendered until it has been bound to vertex/index buffers;
 see BindMeshBuffersCmd.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### ImportToken {:#ImportToken}
*Defined in [fuchsia.ui.gfx/tokens.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/tokens.fidl#18)*



 Token that uniquely identifies an attachment point for a subgraph in the
 global scene graph.  Each `ImportToken` has exactly one corresponding
 `ExportToken`.

 A Scenic client can reference contents from another client by creating a
 typed resource using this token.  The other client must also create a
 correspondingly typed resource using the corresponding `ExportToken`.

 The exact nature of the inter-client reference depends on the specific
 resources created from the tokens.  For example, creating a `ViewHolder`
 resource from this token allows a client to embed another client's `View`.


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

### ExportToken {:#ExportToken}
*Defined in [fuchsia.ui.gfx/tokens.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/tokens.fidl#34)*



 Token that uniquely identifies a root point for a subgraph in the global
 scene graph. Each `ExportToken` has exactly one corresponding `ImportToken`.

 A Scenic client can have its contents referenced from another client by
 creating a typed resource using this token.  The other client must also
 create a correspondingly typed resource using the corresponding
 `ImportToken`.

 The exact nature of the inter-client reference depends on the specific
 resources created from the tokens.  For example, creating a `View`
 resource from this token allows everything attached to the `View` to be
 embedded in another clients `ViewHolder`.


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

### vec2 {:#vec2}
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

### vec3 {:#vec3}
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

### vec4 {:#vec4}
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

### mat4 {:#mat4}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>matrix</code></td>
            <td>
                <code>float32[16]</code>
            </td>
            <td> Column major order.
</td>
            <td>No default</td>
        </tr>
</table>

### ColorRgba {:#ColorRgba}
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

### ColorRgb {:#ColorRgb}
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

### Quaternion {:#Quaternion}
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

### Plane3 {:#Plane3}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#53)*



 Oriented plane described by a normal vector and a distance
 from the origin along that vector.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>dir</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
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

### FactoredTransform {:#FactoredTransform}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#58)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>translation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>scale</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>anchor</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td> Point around which rotation and scaling occur.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>rotation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Quaternion'>Quaternion</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### FloatValue {:#FloatValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#87)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a float32, and `value` is ignored.


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

### Vector2Value {:#Vector2Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#96)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a vec2, and `value` is ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec2'>vec2</a></code>
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

### Vector3Value {:#Vector3Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#105)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a vec3, and `value` is ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
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

### Vector4Value {:#Vector4Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#114)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a vec4, and `value` is ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec4'>vec4</a></code>
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

### Matrix4Value {:#Matrix4Value}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#123)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a vec4, and `value` is ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#mat4'>mat4</a></code>
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

### ColorRgbValue {:#ColorRgbValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#132)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a ColorRgb, and `value` is ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ColorRgb'>ColorRgb</a></code>
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

### ColorRgbaValue {:#ColorRgbaValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#141)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a ColorRgba, and `value` is ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ColorRgba'>ColorRgba</a></code>
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

### QuaternionValue {:#QuaternionValue}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#150)*



 A value that is specified explicitly by `value` if `variable_id` is zero,
 or is the value produced by the resource identified by `variable_id`, e.g.
 an animation or expression.  In the latter case, the value produced by the
 resource must be a Quaternion, and `value` is ignored.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Quaternion'>Quaternion</a></code>
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

### Metrics {:#Metrics}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#179)*



 Rendering target metrics associated with a node.
 See also `MetricsEvent`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scale_x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The ratio between the size of one logical pixel within the node's local
 coordinate system and the size of one physical pixel of the rendering
 target.

 This scale factors change in relation to the resolution of the rendering
 target and the scale transformations applied by containing nodes.
 They are always strictly positive and non-zero.

 For example, suppose the rendering target is a high resolution display
 with a device pixel ratio of 2.0 meaning that each logical pixel
 within the model corresponds to two physical pixels of the display.
 Assuming no scale transformations affect the node, then its metrics event
 will report a scale factor of 2.0.

 Building on this example, if instead the node's parent applies a
 scale transformation of 0.25 to the node, then the node's metrics event
 will report a scale factor of 0.5 indicating that the node should render
 its content at a reduced resolution and level of detail since a smaller
 area of physical pixels (half the size in each dimension) will be rendered.
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

### BoundingBox {:#BoundingBox}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#207)*



 Represents an axis-aligned bounding box.  If any of the dimensions has a
 negative extent (e.g. max.x < min.x) then the bounding box is treated as
 empty.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ViewProperties {:#ViewProperties}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#213)*



 Represents the properties for a View.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bounding_box</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#BoundingBox'>BoundingBox</a></code>
            </td>
            <td> The View's bounding box extents can be defined as:
    { bounding_box.min + inset_from_min, bounding_box.max - inset_from_max }
 Content contained within the View is clipped to this bounding box.

</td>
            <td>No default</td>
        </tr><tr>
            <td><code>inset_from_min</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td> `insets_from_min` and `insets_from_max` specify the distances between the
 view's bounding box and that of its parent.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>inset_from_max</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>focus_change</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the View can receive a focus event; default is true.  When
 false, and this View is eligible to receive a focus event, no
 focus/unfocus event is actually sent to any View.
</td>
            <td>true</td>
        </tr><tr>
            <td><code>downward_input</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the View allows geometrically underlying Views to receive input;
 default is true. When false, Scenic does not send input events to
 underlying Views.
</td>
            <td>true</td>
        </tr>
</table>

### ViewState {:#ViewState}
*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#240)*



 Represents the state of a View in Scenic.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>is_rendering</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the View is rendering. Default is false. Delivered to the View's
 corresponding ViewHolder after the View's first frame render request.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### MeshIndexFormat {:#MeshIndexFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#607)*

 Set a mesh's indices and vertices.

 `mesh_id` refs the Mesh to be updated.
 `index_buffer_id` refs a Buffer that contains the mesh indices.
 `index_format` defines how the index buffer data is to be interpreted.
 `index_offset` number of bytes from the start of the index Buffer.
 `index_count` number of indices.
 `vertex_buffer_id` refs a Buffer that contains the mesh vertices.
 `vertex_format` defines how the vertex buffer data is to be interpreted.
 `vertex_offset` number of bytes from the start of the vertex Buffer.
 `vertex_count` number of vertices.
 `bounding_box` must contain all vertices within the specified range.

 The MeshVertexFormat defines which per-vertex attributes are provided by the
 mesh, and the size of each attribute (and therefore the size of each vertex).
 The attributes are ordered within the vertex in the same order that they
 appear within the MeshVertexFormat struct.  For example, if the values are
 kVector3, kNone and kVector2, then:
   - each vertex has a position and UV-coordinates, but no surface normal.
   - the 3D position occupies bytes 0-11 (3 dimensions * 4 bytes per float32).
   - the UV coords occupy bytes 12-19, since no surface normal is provided.


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

### ShadowTechnique {:#ShadowTechnique}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/renderer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/renderer.fidl#17)*

 Represents the shadow algorithm that the `Renderer` should use when lighting
 the scene.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSHADOWED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>SCREEN_SPACE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SHADOW_MAP</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>MOMENT_SHADOW_MAP</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>STENCIL_SHADOW_VOLUME</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### RenderFrequency {:#RenderFrequency}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/renderer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/renderer.fidl#30)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>WHEN_REQUESTED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CONTINUOUSLY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### ImportSpec {:#ImportSpec}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#324)*

 Describes an exported resource that is to be imported by an
 ImportResourceCmd.

 NOTE: Currently just an enum of importable resource types, but may later be
 expanded to express concepts like "meshes with a particular vertex format".


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NODE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### ValueType {:#ValueType}
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

### HitTestBehavior {:#HitTestBehavior}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.gfx/types.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/types.fidl#169)*

 Describes how nodes interact with hit testings.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kDefault</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>kSuppress</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>





## **UNIONS**

### Command {:#Command}
*Defined in [fuchsia.ui.gfx/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#10)*

 Commands that are used to modify the state of a `Session`.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>create_resource</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#CreateResourceCmd'>CreateResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>release_resource</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ReleaseResourceCmd'>ReleaseResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>export_resource</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ExportResourceCmd'>ExportResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>import_resource</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ImportResourceCmd'>ImportResourceCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_tag</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetTagCmd'>SetTagCmd</a></code>
            </td>
            <td> Tagging commands.
</td>
        </tr><tr>
            <td><code>detach</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#DetachCmd'>DetachCmd</a></code>
            </td>
            <td> Grouping commands.
</td>
        </tr><tr>
            <td><code>set_translation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetTranslationCmd'>SetTranslationCmd</a></code>
            </td>
            <td> Spatial commands.
</td>
        </tr><tr>
            <td><code>set_scale</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetScaleCmd'>SetScaleCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_rotation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetRotationCmd'>SetRotationCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_anchor</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetAnchorCmd'>SetAnchorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_size</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetSizeCmd'>SetSizeCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_opacity</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetOpacityCmd'>SetOpacityCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>send_size_change_hint_hack</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SendSizeChangeHintCmdHACK'>SendSizeChangeHintCmdHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>add_child</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#AddChildCmd'>AddChildCmd</a></code>
            </td>
            <td> Node-specific commands.
</td>
        </tr><tr>
            <td><code>add_part</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#AddPartCmd'>AddPartCmd</a></code>
            </td>
            <td> re-parenting?
</td>
        </tr><tr>
            <td><code>detach_children</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#DetachChildrenCmd'>DetachChildrenCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_shape</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetShapeCmd'>SetShapeCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_material</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetMaterialCmd'>SetMaterialCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_clip</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetClipCmd'>SetClipCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_hit_test_behavior</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetHitTestBehaviorCmd'>SetHitTestBehaviorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_view_properties</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetViewPropertiesCmd'>SetViewPropertiesCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>take_snapshot_cmd</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#TakeSnapshotCmdHACK'>TakeSnapshotCmdHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_camera</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetCameraCmd'>SetCameraCmd</a></code>
            </td>
            <td> Camera and lighting commands.
</td>
        </tr><tr>
            <td><code>set_camera_transform</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetCameraTransformCmd'>SetCameraTransformCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_camera_projection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetCameraProjectionCmd'>SetCameraProjectionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_stereo_camera_projection</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetStereoCameraProjectionCmd'>SetStereoCameraProjectionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_camera_pose_buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetCameraPoseBufferCmd'>SetCameraPoseBufferCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_light_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetLightColorCmd'>SetLightColorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_light_direction</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetLightDirectionCmd'>SetLightDirectionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>add_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#AddLightCmd'>AddLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>detach_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#DetachLightCmd'>DetachLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>detach_lights</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#DetachLightsCmd'>DetachLightsCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_texture</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetTextureCmd'>SetTextureCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetColorCmd'>SetColorCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bind_mesh_buffers</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#BindMeshBuffersCmd'>BindMeshBuffersCmd</a></code>
            </td>
            <td> Mesh commands.
</td>
        </tr><tr>
            <td><code>add_layer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#AddLayerCmd'>AddLayerCmd</a></code>
            </td>
            <td> Layer and renderer commands.
</td>
        </tr><tr>
            <td><code>remove_layer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#RemoveLayerCmd'>RemoveLayerCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>remove_all_layers</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#RemoveAllLayersCmd'>RemoveAllLayersCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_layer_stack</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetLayerStackCmd'>SetLayerStackCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_renderer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetRendererCmd'>SetRendererCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_renderer_param</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetRendererParamCmd'>SetRendererParamCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_event_mask</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetEventMaskCmd'>SetEventMaskCmd</a></code>
            </td>
            <td> Events.
</td>
        </tr><tr>
            <td><code>set_label</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetLabelCmd'>SetLabelCmd</a></code>
            </td>
            <td> Diagnostic commands.
</td>
        </tr><tr>
            <td><code>set_disable_clipping</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetDisableClippingCmd'>SetDisableClippingCmd</a></code>
            </td>
            <td> Debugging commands.
</td>
        </tr><tr>
            <td><code>set_import_focus</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetImportFocusCmdDEPRECATED'>SetImportFocusCmdDEPRECATED</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_clip_planes</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetClipPlanesCmd'>SetClipPlanesCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_point_light_position</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetPointLightPositionCmd'>SetPointLightPositionCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_point_light_falloff</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetPointLightFalloffCmd'>SetPointLightFalloffCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene__add_ambient_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SceneAddAmbientLightCmd'>SceneAddAmbientLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene__add_directional_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SceneAddDirectionalLightCmd'>SceneAddDirectionalLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene__add_point_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SceneAddPointLightCmd'>SceneAddPointLightCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_display_color_conversion</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetDisplayColorConversionCmdHACK'>SetDisplayColorConversionCmdHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_display_rotation</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetDisplayRotationCmdHACK'>SetDisplayRotationCmdHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_enable_view_debug_bounds</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetEnableDebugViewBoundsCmd'>SetEnableDebugViewBoundsCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_view_holder_bounds_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SetViewHolderBoundsColorCmd'>SetViewHolderBoundsColorCmd</a></code>
            </td>
            <td></td>
        </tr></table>

### Event {:#Event}
*Defined in [fuchsia.ui.gfx/events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#14)*

 These are all of the types of events which can be reported by a `Session`.
 Use `SetEventMaskCmd` to enable event delivery for a resource.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>metrics</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#MetricsEvent'>MetricsEvent</a></code>
            </td>
            <td> Events which are controlled by a mask.
</td>
        </tr><tr>
            <td><code>size_change_hint</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SizeChangeHintEvent'>SizeChangeHintEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>import_unbound</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ImportUnboundEvent'>ImportUnboundEvent</a></code>
            </td>
            <td> Events which are always delivered, regardless of mask.
</td>
        </tr><tr>
            <td><code>view_connected</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewConnectedEvent'>ViewConnectedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_disconnected</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewDisconnectedEvent'>ViewDisconnectedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder_disconnected</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewHolderDisconnectedEvent'>ViewHolderDisconnectedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_attached_to_scene</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewAttachedToSceneEvent'>ViewAttachedToSceneEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_detached_from_scene</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewDetachedFromSceneEvent'>ViewDetachedFromSceneEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_properties_changed</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewPropertiesChangedEvent'>ViewPropertiesChangedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_state_changed</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewStateChangedEvent'>ViewStateChangedEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder_connected</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewHolderConnectedEvent'>ViewHolderConnectedEvent</a></code>
            </td>
            <td></td>
        </tr></table>

### RendererParam {:#RendererParam}
*Defined in [fuchsia.ui.gfx/renderer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/renderer.fidl#9)*

 These are all of the types of parameters that can be set to configure a
 `Renderer`.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>shadow_technique</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ShadowTechnique'>ShadowTechnique</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>render_frequency</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#RenderFrequency'>RenderFrequency</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>enable_debugging</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### ResourceArgs {:#ResourceArgs}
*Defined in [fuchsia.ui.gfx/resources.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/resources.fidl#12)*

 These are all of the types of resources that can be created within a
 `Session`.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>memory</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#MemoryArgs'>MemoryArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>image</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ImageArgs'>ImageArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>image_pipe</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ImagePipeArgs'>ImagePipeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#BufferArgs'>BufferArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewArgs'>ViewArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewHolderArgs'>ViewHolderArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>rectangle</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#RectangleArgs'>RectangleArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>rounded_rectangle</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#RoundedRectangleArgs'>RoundedRectangleArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>circle</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#CircleArgs'>CircleArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>mesh</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#MeshArgs'>MeshArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>shape_node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ShapeNodeArgs'>ShapeNodeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>clip_node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ClipNodeArgs'>ClipNodeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>entity_node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#EntityNodeArgs'>EntityNodeArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>opacity_node</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#OpacityNodeArgsHACK'>OpacityNodeArgsHACK</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>material</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#MaterialArgs'>MaterialArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>compositor</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#CompositorArgs'>CompositorArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>display_compositor</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#DisplayCompositorArgs'>DisplayCompositorArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>image_pipe_compositor</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ImagePipeCompositorArgs'>ImagePipeCompositorArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>layer_stack</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#LayerStackArgs'>LayerStackArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>layer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#LayerArgs'>LayerArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scene</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#SceneArgs'>SceneArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>camera</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#CameraArgs'>CameraArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>stereo_camera</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#StereoCameraArgs'>StereoCameraArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>renderer</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#RendererArgs'>RendererArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>ambient_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#AmbientLightArgs'>AmbientLightArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>directional_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#DirectionalLightArgs'>DirectionalLightArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variable</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#VariableArgs'>VariableArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>point_light</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#PointLightArgs'>PointLightArgs</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view2</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewArgs2'>ViewArgs2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view_holder2</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewHolderArgs2'>ViewHolderArgs2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>view3</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ViewArgs3'>ViewArgs3</a></code>
            </td>
            <td></td>
        </tr></table>

### Value {:#Value}
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
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec2'>vec2</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector3</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec3'>vec3</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>vector4</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#vec4'>vec4</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>matrix4x4</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#mat4'>mat4</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>color_rgba</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ColorRgba'>ColorRgba</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>color_rgb</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#ColorRgb'>ColorRgb</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>degrees</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Degrees of counter-clockwise rotation in the XY plane.
</td>
        </tr><tr>
            <td><code>quaternion</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#Quaternion'>Quaternion</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>transform</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.gfx/index.html#FactoredTransform'>FactoredTransform</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variable_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> ID of a value-producing resource (an animation or an expression).
 The type of this value matches the type produced by the named resource.
</td>
        </tr></table>







## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/commands.fidl#705">kLabelMaxLength</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#9">kMetricsEventMask</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.gfx/events.fidl#10">kSizeChangeHintEventMask</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

