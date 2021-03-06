[TOC]

# fuchsia.ui.policy


## **PROTOCOLS**

## DeviceListenerRegistry {#DeviceListenerRegistry}
*Defined in [fuchsia.ui.policy/device_listener.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/device_listener.fidl#11)*

<p>Service for exposing state and events of devices, such as media buttons.</p>

### RegisterMediaButtonsListener {#RegisterMediaButtonsListener}

<p>Registers a listener to receive media button related events, such as
changes from volume buttons and mute switches.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#MediaButtonsListener'>MediaButtonsListener</a></code>
            </td>
        </tr></table>



## MediaButtonsListener {#MediaButtonsListener}
*Defined in [fuchsia.ui.policy/device_listener.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/device_listener.fidl#20)*

<p>A listener for media buttons events. <code>DeviceListenerRegistry.RegisterMediaButtonsListener</code>
will consume this listener interface and call <code>OnMediaButtonsEvent</code> when the
registered media buttons event occurs.</p>

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



## KeyboardCaptureListenerHACK {#KeyboardCaptureListenerHACK}
*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#11)*

<p><code>Presentation.CaptureKeyboardEvent</code> will consume this listener interface and
call <code>OnEvent</code> when the registered keyboard event occurs.</p>

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

<p><code>Presentation.CapturePointerEvent</code> will consume this listener interface and
call <code>OnEvent</code> when a pointer event occurs.</p>

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



## Presentation {#Presentation}
*Defined in [fuchsia.ui.policy/presentation.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presentation.fidl#24)*

<p>Allows clients of Presenter.Present() to control a presentation.
Experimental.</p>

### CaptureKeyboardEventHACK {#CaptureKeyboardEventHACK}

<p>This call exists so that base shell can capture hotkeys and do special
things with it (e.g., switch a session shell). Phase and modifiers are always
matched, and valid (non-zero) code points are matched. If there is no
valid code point, the filter will match against the hid usage value.
The full KeyboardEvent is supplied to <code>listener</code>'s OnEvent.</p>

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

<p>This call exists so that base shell can capture pointer events.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>listener</code></td>
            <td>
                <code><a class='link' href='#PointerCaptureListenerHACK'>PointerCaptureListenerHACK</a></code>
            </td>
        </tr></table>



### InjectPointerEventHACK {#InjectPointerEventHACK}

<p>EXPERIMENTAL. Inject pointer events into input stream. This WILL go
away. Used exclusively by Session Shells to test focus navigation.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input/'>fuchsia.ui.input</a>/<a class='link' href='../fuchsia.ui.input/#PointerEvent'>PointerEvent</a></code>
            </td>
        </tr></table>



## Presenter {#Presenter}
*Defined in [fuchsia.ui.policy/presenter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.policy/presenter.fidl#14)*

<p>The Presenter service provides a way for applications to ask that a view be
added to a view tree, leaving any window management concerns up to the
discretion of the presenter implementation.</p>

### PresentView {#PresentView}

<p>Request that the View's contents be displayed on the screen as a <code>Presentation</code>.
Each call to <code>PresentView</code> creates a new <code>Presentation</code>. Having more than one simultaneous
<code>Presentation</code> (i.e. calling <code>PresentView</code> more than once) is deprecated, and will
print a warning. In the future, this will result in an error and the channel being closed.</p>

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



### PresentOrReplaceView {#PresentOrReplaceView}

<p>Request that the View's contents be displayed on the screen as a <code>Presentation</code>.
Destroys any existing presentations and replaces them with the new one.
This is true whether the existing view was created by a call to
PresentOrReplaceView or to PresentView.</p>

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

<p>Sets new default renderer params and forces them on for the duration of the
presenter's lifetime. Only applies to any subsequent calls to Present().
Used for testing.</p>

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

<p>Describes the intended usage of the display.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>kUnknown</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>kHandheld</code></td>
            <td><code>1</code></td>
            <td><p>Display is held in one or both hands.</p>
</td>
        </tr><tr>
            <td><code>kClose</code></td>
            <td><code>2</code></td>
            <td><p>Display is used well within arm's reach.</p>
</td>
        </tr><tr>
            <td><code>kNear</code></td>
            <td><code>3</code></td>
            <td><p>Display is used at arm's reach.</p>
</td>
        </tr><tr>
            <td><code>kMidrange</code></td>
            <td><code>4</code></td>
            <td><p>Display is used beyond arm's reach.</p>
</td>
        </tr><tr>
            <td><code>kFar</code></td>
            <td><code>5</code></td>
            <td><p>Display is used well beyond arm's reach.</p>
</td>
        </tr></table>













