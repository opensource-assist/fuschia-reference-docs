[TOC]

# fuchsia.ui.remotewidgets


## **PROTOCOLS**

## QuickUi {#QuickUi}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#128)*

<p>Defines a protocol for a component to provide specs for building UI for
quick settings or notifications, independent of any platform.</p>

### GetSpec {#GetSpec}

<p>Request [Spec] from the provider. The provider should return Spec
whenever it is ready to. Until then this request remains outstanding,
aka &quot;hanging get&quot;. The provider can return completely different set of
status on every invocation. The client can provide an optional [Value]
to allow the provider to customize the returned UI spec. Typically,
this value was part of previous [Spec] and identifies the part of
[Spec] the user interacted with.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a>?</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>spec</code></td>
            <td>
                <code><a class='link' href='#Spec'>Spec</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### NumberValue {#NumberValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#34)*



<p>Represents a number type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Number'>Number</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### TextValue {#TextValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#40)*



<p>Represents a string type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>text</code></td>
            <td>
                <code>string[64]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### ButtonValue {#ButtonValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#46)*



<p>Represents a button type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string[64]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### ProgressValue {#ProgressValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#52)*



<p>Represents a progress indicator type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### InputValue {#InputValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#59)*



<p>Represents an input type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>text</code></td>
            <td>
                <code>string[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>lines</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>1</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### IconValue {#IconValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#67)*



<p>Represents an icon type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>code_point</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>font_family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.fonts/'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/#FamilyName'>FamilyName</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### GridValue {#GridValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#74)*



<p>Represents a grid of strings type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>columns</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TextValue'>TextValue</a>&gt;[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### ListValue {#ListValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#80)*



<p>Represents a list of strings type in a ui spec.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>multiselect</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>false</td>
        </tr><tr>
            <td><code>popup</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>false</td>
        </tr><tr>
            <td><code>title</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>items</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#TextValue'>TextValue</a>&gt;[1024]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### GraphValue {#GraphValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#88)*



<p>Represents a graph type in a ui spec with an associated action.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>value</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>step</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### Group {#Group}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#110)*



<p>Represents a group of [Value]s with a title.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>title</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Value'>Value</a>&gt;[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Spec {#Spec}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#118)*



<p>Describes a specification of quick UI.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>title</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>groups</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Group'>Group</a>&gt;[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### QuickAction {#QuickAction}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#11)*

<p>Defines special actions that are used on Values to control QuickUi
navigation or provide extra semantics to actions associated with them.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DETAILS</code></td>
            <td><code>2147483648</code></td>
            <td><p>Can be set on a button spec. Tells the client to navigate to a details
view reserved exclusively for specs from this server.</p>
</td>
        </tr><tr>
            <td><code>CANCEL</code></td>
            <td><code>1073741824</code></td>
            <td><p>Can be set on a button spec. Tells the client to return to the previous
view and discard any changes in flight.</p>
</td>
        </tr><tr>
            <td><code>SUBMIT</code></td>
            <td><code>536870912</code></td>
            <td><p>Can be set on a button spec. Tells the client to return to the previous
view and send all changes in flight to the server.</p>
</td>
        </tr><tr>
            <td><code>SELECT</code></td>
            <td><code>268435456</code></td>
            <td><p>Can be set on a text spec used in a ListValue. Tells the client to
consider the associated list item as selected.</p>
</td>
        </tr></table>





## **UNIONS**

### Number {#Number}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#27)*

<p>The value to hold these numeric types.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>int_value</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint_value</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>double_value</code></td>
            <td>
                <code>float64</code>
            </td>
            <td></td>
        </tr></table>

### Value {#Value}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#97)*

<p>Represents a Value that is union of all types.</p>

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>number</code></td>
            <td>
                <code><a class='link' href='#NumberValue'>NumberValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code><a class='link' href='#TextValue'>TextValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>progress</code></td>
            <td>
                <code><a class='link' href='#ProgressValue'>ProgressValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>button</code></td>
            <td>
                <code><a class='link' href='#ButtonValue'>ButtonValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='#InputValue'>InputValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>icon</code></td>
            <td>
                <code><a class='link' href='#IconValue'>IconValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>grid</code></td>
            <td>
                <code><a class='link' href='#GridValue'>GridValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>graph</code></td>
            <td>
                <code><a class='link' href='#GraphValue'>GraphValue</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>list</code></td>
            <td>
                <code><a class='link' href='#ListValue'>ListValue</a></code>
            </td>
            <td></td>
        </tr></table>







