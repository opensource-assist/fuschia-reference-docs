[TOC]

# fuchsia.test.breakpoints


## **PROTOCOLS**

## BreakpointSystem {#BreakpointSystem}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#62)*

<p>Registers breakpoints in component manager.</p>

### Register {#Register}

<p>Registers breakpoints for the given EventTypes.
Returns a BreakpointInvocationReceiver which can be used
to expect the registered types.</p>
<p>If component manager is in debug mode, the first call to this
method implicitly starts component manager's execution.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event_types</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EventType'>EventType</a>&gt;[3]</code>
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

## InvocationReceiver {#InvocationReceiver}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#73)*

<p>Receives invocations for registered events in component manager.</p>

### Expect {#Expect}

<p>Blocks until the next invocation of a breakpoint occurs and verifies
that the EventType and component are as expected.</p>
<p>Note: The component manager is blocked after this call and will not be
allowed to proceed until resumed explicitly via the Invocation object.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event_type</code></td>
            <td>
                <code><a class='link' href='#EventType'>EventType</a></code>
            </td>
        </tr><tr>
            <td><code>component</code></td>
            <td>
                <code>vector&lt;string&gt;[10]</code>
            </td>
        </tr><tr>
            <td><code>server_end</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Invocation'>Invocation</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### ExpectType {#ExpectType}

<p>Blocks until the next invocation of a breakpoint occurs and verifies
that the EventType is as expected.</p>
<p>Note: The component manager is blocked after this call and will not be
allowed to proceed until resumed explicitly via the Invocation object.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event_type</code></td>
            <td>
                <code><a class='link' href='#EventType'>EventType</a></code>
            </td>
        </tr><tr>
            <td><code>server_end</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Invocation'>Invocation</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### WaitUntilUseCapability {#WaitUntilUseCapability}

<p>Blocks until a UseCapability invocation matching the specified component
and capability path. All other invocations are ignored.</p>
<p>Note: The component manager is blocked after this call and will not be
allowed to proceed until resumed explicitly via the Invocation object.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>component</code></td>
            <td>
                <code>vector&lt;string&gt;[10]</code>
            </td>
        </tr><tr>
            <td><code>requested_capability_path</code></td>
            <td>
                <code>string[50]</code>
            </td>
        </tr><tr>
            <td><code>server_end</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Invocation'>Invocation</a>&gt;</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Invocation {#Invocation}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#97)*

<p>A single invocation of a breakpoint in component manager.</p>

### Resume {#Resume}

<p>Resume/unblock the component manager from this invocation.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>





## **ENUMS**

### EventType {#EventType}
Type: <code>uint32</code>

*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#34)*

<p>These EventTypes are used for the Breakpoints protocol.
They are FIDL versions of the EventType enum in hooks.rs and have
the same meaning.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>START_INSTANCE</code></td>
            <td><code>0</code></td>
            <td><p>An instance was bound to successfully.
This instance is now running.</p>
</td>
        </tr><tr>
            <td><code>STOP_INSTANCE</code></td>
            <td><code>1</code></td>
            <td><p>An instance was stopped successfully.
This event must occur before PostDestroyInstance.</p>
</td>
        </tr><tr>
            <td><code>PRE_DESTROY_INSTANCE</code></td>
            <td><code>2</code></td>
            <td><p>The component subtree rooted at this instance is about to be destroyed.
The instance may have been stopped by this point.
This event must occur before PostDestroyInstance.
TODO(fxb/39417): Ensure the instance is stopped before this event.</p>
</td>
        </tr><tr>
            <td><code>POST_DESTROY_INSTANCE</code></td>
            <td><code>3</code></td>
            <td><p>The component subtree rooted at this instance has been destroyed.
All instances under this subtree have been stopped by this point.</p>
</td>
        </tr><tr>
            <td><code>USE_CAPABILITY</code></td>
            <td><code>4</code></td>
            <td><p>A capability has been requested for use by the component.
A component uses a capability by creating a channel and providing
the server end of the channel to the component manager for routing
to a particular capability.</p>
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#9">MAX_NUM_EVENT_TYPES</a></td>
            <td>
                    <code>3</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>The maximum number of event types to register breakpoints for.
This capacity should match the actual number of event types.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#15">MAX_COMPONENT_DEPTH</a></td>
            <td>
                    <code>10</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>When a caller expects an Event or waits until a capability is used
by a specific component, this constant determines the maximum depth
(in terms of components) of that capability. This value is currently
set arbitrarily.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#24">MAX_MONIKER_LENGTH</a></td>
            <td>
                    <code>50</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>When a caller expects an Event or waits until a capability is used
by a specific component, this constant determines the maximum string
length of the moniker of each comprising instance.</p>
<p>For example, if a caller expects an event on a component whose path is
&quot;/<A>/<B>/<C>&quot;, then this constant determines the maximum length of
<A>, <B> and <C>. This value is currently set arbitrarily.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#29">MAX_CAPABILITY_PATH_LENGTH</a></td>
            <td>
                    <code>50</code>
                </td>
                <td><code>uint64</code></td>
            <td><p>When a caller waits until a specific capability is used by a specific
component, this constant determines the maximum string length of the path
of that capability. This value is currently set arbitrarily.</p>
</td>
        </tr>
    
</table>



