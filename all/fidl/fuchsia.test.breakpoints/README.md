[TOC]

# fuchsia.test.breakpoints


## **PROTOCOLS**

## Breakpoints {#Breakpoints}
*Defined in [fuchsia.test.breakpoints/breakpoints.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/src/sys/component_manager/tests/fidl/breakpoints.fidl#59)*

<p>A protocol used in testing by a component instance to block the
component manager until specific events occur.</p>

### Register {#Register}

<p>Register breakpoints for the given EventTypes.
Must be called exactly once before Expect or Resume.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event_types</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#EventType'>EventType</a>&gt;[3]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Expect {#Expect}

<p>Blocks until the next invocation of a breakpoint occurs and verifies
that the EventType and component list are as expected.</p>
<p>Note: The component manager is blocked after this call and will not be
allowed to proceed until resumed explicitly by calling Resume().</p>

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
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### WaitUntilCapabilityUse {#WaitUntilCapabilityUse}

<p>Blocks until a CapabilityUse invocation matching the specified component
and capability path. All other invocations are ignored.</p>
<p>Note: The component manager is blocked after this call and will not be
allowed to proceed until resumed explicitly by calling Resume().</p>

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
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Resume {#Resume}

<p>Resume the component manager from the last expected invocation.</p>

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
            <td><code>STOP_INSTANCE</code></td>
            <td><code>0</code></td>
            <td><p>An instance was stopped successfully.
This event must occur before PostDestroyInstance.</p>
</td>
        </tr><tr>
            <td><code>PRE_DESTROY_INSTANCE</code></td>
            <td><code>1</code></td>
            <td><p>The component subtree rooted at this instance is about to be destroyed.
The instance may have been stopped by this point.
This event must occur before PostDestroyInstance.</p>
</td>
        </tr><tr>
            <td><code>POST_DESTROY_INSTANCE</code></td>
            <td><code>2</code></td>
            <td><p>The component subtree rooted at this instance has been destroyed.
All instances under this subtree have been stopped by this point.</p>
</td>
        </tr><tr>
            <td><code>CAPABILITY_USE</code></td>
            <td><code>3</code></td>
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

