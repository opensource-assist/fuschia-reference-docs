Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.input.accessibility


## **PROTOCOLS**

## PointerEventRegistry {:#PointerEventRegistry}
*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#50)*

 PointerEventRegistration allows an accessibility service to register a
 pointer event listener, so that it can intercept pointer events before they
 reach clients.

### Register {:#Register}

 Registers a listener to start receiving incoming pointer events. For
 now, only one listener is allowed and the first to register is honored.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pointer_event_listener</code></td>
            <td>
                <code><a class='link' href='#PointerEventListener'>PointerEventListener</a></code>
            </td>
        </tr></table>



## PointerEventListener {:#PointerEventListener}
*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#59)*

 A PointerEventListener receives pointer events and decides to consume them
 or not.
 TODO(fxb/36429): Investigate flow control mechanisms for a11y input events.

### OnEvent {:#OnEvent}

 Sends a PointerEvent to an accessibility service. An event is returned
 at any time to indicate whether the pointer event stream was consumed /
 rejected for a particular stream of pointer events related to a
 `device_id` and a `pointer_id`. A stream is a sequence of pointer events
 starting with an event with phase DOWN, followed by any number of MOVE,
 ending in an UP phase event. The event can arrive while the stream is in
 progress or when it has already finished. The resulting
 behavior depends on how it was handled, please see EventHandling above.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>pointer_event</code></td>
            <td>
                <code><a class='link' href='#PointerEvent'>PointerEvent</a></code>
            </td>
        </tr></table>



### OnStreamHandled {:#OnStreamHandled}




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

### EventHandling {:#EventHandling}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#12)*

 Possible ways an accessibility listener can process pointer events.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CONSUMED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>REJECTED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### PointerEvent {:#PointerEvent}


*Defined in [fuchsia.ui.input.accessibility/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input.accessibility/accessibility.fidl#24)*

 A PointerEvent is a privileged pointer event that has local view and global
 screen coordinates as well as some metadata about the event type.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>event_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time the event was delivered. The time is in nanoseconds and corresponds
 to the uptime of the machine.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>device_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> ID of the device that captured this event.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>pointer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> ID of the pointer that identifies this event.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#PointerEventType'>PointerEventType</a></code>
            </td>
            <td> Type of this event, e.g. touch, mouse, etc.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>phase</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/index.html'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/index.html#PointerEventPhase'>PointerEventPhase</a></code>
            </td>
            <td> Phase of this event, e.g. add, down, etc.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>global_point</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#PointF'>PointF</a></code>
            </td>
            <td> The point of this pointer event in global screen coordinates.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>viewref_koid</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The viewref koid of the top most view hit for this pointer event.
 This field is set to `ZX_KOID_INVALID` when there is no view hit and
 `local_point` is undefined.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>local_point</code></td>
            <td>
                <code><a class='link' href='../fuchsia.math/index.html'>fuchsia.math</a>/<a class='link' href='../fuchsia.math/index.html#PointF'>PointF</a></code>
            </td>
            <td> The point of this pointer event in local view coordinates.
</td>
        </tr></table>









