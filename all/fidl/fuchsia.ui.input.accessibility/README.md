[TOC]

# fuchsia.ui.input.accessibility


## **PROTOCOLS**

## PointerEventRegistry {#PointerEventRegistry}
*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#53)*

<p>PointerEventRegistration allows an accessibility service to register a
pointer event listener, so that it can intercept pointer events before they
reach clients.</p>

### Register {#Register}

<p>Registers a listener to start receiving incoming pointer events. For
now, only one listener is allowed and the first to register is honored.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pointer_event_listener</code></td>
            <td>
                <code><a class='link' href='#PointerEventListener'>PointerEventListener</a></code>
            </td>
        </tr></table>



## PointerEventListener {#PointerEventListener}
*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#62)*

<p>A PointerEventListener receives pointer events and decides to consume them
or not.
TODO(fxb/36429): Investigate flow control mechanisms for a11y input events.</p>

### OnEvent {#OnEvent}

<p>Sends a PointerEvent to an accessibility service. An event is returned
at any time to indicate whether the pointer event stream was consumed /
rejected for a particular stream of pointer events related to a
<code>device_id</code> and a <code>pointer_id</code>. A stream is a sequence of pointer events
starting with an event with phase DOWN, followed by any number of MOVE,
ending in an UP phase event. The event can arrive while the stream is in
progress or when it has already finished. The resulting
behavior depends on how it was handled, please see EventHandling above.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pointer_event</code></td>
            <td>
                <code><a class='link' href='#PointerEvent'>PointerEvent</a></code>
            </td>
        </tr></table>



### OnStreamHandled {#OnStreamHandled}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>pointer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>handled</code></td>
            <td>
                <code><a class='link' href='#EventHandling'>EventHandling</a></code>
            </td>
        </tr></table>





## **ENUMS**

### EventHandling {#EventHandling}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#12)*

<p>Possible ways an accessibility listener can process pointer events.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONSUMED</code></td>
            <td><code>1</code></td>
            <td><p>The listener consumes all the pointer events for (device_id, pointer_id)
until the next UP event.</p>
</td>
        </tr><tr>
            <td><code>REJECTED</code></td>
            <td><code>2</code></td>
            <td><p>The listener rejects the remaining pointer events for (device_id,
pointer_id), and observed (past) and expected (future) pointer events
until the next UP event are to be sent for regular input dispatch.</p>
</td>
        </tr></table>



## **TABLES**

### PointerEvent {#PointerEvent}


*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#24)*

<p>A PointerEvent is a privileged pointer event that has local view and global
screen coordinates as well as some metadata about the event type.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>event_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Time the event was delivered. The time is in nanoseconds and corresponds
to the uptime of the machine.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>device_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>ID of the device that captured this event.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>pointer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>ID of the pointer that identifies this event.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#PointerEventType'>PointerEventType</a></code>
            </td>
            <td><p>Type of this event, e.g. touch, mouse, etc.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>phase</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#PointerEventPhase'>PointerEventPhase</a></code>
            </td>
            <td><p>Phase of this event, e.g. add, down, etc.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>ndc_point</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/#PointF'>PointF</a></code>
            </td>
            <td><p>The coordinate of this pointer event in normalized device coordinates.
Normalized device coordinates have dimensions in the range [-1, 1],
with (0, 0) being the center of the device and axes aligned with the
native display.</p>
</td>
        </tr><tr>
            <td>7</td>
            <td><code>viewref_koid</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#koid'>koid</a></code>
            </td>
            <td><p>The viewref koid of the top most view hit for this pointer event.
This field is set to <code>ZX_KOID_INVALID</code> when there is no view hit and
<code>local_point</code> is undefined.</p>
</td>
        </tr><tr>
            <td>8</td>
            <td><code>local_point</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/#PointF'>PointF</a></code>
            </td>
            <td><p>The point of this pointer event in local view coordinates.</p>
</td>
        </tr></table>











