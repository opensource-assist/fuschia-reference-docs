[TOC]

# fuchsia.test.breakpoints


## **PROTOCOLS**

## BreakpointSystem {#BreakpointSystem}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#100)*

<p>Registers breakpoints in component manager.</p>

### SetBreakpoints {#SetBreakpoints}

<p>Sets breakpoints on the given EventTypes.
Returns a BreakpointInvocationReceiver which can be used
to expect the registered types.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event_types</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EventType'>EventType</a>&gt;[9]</code>
            </td>
        </tr><tr>
            <td><code>server_end</code></td>
            <td>
                <code>request&lt;<a class='link' href='#InvocationReceiver'>InvocationReceiver</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### StartComponentManager {#StartComponentManager}

<p>Begins component manager's execution.
This method is a no-op when invoked more than once or by
a component inside component manager.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## InvocationReceiver {#InvocationReceiver}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#113)*

<p>Receives invocations for registered events in component manager.</p>

### Next {#Next}

<p>Blocks until the next invocation of a breakpoint occurs.</p>
<p>Note: The component manager is blocked after this call and will not be
allowed to proceed until resumed explicitly via the Handler.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>invocation</code></td>
            <td>
                <code><a class='link' href='#Invocation'>Invocation</a></code>
            </td>
        </tr></table>

## Handler {#Handler}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#122)*

<p>Every Invocation supports this basic handler to allow resumption.</p>

### Resume {#Resume}

<p>Resumes/unblocks from an invocation.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## RoutingProtocol {#RoutingProtocol}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#129)*

<p>Allows injecting capabilities over FIDL.
Used by RouteFrameworkCapability and RouteBuiltinCapability</p>

### SetProvider {#SetProvider}

<p>Inject a CapabilityProvider in response to a routing event.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>client_end</code></td>
            <td>
                <code><a class='link' href='#CapabilityProvider'>CapabilityProvider</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## CapabilityProvider {#CapabilityProvider}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#135)*

<p>A FIDL-based version of a CapabilityProvider</p>

### Open {#Open}

<p>Called to bind a server end of a channel to the provided framework capability.
TODO(xbhatnag): provide all arguments (flags, mode, path) to this method.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>server_end</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **ENUMS**

### EventType {#EventType}
Type: <code>uint32</code>

*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#21)*

<p>These EventTypes are used for the Breakpoints protocol.
They are FIDL versions of the EventType enum in hooks.rs and have
the same meaning.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADD_DYNAMIC_CHILD</code></td>
            <td><code>1</code></td>
            <td><p>A dynamic child was added to the parent instance.
Depending on its eagerness, this child may/may not be started yet.</p>
</td>
        </tr><tr>
            <td><code>POST_DESTROY_INSTANCE</code></td>
            <td><code>2</code></td>
            <td><p>An instance was destroyed successfully. The instance is stopped and no longer
exists in the parent's realm.</p>
</td>
        </tr><tr>
            <td><code>PRE_DESTROY_INSTANCE</code></td>
            <td><code>3</code></td>
            <td><p>Destruction of an instance has begun. The instance may/may not be stopped by this point.
The instance still exists in the parent's realm but will soon be removed.
TODO(fxb/39417): Ensure the instance is stopped before this event.</p>
</td>
        </tr><tr>
            <td><code>ROOT_COMPONENT_RESOLVED</code></td>
            <td><code>4</code></td>
            <td><p>The root component instance's declaration was resolved successfully for the first time.</p>
</td>
        </tr><tr>
            <td><code>ROUTE_BUILTIN_CAPABILITY</code></td>
            <td><code>5</code></td>
            <td><p>A builtin capability is being requested by a component and requires routing.
The event propagation system is used to supply the capability being requested.</p>
</td>
        </tr><tr>
            <td><code>ROUTE_FRAMEWORK_CAPABILITY</code></td>
            <td><code>6</code></td>
            <td><p>A framework capability is being requested by a component and requires routing.
The event propagation system is used to supply the capability being requested.</p>
</td>
        </tr><tr>
            <td><code>START_INSTANCE</code></td>
            <td><code>7</code></td>
            <td><p>An instance was bound to. If the instance is executable, it is also started.</p>
</td>
        </tr><tr>
            <td><code>STOP_INSTANCE</code></td>
            <td><code>8</code></td>
            <td><p>An instance was stopped successfully.
This event must occur before PostDestroyInstance.</p>
</td>
        </tr><tr>
            <td><code>USE_CAPABILITY</code></td>
            <td><code>9</code></td>
            <td><p>A capability was used by an instance. An instance uses a capability when
it creates a channel and provides the server end to ComponentManager for routing.</p>
</td>
        </tr></table>



## **TABLES**

### EventPayload {#EventPayload}


*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#59)*

<p>Encapsulates additional data/protocols for some event types.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>routing_payload</code></td>
            <td>
                <code><a class='link' href='#RoutingPayload'>RoutingPayload</a></code>
            </td>
            <td><p>Payload for RouteFrameworkCapability and RouteBuiltinCapability events</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>use_capability_payload</code></td>
            <td>
                <code><a class='link' href='#UseCapabilityPayload'>UseCapabilityPayload</a></code>
            </td>
            <td><p>Payload for UseCapability event</p>
</td>
        </tr></table>

### RoutingPayload {#RoutingPayload}


*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#68)*

<p>Payload for RouteFrameworkCapability and RouteBuiltinCapability events</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>routing_protocol</code></td>
            <td>
                <code><a class='link' href='#RoutingProtocol'>RoutingProtocol</a></code>
            </td>
            <td><p>Allows setting a capability provider for RouteFrameworkCapability
and RouteBuiltinCapability events</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>capability</code></td>
            <td>
                <code>string[50]</code>
            </td>
            <td><p>Name/Path of a capability.</p>
</td>
        </tr></table>

### UseCapabilityPayload {#UseCapabilityPayload}


*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#78)*

<p>Payload for UseCapability event</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>capability</code></td>
            <td>
                <code>string[50]</code>
            </td>
            <td><p>Name/Path of a capability</p>
</td>
        </tr></table>

### Invocation {#Invocation}


*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#84)*

<p>Contains all information about a single invocation of a breakpoint</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>event_type</code></td>
            <td>
                <code><a class='link' href='#EventType'>EventType</a></code>
            </td>
            <td><p>Event type corresponding to the invocation</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>target_moniker</code></td>
            <td>
                <code>string[100]</code>
            </td>
            <td><p>Moniker of instance corresponding to the invocation</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>handler</code></td>
            <td>
                <code><a class='link' href='#Handler'>Handler</a></code>
            </td>
            <td><p>Handler for resuming from invocation</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>event_payload</code></td>
            <td>
                <code><a class='link' href='#EventPayload'>EventPayload</a></code>
            </td>
            <td><p>Optional payload for some event types</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#9">MAX_NUM_EVENT_TYPES_RECEIVED</a></td>
            <td>
                    <code>9</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum number of event types that a receiver can listen to.
This capacity should match the actual number of event types.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#12">MAX_MONIKER_LENGTH</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum string length of a component moniker.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#16">MAX_CAPABILITY_LENGTH</a></td>
            <td>
                    <code>50</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum string length of the name/path of a capability.
This value is currently set arbitrarily.</p>
</td>
        </tr>
    
</table>



