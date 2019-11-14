[TOC]

# fuchsia.ui.display


## **PROTOCOLS**

## DisplayListener {#DisplayListener}
*Defined in [fuchsia.ui.display/display_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#42)*

<p>Display Listener protocol implemented by clients.</p>

### OnDisplayAdded {#OnDisplayAdded}

<p>Called when displays are added. This method will also be called when
the listener is registered for any connected displays.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>display</code></td>
            <td>
                <code><a class='link' href='#Info'>Info</a></code>
            </td>
        </tr></table>



### OnDisplayRemoved {#OnDisplayRemoved}

<p>Called when displays are removed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>display</code></td>
            <td>
                <code><a class='link' href='#DisplayRef'>DisplayRef</a></code>
            </td>
        </tr></table>



### OnDisplayOwnershipChanged {#OnDisplayOwnershipChanged}

<p>Called when the client gains or loses ownership of the displays.</p>
<p>New clients should assume they do not have ownership of the display
until informed otherwise by this method. Ownership can be lost and
gained more than once.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>displays</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#DisplayRef'>DisplayRef</a>&gt;[1024]</code>
            </td>
        </tr><tr>
            <td><code>owned_by_display_controller</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## DisplayManager {#DisplayManager}
*Defined in [fuchsia.ui.display/display_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#63)*

<p>|DisplayManager| is a service that informs the client of new or removed
displays and allows changing of display configuration. Every display is
associated with a DisplayRef which can also be used as a parameter to other
apis (e.g. Scenic).</p>

### AddDisplayListener {#AddDisplayListener}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#DisplayListener'>DisplayListener</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### DisplayRef {#DisplayRef}
*Defined in [fuchsia.ui.display/display_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#13)*



<p>Unique identifier for a display.
Also serves as a capability, enabling the owner to perform certain
operations on displays in the DisplayManager protocol and other protocols
(like Scenic).</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>reference</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### Info {#Info}


*Defined in [fuchsia.ui.display/display_manager.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#27)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>display_ref</code></td>
            <td>
                <code><a class='link' href='#DisplayRef'>DisplayRef</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>modes</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.hardware.display/'>fuchsia.hardware.display</a>/<a class='link' href='../fuchsia.hardware.display/#Mode'>Mode</a>&gt;[256]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>manufacturer_name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>monitor_name</code></td>
            <td>
                <code>string[128]</code>
            </td>
            <td></td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#19">MODES_MAX_LEN</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#22">MODE_INTERLACED</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#24">IDENTIFIER_MAX_LEN</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.display/display_manager.fidl#39">DISPLAYS_MAX_LEN</a></td>
            <td>
                    <code>1024</code>
                </td>
                <td><code>int32</code></td>
            <td></td>
        </tr>
    
</table>

