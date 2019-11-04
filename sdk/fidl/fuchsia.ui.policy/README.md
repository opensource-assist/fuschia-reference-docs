[TOC]

# fuchsia.ui.policy


## **PROTOCOLS**

## DeviceListenerRegistry {#DeviceListenerRegistry}
*Defined in [fuchsia.ui.policy/device_listener.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/device_listener.fidl#9)*

 Service for exposing state and events of devices, such as media buttons.

### RegisterMediaButtonsListener {#RegisterMediaButtonsListener}

 Registers a listener to receive media button related events, such as
 changes from volume buttons and mute switches.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#MediaButtonsListener'>MediaButtonsListener</a></code>
            </td>
        </tr></table>



## KeyboardCaptureListenerHACK {#KeyboardCaptureListenerHACK}
*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#11)*

 `Presentation.CaptureKeyboardEvent` will consume this listener interface and
 call `OnEvent` when the registered keyboard event occurs.

### OnEvent {#OnEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#KeyboardEvent'>KeyboardEvent</a></code>
            </td>
        </tr></table>



## PointerCaptureListenerHACK {#PointerCaptureListenerHACK}
*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#17)*

 `Presentation.CapturePointerEvent` will consume this listener interface and
 call `OnEvent` when a pointer event occurs.

### OnPointerEvent {#OnPointerEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#PointerEvent'>PointerEvent</a></code>
            </td>
        </tr></table>



## MediaButtonsListener {#MediaButtonsListener}
*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#23)*

 `Presentation.RegisterMediaButtonsListener` will consume this listener interface
 and call `OnMediaButtonsEvent` when the registered media buttons event occurs.

### OnMediaButtonsEvent {#OnMediaButtonsEvent}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#MediaButtonsEvent'>MediaButtonsEvent</a></code>
            </td>
        </tr></table>



## Presentation {#Presentation}
*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#30)*

 Allows clients of Presenter.Present() to control a presentation.
 Experimental.

### CaptureKeyboardEventHACK {#CaptureKeyboardEventHACK}

 This call exists so that base shell can capture hotkeys and do special
 things with it (e.g., switch a session shell). Phase and modifiers are always
 matched, and valid (non-zero) code points are matched. If there is no
 valid code point, the filter will match against the hid usage value.
 The full KeyboardEvent is supplied to `listener`'s OnEvent.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event_to_capture</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#KeyboardEvent'>KeyboardEvent</a></code>
            </td>
        </tr><tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#KeyboardCaptureListenerHACK'>KeyboardCaptureListenerHACK</a></code>
            </td>
        </tr></table>



### CapturePointerEventsHACK {#CapturePointerEventsHACK}

 This call exists so that base shell can capture pointer events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#PointerCaptureListenerHACK'>PointerCaptureListenerHACK</a></code>
            </td>
        </tr></table>



### RegisterMediaButtonsListener {#RegisterMediaButtonsListener}

 Registers a listener for media buttons events.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#MediaButtonsListener'>MediaButtonsListener</a></code>
            </td>
        </tr></table>



### InjectPointerEventHACK {#InjectPointerEventHACK}

 EXPERIMENTAL. Inject pointer events into input stream. This WILL go
 away. Used exclusively by Session Shells to test focus navigation.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#PointerEvent'>PointerEvent</a></code>
            </td>
        </tr></table>



## PresentationModeListener {#PresentationModeListener}
*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#70)*

 Tell client that the screen mode has changed, according to sensors.
 N.B. There can be a race where the actual mode continues to change, after
 the listener has been notified. The client must call GetPresentationMode(),
 which will return the latest detected mode.

### OnModeChanged {#OnModeChanged}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## Presenter {#Presenter}
*Defined in [fuchsia.ui.policy/presenter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presenter.fidl#14)*

 The Presenter service provides a way for applications to ask that a view be
 added to a view tree, leaving any window management concerns up to the
 discretion of the presenter implementation.

### PresentView {#PresentView}

 Request that the View's contents be displayed on the screen as a
 `Presentation`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>view_holder_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.views/'>fuchsia.ui.views</a>/<a class='link' href='../fuchsia.ui.views/#ViewHolderToken'>ViewHolderToken</a></code>
            </td>
        </tr><tr>
            <td><code>presentation_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Presentation'>Presentation</a>&gt;?</code>
            </td>
        </tr></table>



### HACK_SetRendererParams {#HACK_SetRendererParams}

 Sets new default renderer params and forces them on for the duration of the
 presenter's lifetime. Only applies to any subsequent calls to Present().
 Used for testing.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enable_clipping</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>params</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.ui.gfx/'>fuchsia.ui.gfx</a>/<a class='link' href='../fuchsia.ui.gfx/#RendererParam'>RendererParam</a>&gt;</code>
            </td>
        </tr></table>







## **ENUMS**

### DisplayUsage {#DisplayUsage}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.policy/display_usage.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/display_usage.fidl#8)*

 Describes the intended usage of the display.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kUnknown</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>kHandheld</code></td>
            <td><code>1</code></td>
            <td> Display is held in one or both hands.
</td>
        </tr><tr>
            <td><code>kClose</code></td>
            <td><code>2</code></td>
            <td> Display is used well within arm's reach.
</td>
        </tr><tr>
            <td><code>kNear</code></td>
            <td><code>3</code></td>
            <td> Display is used at arm's reach.
</td>
        </tr><tr>
            <td><code>kMidrange</code></td>
            <td><code>4</code></td>
            <td> Display is used beyond arm's reach.
</td>
        </tr><tr>
            <td><code>kFar</code></td>
            <td><code>5</code></td>
            <td> Display is used well beyond arm's reach.
</td>
        </tr></table>

### PresentationMode {#PresentationMode}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#59)*

 Screen modes that can be detected via sensor data.
 N.B. We use accelerometers to measure gravity when at rest, so detection is
 limited to earth-relative orientations.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>CLOSED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LAPTOP</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>TABLET</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>TENT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>










