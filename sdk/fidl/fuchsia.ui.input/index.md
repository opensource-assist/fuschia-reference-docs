Project: /_project.yaml
Book: /_book.yaml

# fuchsia.ui.input


## **PROTOCOLS**

## ImeService {:#ImeService}
*Defined in [fuchsia.ui.input/ime_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/ime_service.fidl#11)*

 The service provided by an IME

### GetInputMethodEditor {:#GetInputMethodEditor}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>keyboard_type</code></td>
            <td>
                <code><a class='link' href='#KeyboardType'>KeyboardType</a></code>
            </td>
        </tr><tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#InputMethodAction'>InputMethodAction</a></code>
            </td>
        </tr><tr>
            <td><code>initial_state</code></td>
            <td>
                <code><a class='link' href='#TextInputState'>TextInputState</a></code>
            </td>
        </tr><tr>
            <td><code>client</code></td>
            <td>
                <code><a class='link' href='#InputMethodEditorClient'>InputMethodEditorClient</a></code>
            </td>
        </tr><tr>
            <td><code>editor</code></td>
            <td>
                <code>request&lt;<a class='link' href='#InputMethodEditor'>InputMethodEditor</a>&gt;</code>
            </td>
        </tr></table>



### ShowKeyboard {:#ShowKeyboard}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### HideKeyboard {:#HideKeyboard}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### InjectInput {:#InjectInput}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#InputEvent'>InputEvent</a></code>
            </td>
        </tr></table>



### DispatchKey {:#DispatchKey}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.input2/index.html'>fuchsia.ui.input2</a>/<a class='link' href='../fuchsia.ui.input2/index.html#KeyEvent'>KeyEvent</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## ImeVisibilityService {:#ImeVisibilityService}
*Defined in [fuchsia.ui.input/ime_service.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/ime_service.fidl#28)*

 Onscreen keyboard containers connect to this to know when a keyboard
 should be shown or hidden.

### OnKeyboardVisibilityChanged {:#OnKeyboardVisibilityChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>visible</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

## InputDeviceRegistry {:#InputDeviceRegistry}
*Defined in [fuchsia.ui.input/input_device_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_device_registry.fidl#12)*

 Service to receive input events.

 Input devices can describe their capabilities using `DeviceDescriptor`
 and register themselves with the `InputDeviceRegistry`.

### RegisterDevice {:#RegisterDevice}

 Register a device with the capabilities described by `DeviceDescriptor`

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#DeviceDescriptor'>DeviceDescriptor</a></code>
            </td>
        </tr><tr>
            <td><code>input_device</code></td>
            <td>
                <code>request&lt;<a class='link' href='#InputDevice'>InputDevice</a>&gt;</code>
            </td>
        </tr></table>



## InputDevice {:#InputDevice}
*Defined in [fuchsia.ui.input/input_device_registry.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_device_registry.fidl#17)*


### DispatchReport {:#DispatchReport}

 Dispatch an `InputReport` from the device `token`

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>report</code></td>
            <td>
                <code><a class='link' href='#InputReport'>InputReport</a></code>
            </td>
        </tr></table>



## InputMethodEditor {:#InputMethodEditor}
*Defined in [fuchsia.ui.input/text_input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_input.fidl#41)*

 A interface for interacting with a text input control.

### SetKeyboardType {:#SetKeyboardType}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>keyboard_type</code></td>
            <td>
                <code><a class='link' href='#KeyboardType'>KeyboardType</a></code>
            </td>
        </tr></table>



### SetState {:#SetState}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#TextInputState'>TextInputState</a></code>
            </td>
        </tr></table>



### InjectInput {:#InjectInput}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#InputEvent'>InputEvent</a></code>
            </td>
        </tr></table>



### Show {:#Show}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Hide {:#Hide}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## InputMethodEditorClient {:#InputMethodEditorClient}
*Defined in [fuchsia.ui.input/text_input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_input.fidl#53)*

 An interface to receive information from `TextInputService`.

### DidUpdateState {:#DidUpdateState}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#TextInputState'>TextInputState</a></code>
            </td>
        </tr><tr>
            <td><code>event</code></td>
            <td>
                <code><a class='link' href='#InputEvent'>InputEvent</a>?</code>
            </td>
        </tr></table>



### OnAction {:#OnAction}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>action</code></td>
            <td>
                <code><a class='link' href='#InputMethodAction'>InputMethodAction</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### SendKeyboardInputCmd {:#SendKeyboardInputCmd}
*Defined in [fuchsia.ui.input/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/commands.fidl#20)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>compositor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>keyboard_event</code></td>
            <td>
                <code><a class='link' href='#KeyboardEvent'>KeyboardEvent</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SendPointerInputCmd {:#SendPointerInputCmd}
*Defined in [fuchsia.ui.input/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/commands.fidl#25)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>compositor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pointer_event</code></td>
            <td>
                <code><a class='link' href='#PointerEvent'>PointerEvent</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetHardKeyboardDeliveryCmd {:#SetHardKeyboardDeliveryCmd}
*Defined in [fuchsia.ui.input/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/commands.fidl#36)*



 Typically, clients should receive text inputs from an IME.

 For cases where no IME mediation is desired (such as a game application),
 this command requests Scenic to deliver hard keyboard events to the client.

 By default, Scenic will *not* deliver hard keyboard events to a client.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>delivery_request</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SetParallelDispatchCmd {:#SetParallelDispatchCmd}
*Defined in [fuchsia.ui.input/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/commands.fidl#46)*



 Typically, clients that participate in the hit test should receive input
 events in parallel. This behavior is required for gesture disambiguation.

 This command, typically set by the root presenter, allows disabling parallel
 dispatch; it is part of the input v2 transition work.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>parallel_dispatch</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyboardEvent {:#KeyboardEvent}
*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#32)*



 `KeyboardEvent` represents event generated by a user's interaction with a
 keyboard.

 Those events are triggered by distinct pressed state changes of the keys.

 The state transitions should be as follows:
 PRESSED -> (REPEAT ->) RELEASED
 or
 PRESSED -> (REPEAT ->) CANCELLED

 The input system will repeat those events automatically when a code_point is
 available.

 DEPRECATED: Will be removed in favor of `fuchsia.ui.input.KeyEvent`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time the event was delivered. The time is in nanoseconds and corresponds
 to the uptime of the machine.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>device_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phase</code></td>
            <td>
                <code><a class='link' href='#KeyboardEventPhase'>KeyboardEventPhase</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>hid_usage</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Keyboard HID Usage
 See https://www.usb.org/sites/default/files/documents/hut1_12v2.pdf
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>code_point</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The unicode code point represented by this key event, if any.
 Dead keys are represented as Unicode combining characters.

 If there is no unicode code point, this value is zero.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>modifiers</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Key modifiers as defined by the different kModifier constants such as
 `kModifierCapsLock` currently pressed
</td>
            <td>No default</td>
        </tr>
</table>

### PointerEvent {:#PointerEvent}
*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#115)*



 Pointers represent raw data about the user's interaction with the screen.

 The state transitions should be as follows:
 ADD (-> HOVER) -> DOWN -> MOVE -> UP (-> HOVER) -> REMOVE

 At any point after the initial ADD, a transition to CANCEL is also possible.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time the event was delivered. The time is in nanoseconds and corresponds
 to the uptime of the machine.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>device_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pointer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#PointerEventType'>PointerEventType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phase</code></td>
            <td>
                <code><a class='link' href='#PointerEventPhase'>PointerEventPhase</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> `x` and `y` are in the coordinate system of the View.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>radius_major</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>0.0</td>
        </tr><tr>
            <td><code>radius_minor</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>0.0</td>
        </tr><tr>
            <td><code>buttons</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Currently pressed buttons as defined the kButton constants such as
 `kMousePrimaryButton`
</td>
            <td>No default</td>
        </tr>
</table>

### FocusEvent {:#FocusEvent}
*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#147)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Time the event was delivered. The time is in nanoseconds and corresponds
 to the uptime of the machine.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>focused</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the view has gained input focused or not.
</td>
            <td>No default</td>
        </tr>
</table>

### Range {:#Range}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#19)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### RangeF {:#RangeF}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#24)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Axis {:#Axis}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#35)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>resolution</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>1</td>
        </tr><tr>
            <td><code>scale</code></td>
            <td>
                <code><a class='link' href='#AxisScale'>AxisScale</a></code>
            </td>
            <td></td>
            <td><a class='link' href='#LINEAR'>LINEAR</a></td>
        </tr>
</table>

### AxisF {:#AxisF}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#41)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#RangeF'>RangeF</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>resolution</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>1.0</td>
        </tr><tr>
            <td><code>scale</code></td>
            <td>
                <code><a class='link' href='#AxisScale'>AxisScale</a></code>
            </td>
            <td></td>
            <td><a class='link' href='#LINEAR'>LINEAR</a></td>
        </tr>
</table>

### MediaButtonsDescriptor {:#MediaButtonsDescriptor}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#48)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>buttons</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyboardDescriptor {:#KeyboardDescriptor}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#57)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>keys</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### KeyboardReport {:#KeyboardReport}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#63)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pressed_keys</code></td>
            <td>
                <code>vector&lt;uint32&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MouseDescriptor {:#MouseDescriptor}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#72)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>rel_x</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rel_y</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>vscroll</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>hscroll</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>buttons</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MouseReport {:#MouseReport}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#89)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>rel_x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rel_y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rel_hscroll</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>rel_vscroll</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pressed_buttons</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StylusDescriptor {:#StylusDescriptor}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#105)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pressure</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_invertible</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>false</td>
        </tr><tr>
            <td><code>buttons</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StylusReport {:#StylusReport}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#120)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pressure</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_in_contact</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>in_range</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_inverted</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pressed_buttons</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TouchscreenDescriptor {:#TouchscreenDescriptor}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#146)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>x</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_finger_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Touch {:#Touch}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#155)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>finger_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>x</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### TouchscreenReport {:#TouchscreenReport}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#172)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>touches</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Touch'>Touch</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SensorDescriptor {:#SensorDescriptor}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#197)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#SensorType'>SensorType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>loc</code></td>
            <td>
                <code><a class='link' href='#SensorLocation'>SensorLocation</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>min_sampling_freq</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max_sampling_freq</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>fifo_max_event_count</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phys_min</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>phys_max</code></td>
            <td>
                <code>int32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### MediaButtonsReport {:#MediaButtonsReport}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#225)*



 `MediaButtonsReport` describes the media buttons event delivered from the event stream.
 Each bool in the report represents a single button where true means the button
 is being pressed. A single report should be sent on every state change.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>volume_up</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>volume_down</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mic_mute</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>reset</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceInfo {:#DeviceInfo}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#234)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vendor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>product_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>version</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### DeviceDescriptor {:#DeviceDescriptor}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#242)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>device_info</code></td>
            <td>
                <code><a class='link' href='#DeviceInfo'>DeviceInfo</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>keyboard</code></td>
            <td>
                <code><a class='link' href='#KeyboardDescriptor'>KeyboardDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>media_buttons</code></td>
            <td>
                <code><a class='link' href='#MediaButtonsDescriptor'>MediaButtonsDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mouse</code></td>
            <td>
                <code><a class='link' href='#MouseDescriptor'>MouseDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>stylus</code></td>
            <td>
                <code><a class='link' href='#StylusDescriptor'>StylusDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>touchscreen</code></td>
            <td>
                <code><a class='link' href='#TouchscreenDescriptor'>TouchscreenDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>sensor</code></td>
            <td>
                <code><a class='link' href='#SensorDescriptor'>SensorDescriptor</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### InputReport {:#InputReport}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#253)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>event_time</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>keyboard</code></td>
            <td>
                <code><a class='link' href='#KeyboardReport'>KeyboardReport</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>media_buttons</code></td>
            <td>
                <code><a class='link' href='#MediaButtonsReport'>MediaButtonsReport</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>mouse</code></td>
            <td>
                <code><a class='link' href='#MouseReport'>MouseReport</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>stylus</code></td>
            <td>
                <code><a class='link' href='#StylusReport'>StylusReport</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>touchscreen</code></td>
            <td>
                <code><a class='link' href='#TouchscreenReport'>TouchscreenReport</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>sensor</code></td>
            <td>
                <code><a class='link' href='#SensorReport'>SensorReport</a>?</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>trace_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>0</td>
        </tr>
</table>

### TextRange {:#TextRange}
*Defined in [fuchsia.ui.input/text_editing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_editing.fidl#32)*



 A range of characters in a string of text. Although strings in FIDL's wire
 format are UTF-8 encoded, these indices are measured in UTF-16 code units
 for legacy reasons. These text input APIs will eventually be replaced by
 fuchsia.ui.text, which uses code points instead.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>start</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The index of the first UTF-16 code unit in the range.

 If `start` and `end` are both -1, the text range is empty.
</td>
            <td>-1</td>
        </tr><tr>
            <td><code>end</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The next index after the last UTF-16 code unit in this range.

 If `start` and `end` are both -1, the text range is empty.
</td>
            <td>-1</td>
        </tr>
</table>

### TextSelection {:#TextSelection}
*Defined in [fuchsia.ui.input/text_editing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_editing.fidl#51)*



 A range of text that represents a selection. Although strings in FIDL's wire
 format are UTF-8 encoded, these indices are measured in UTF-16 code units
 for legacy reasons. These text input APIs will eventually be replaced by
 fuchsia.ui.text, which uses code points instead.

 Text selection is always directional. Direction should be determined by
 comparing base and extent.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>base</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The offset at which the selection originates, as measured in UTF-16 code units.

 Might be larger than, smaller than, or equal to extent.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>extent</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> The offset at which the selection terminates, as measured in UTF-16 code units.

 When the user uses the arrow keys to adjust the selection, this is the
 value that changes. Similarly, if the current theme paints a caret on one
 side of the selection, this is the location at which to paint the caret.

 Might be larger than, smaller than, or equal to base.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>affinity</code></td>
            <td>
                <code><a class='link' href='#TextAffinity'>TextAffinity</a></code>
            </td>
            <td> If the text range is collapsed and has more than one visual location
 (e.g., occurs at a line break), which of the two locations to use when
 painting the caret.
</td>
            <td>No default</td>
        </tr>
</table>

### TextInputState {:#TextInputState}
*Defined in [fuchsia.ui.input/text_input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_input.fidl#26)*



 The current text, selection, and composing state for editing a run of text.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>revision</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Current state revision to avoid race conditions.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code>string</code>
            </td>
            <td> The current text being edited.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>selection</code></td>
            <td>
                <code><a class='link' href='#TextSelection'>TextSelection</a></code>
            </td>
            <td> The range of text that is currently selected.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>composing</code></td>
            <td>
                <code><a class='link' href='#TextRange'>TextRange</a></code>
            </td>
            <td> The range of text that is still being composed.
</td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### KeyboardEventPhase {:#KeyboardEventPhase}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>PRESSED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>RELEASED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CANCELLED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>REPEAT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### PointerEventType {:#PointerEventType}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#56)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>TOUCH</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>STYLUS</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVERTED_STYLUS</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>MOUSE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### PointerEventPhase {:#PointerEventPhase}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#70)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ADD</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>HOVER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWN</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>MOVE</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>UP</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>REMOVE</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>CANCEL</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr></table>

### AxisScale {:#AxisScale}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#29)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINEAR</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LOGARITHMIC</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### SensorType {:#SensorType}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#181)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ACCELEROMETER</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>GYROSCOPE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAGNETOMETER</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>LIGHTMETER</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### SensorLocation {:#SensorLocation}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#188)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>BASE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>LID</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### TextAffinity {:#TextAffinity}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/text_editing.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_editing.fidl#14)*

 Whether a TextPosition is visually upstream or downstream of its offset.

 For example, when a text position exists at a line break, a single offset has
 two visual positions, one prior to the line break (at the end of the first
 line) and one after the line break (at the start of the second line). A text
 affinity disambiguates between those cases. (Something similar happens with
 between runs of bidirectional text.)


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UPSTREAM</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DOWNSTREAM</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### KeyboardType {:#KeyboardType}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/text_input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_input.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>TEXT</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NUMBER</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PHONE</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DATETIME</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### InputMethodAction {:#InputMethodAction}
Type: <code>uint32</code>

*Defined in [fuchsia.ui.input/text_input.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/text_input.fidl#14)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>GO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>SEARCH</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>SEND</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>NEXT</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>DONE</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>PREVIOUS</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### MediaButtonsEvent {:#MediaButtonsEvent}


*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#156)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>volume</code></td>
            <td>
                <code>int8</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>mic_mute</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### Command {:#Command}
*Defined in [fuchsia.ui.input/commands.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/commands.fidl#7)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>send_keyboard_input</code></td>
            <td>
                <code><a class='link' href='#SendKeyboardInputCmd'>SendKeyboardInputCmd</a></code>
            </td>
            <td> Commands for conveying input events to a `Session`.
 Structs defined in input_events.fidl.
</td>
        </tr><tr>
            <td><code>send_pointer_input</code></td>
            <td>
                <code><a class='link' href='#SendPointerInputCmd'>SendPointerInputCmd</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>set_hard_keyboard_delivery</code></td>
            <td>
                <code><a class='link' href='#SetHardKeyboardDeliveryCmd'>SetHardKeyboardDeliveryCmd</a></code>
            </td>
            <td> Command to enable/disable delivery of hard keyboard events.
</td>
        </tr><tr>
            <td><code>set_parallel_dispatch</code></td>
            <td>
                <code><a class='link' href='#SetParallelDispatchCmd'>SetParallelDispatchCmd</a></code>
            </td>
            <td> Command to enable/disable parallel delivery of input events.
</td>
        </tr></table>

### InputEvent {:#InputEvent}
*Defined in [fuchsia.ui.input/input_events.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_events.fidl#162)*

 This union does not include MediaButtonsEvent because it's processed differently.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>pointer</code></td>
            <td>
                <code><a class='link' href='#PointerEvent'>PointerEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>keyboard</code></td>
            <td>
                <code><a class='link' href='#KeyboardEvent'>KeyboardEvent</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>focus</code></td>
            <td>
                <code><a class='link' href='#FocusEvent'>FocusEvent</a></code>
            </td>
            <td></td>
        </tr></table>

### SensorReport {:#SensorReport}
*Defined in [fuchsia.ui.input/input_reports.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_reports.fidl#217)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>vector</code></td>
            <td>
                <code>int16[3]</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>scalar</code></td>
            <td>
                <code>uint16</code>
            </td>
            <td></td>
        </tr></table>







## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#8">kModifierNone</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#9">kModifierCapsLock</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#10">kModifierLeftShift</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#11">kModifierRightShift</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#12">kModifierShift</a></td>
            <td>
                    <code>6</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#13">kModifierLeftControl</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#14">kModifierRightControl</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#15">kModifierControl</a></td>
            <td>
                    <code>24</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#16">kModifierLeftAlt</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#17">kModifierRightAlt</a></td>
            <td>
                    <code>64</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#18">kModifierAlt</a></td>
            <td>
                    <code>96</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#19">kModifierLeftSuper</a></td>
            <td>
                    <code>128</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#20">kModifierRightSuper</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#21">kModifierSuper</a></td>
            <td>
                    <code>384</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#24">kMousePrimaryButton</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#25">kMouseSecondaryButton</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#26">kMouseTertiaryButton</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#29">kStylusPrimaryButton</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/input_event_constants.fidl#30">kStylusSecondaryButton</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#8">kMouseButtonPrimary</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#9">kMouseButtonSecondary</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#10">kMouseButtonTertiary</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#13">kStylusBarrel</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#16">kVolumeUp</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#17">kVolumeDown</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#18">kMicMute</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.input/usages.fidl#19">kReset</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
        </tr>
    
</table>

