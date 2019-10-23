[TOC]

# fuchsia.ui.policy.accessibility


## **PROTOCOLS**

## PointerEventRegistry {#PointerEventRegistry}
*Defined in [fuchsia.ui.policy.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy.accessibility/accessibility.fidl#10)*


### Register {#Register}

 Registers a listener with Scenic which will receive accessibility
 pointer events. These events will be handled by the accessibility
 listener, which will have the chance to either consume or reject them.
 If rejected, they will continue their normal flow. Only one listener can
 be registered.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pointer_event_listener</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input.accessibility/'>fuchsia.ui.input.accessibility</a>/<a class='link' href='../fuchsia.ui.input.accessibility/#PointerEventListener'>PointerEventListener</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>success</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>















