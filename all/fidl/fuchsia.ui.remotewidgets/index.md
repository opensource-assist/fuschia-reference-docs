Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.remotewidgets


## **PROTOCOLS**

## QuickUi {:#QuickUi}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#100)*

 Defines a protocol for a component to provide specs for building UI for
 quick settings or notifications, independent of any platform.

### GetSpec {:#GetSpec}

 Request [Spec] from the provider. The provider should return Spec
 whenever it is ready to. Until then this request remains outstanding,
 aka "hanging get". The provider can return completely different set of
 status on every invocation. The client can provide an optional [Value]
 to allow the provider to customize the returned UI spec. Typically,
 this value was part of previous [Spec] and identifies the part of
 [Spec] the user interacted with.

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

### NumberValue {:#NumberValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#17)*



 Represents a number type in a ui spec with an associated action.


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

### TextValue {:#TextValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#23)*



 Represents a string type in a ui spec with an associated action.


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

### ButtonValue {:#ButtonValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#29)*



 Represents a button type in a ui spec with an associated action.


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

### ProgressValue {:#ProgressValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#35)*



 Represents a progress indicator type in a ui spec with an associated action.


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

### InputValue {:#InputValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#42)*



 Represents an input type in a ui spec with an associated action.


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

### IconValue {:#IconValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#50)*



 Represents an icon type in a ui spec with an associated action.


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
                <code><a class='link' href='../fuchsia.fonts/index.html'>fuchsia.fonts</a>/<a class='link' href='../fuchsia.fonts/index.html#FamilyName'>FamilyName</a>?</code>
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

### GridValue {:#GridValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#57)*



 Represents a grid of strings type in a ui spec with an associated action.


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

### GraphValue {:#GraphValue}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#63)*



 Represents a graph type in a ui spec with an associated action.


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

### Group {:#Group}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#84)*



 Represents a group of [Value]s with a title.


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

### Spec {:#Spec}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#92)*



 Describes a specification of quick UI.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>groups</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Group'>Group</a>&gt;[8]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>







## **UNIONS**

### Number {:#Number}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#10)*

 The value to hold these numeric types.

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

### Value {:#Value}
*Defined in [fuchsia.ui.remotewidgets/quickui.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.remotewidgets/quickui.fidl#72)*

 Represents a Value that is union of all types.

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
        </tr></table>







