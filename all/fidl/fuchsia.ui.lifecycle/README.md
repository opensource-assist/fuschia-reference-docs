[TOC]

# fuchsia.ui.lifecycle


## **PROTOCOLS**

## LifecycleController {#LifecycleController}
*Defined in [fuchsia.ui.lifecycle/lifecycle_controller.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.lifecycle/lifecycle_controller.fidl#9)*

<p>An interface implemented by system UI components that wish to terminate gracefully.</p>

### Terminate {#Terminate}

<p>The controller of this component has requested that this component terminate gracefully.
If the component does not terminate itself in a timely manner, the client may forcibly
terminate the component.</p>
<p>The connection to the controller will be broken shortly before the target terminates;
clients should listen for channel closure to learn the approximate moment that the target
terminates.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

















