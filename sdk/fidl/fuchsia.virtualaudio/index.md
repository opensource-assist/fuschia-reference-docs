Project: /_project.yaml
Book: /_book.yaml

# fuchsia.virtualaudio


## **PROTOCOLS**

## Forwarder {:#Forwarder}
*Defined in [fuchsia.virtualaudio/virtual_audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualaudio/virtual_audio.fidl#17)*

 Using this Simple Layout (C-bound) protocol, an intermediary (such as the
 virtual audio service) forwards FIDL protocol requests to the virtual audio
 driver, which enables clients to use more full-featured (C++ based) bindings
 with this driver -- specifically the Control, Input and Output protocols.

### SendControl {:#SendControl}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>control</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Control'>Control</a>&gt;</code>
            </td>
        </tr></table>



### SendInput {:#SendInput}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Input'>Input</a>&gt;</code>
            </td>
        </tr></table>



### SendOutput {:#SendOutput}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output</code></td>
            <td>
                <code>request&lt;<a class='link' href='#Output'>Output</a>&gt;</code>
            </td>
        </tr></table>



## Control {:#Control}
*Defined in [fuchsia.virtualaudio/virtual_audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualaudio/virtual_audio.fidl#32)*

 This protocol provides the caller a high-level ON/OFF switch for overall
 virtual audio functionality at the system level. When virtualaudio is
 disabled, device configurations can be created and changed, but no devices
 can be added. When virtualaudio is enabled, device configurations can again
 be converted into devices by calling `Add()`.

### Enable {:#Enable}

 Allow inputs and outputs to be activated, but do not automatically
 reactivate those previously deactivated by `Disable()`. Does not affect
 existing Configs. By default, virtualaudio is enabled on system startup.
 This method's callback can be used as a mechanism to synchronize with
 other asynchronous in-flight virtualaudio FIDL operations.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### Disable {:#Disable}

 Deactivate all active inputs/outputs; disallow subsequent activations.
 This method's callback can be used as a mechanism to synchronize with
 other asynchronous in-flight virtualaudio FIDL operations.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### GetNumDevices {:#GetNumDevices}

 Return the number of active input and output virtual devices.
 This method's callback can be used as a mechanism to synchronize with
 other asynchronous in-flight virtualaudio FIDL operations.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>num_input_devices</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>num_output_devices</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

## Input {:#Input}
*Defined in [fuchsia.virtualaudio/virtual_audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualaudio/virtual_audio.fidl#66)*

 This protocol represents an active virtual audio input device. It inherits
 the parent protocols Device and Configuration. This protocol, as well as the
 contents of Device, represent actions that can be taken by an active input
 device -- actions that should be immediately detected and reacted upon by
 the audio subsystem.

### SetDeviceName {:#SetDeviceName}

 Set the virtual audio device's name. This corresponds to the value
 associated with the device node for this virtual device. This must be
 called before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetManufacturer {:#SetManufacturer}

 Set the virtual audio device's manufacturer name. This must be called
 before calling `Add()`, or after `Remove()`. Once a device is activated,
 this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_MANUFACTURER`. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioDeviceInfo` struct by `GetDevices()` and the
 `->OnDeviceAdded()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>manufacturer_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetProduct {:#SetProduct}

 Set the virtual audio device's product name. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, this
 value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_PRODUCT`. This information is exposed to clients by
 the `fuchsia.media.AudioDeviceEnumerator` protocol: returned in an
 `AudioDeviceInfo` struct by `GetDevices()` and the `->OnDeviceAdded()`
 event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>product_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetUniqueId {:#SetUniqueId}

 Set the virtual audio device's unique ID, a 16-character string. This
 must be called before calling `Add()`, or after `Remove()`. Once the
 device is activated, this value is returned by the driver in response
 to an `AUDIO_STREAM_CMD_GET_UNIQUE_ID` command. This value is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol:
 returned in an `AudioDeviceInfo` struct by `GetDevices()` or
 `->OnDeviceAdded()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>unique_id</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
        </tr></table>



### AddFormatRange {:#AddFormatRange}

 Add a supported format range for this audio device. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, format ranges are returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_FORMATS` command. sample_format_flags is of type
 audio_sample_format_t, and rate_family_flags is a bit field of possible
 constants beginning with `ASF_RANGE_FLAG_FPS_`. See audio.h for details.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sample_format_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>max_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>rate_family_flags</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### ClearFormatRanges {:#ClearFormatRanges}

 Remove the minimal format range that is added by default to all
 configurations. As with `AddFormatRange()`, this method must be called
 before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetFifoDepth {:#SetFifoDepth}

 Set the virtual audio device's fifo depth, in bytes. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, the depth of its FIFO is returned by the driver in response
 to an `AUDIO_RB_CMD_GET_FIFO_DEPTH` command on the ring buffer channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fifo_depth_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetExternalDelay {:#SetExternalDelay}

 Set the virtual audio device's external delay, in nanoseconds. This must
 be called before calling `Add()`, or after `Remove()`. Once the device
 is activated, this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_SET_FORMAT` command.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SetRingBufferRestrictions {:#SetRingBufferRestrictions}

 Set restrictions for the device ring buffer. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, the
 ring buffer and its size are returned by the driver in response to an
 `AUDIO_RB_CMD_GET_BUFFER` command on the ring buffer channel.
 Note: both min_frames and max_frames must be multiples of modulo_frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>modulo_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetGainProperties {:#SetGainProperties}

 Set gain properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, gain
 information is returned by the driver in an
 `audio_stream_cmd_get_gain_resp` struct, in response to an
 `AUDIO_STREAM_CMD_GET_GAIN` command. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioGainInfo` struct by `GetDeviceGain()` and the
 `->OnDeviceGainChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>max_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>gain_step_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>can_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetPlugProperties {:#SetPlugProperties}

 Set plug properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, plug
 information is returned by the driver in response to an
 `AUDIO_STREAM_CMD_PLUG_DETECT` command. This information is used by the
 system when determining which device is default. This in turn is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: in
 `GetDevices()`, `GetDefaultInputDevice()`/`GetDefaultOutputDevice()` and
 the `->OnDefaultDeviceChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plug_change_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>plugged</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>hardwired</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_notify</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### ResetConfiguration {:#ResetConfiguration}

 Return a configuration to its default settings. This call has no effect
 on active devices. In other words, it must be called before calling
 `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Add {:#Add}

 Activate (`DdkAdd`) the virtual audio device as currently configured. A
 device node will be published and detected by the AudioDeviceManager,
 and a driver for the virtual device will be loaded and queried. Device
 arrivals are exposed to clients by the
 `fuchsia.media.AudioDeviceEnumerator` protocol, in `GetDevices()` and
 the `->OnDeviceAdded()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Remove {:#Remove}

 Deactivate (`DdkRemove`) the active virtual audio device, but retain its
 configuration for future activation. The driver for the virtual device
 will be unloaded, and the device node closed. Device removals are
 exposed to clients by `fuchsia.media.AudioDeviceEnumerator`, in
 `GetDevices()` and `->OnDeviceRemoved()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetFormat {:#GetFormat}

 Return the format selected by the client, when that client issued an
 `AUDIO_STREAM_CMD_SET_FORMAT` command. This can only occur after a
 device has been added, and is only allowed to occur before the device's
 ring buffer has been returned (i.e., before an
 `AUDIO_RB_CMD_GET_BUFFER` command).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>sample_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>num_channels</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnSetFormat {:#OnSetFormat}

 Notify all subscribed listeners when the above format is set or changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>sample_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>num_channels</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### GetGain {:#GetGain}

 Return the current gain state for this device. After a device has been
 added, a client can call this at any time -- even before the ring buffer
 has been established, or before the format has been set.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### OnSetGain {:#OnSetGain}

 Notify all subscribed listeners when the above gain is set or changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### GetBuffer {:#GetBuffer}

 Return details about the ring buffer that was established in response
 to a client `AUDIO_RB_CMD_GET_BUFFER` command. This will only occur
 after the client sets the format and retrieves other driver information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>num_ring_buffer_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### OnBufferCreated {:#OnBufferCreated}

 Notify all subscribed listeners when the above buffer has been created.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>num_ring_buffer_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetNotificationFrequency {:#SetNotificationFrequency}

 Override the position notification frequency set by AudioCore for this
 stream, with the given value. Although this method can be called at any
 time (including before this Input|Output is added, or after it is
 started), logically it makes most sense to call this immediately after
 receiving details about the just-created ring buffer, via `GetBuffer` or
 the `->OnBufferCreated` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnStart {:#OnStart}

 Notify all subscribed listeners when the device is commanded to Start
 streaming. This can only occur after a device is fully configured
 (format is set; ring buffer is established and fetched).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnStop {:#OnStop}

 Notify all subscribed listeners when the device is commanded to Stop
 streaming. This can only occur when the device is already Started. Stop
 returns the device to a fully-configured state. Upon this command, the
 already-set format and ring buffer are retained without change, but
 position will re-begin at 0, if the device is again Started.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stop_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetPosition {:#GetPosition}

 Return the current position (in bytes) within the ring buffer. This can
 only be called after the ring buffer is established. If the device has
 not yet Started streaming, then zero will always be returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>clock_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnPositionNotify {:#OnPositionNotify}

 Notify all subscribed listeners, when any `AUDIO_RB_POSITION_NOTIFY`
 position notification is issued by the driver. The frequency of these
 per-stream notifications is set by AudioCore, reported to VAD clients
 via `GetBuffer` or the `->OnBufferCreated` event. VirtualAudioDevice
 clients can enable an alternate notification frequency for a given
 stream by calling `SetNotificationFrequency`.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>clock_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### ChangePlugState {:#ChangePlugState}

 Hot-plug or hot-unplug an active virtual device, at the specified time.
 For devices marked as capable of asynchronously notifying the system of
 plug changes, the driver will now send the values using
 `AUDIO_STREAM_PLUG_DETECT_NOTIFY`. Else, values will be reflected when
 the driver is next sent an `AUDIO_STREAM_CMD_PLUG_DETECT` command. This
 information is used by the system when determining which device is
 default. This, in turn, is exposed to clients by the
 `fuchsia.media.AudioDeviceEnumerator` protocol: in `GetDevices()`,
 `GetDefaultInputDevice()`/`GetDefaultOutputDevice()` and the
 `->OnDefaultDeviceChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plug_change_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>plugged</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## Output {:#Output}
*Defined in [fuchsia.virtualaudio/virtual_audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualaudio/virtual_audio.fidl#85)*

 This protocol represents an active virtual audio output device. It inherits
 the parent protocols Device and Configuration. This protocol, as well as the
 contents of Device, represent actions that can be taken by an active output
 device -- actions that should be immediately detected and reacted upon by
 the audio subsystem.

### SetDeviceName {:#SetDeviceName}

 Set the virtual audio device's name. This corresponds to the value
 associated with the device node for this virtual device. This must be
 called before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetManufacturer {:#SetManufacturer}

 Set the virtual audio device's manufacturer name. This must be called
 before calling `Add()`, or after `Remove()`. Once a device is activated,
 this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_MANUFACTURER`. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioDeviceInfo` struct by `GetDevices()` and the
 `->OnDeviceAdded()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>manufacturer_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetProduct {:#SetProduct}

 Set the virtual audio device's product name. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, this
 value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_PRODUCT`. This information is exposed to clients by
 the `fuchsia.media.AudioDeviceEnumerator` protocol: returned in an
 `AudioDeviceInfo` struct by `GetDevices()` and the `->OnDeviceAdded()`
 event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>product_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetUniqueId {:#SetUniqueId}

 Set the virtual audio device's unique ID, a 16-character string. This
 must be called before calling `Add()`, or after `Remove()`. Once the
 device is activated, this value is returned by the driver in response
 to an `AUDIO_STREAM_CMD_GET_UNIQUE_ID` command. This value is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol:
 returned in an `AudioDeviceInfo` struct by `GetDevices()` or
 `->OnDeviceAdded()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>unique_id</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
        </tr></table>



### AddFormatRange {:#AddFormatRange}

 Add a supported format range for this audio device. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, format ranges are returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_FORMATS` command. sample_format_flags is of type
 audio_sample_format_t, and rate_family_flags is a bit field of possible
 constants beginning with `ASF_RANGE_FLAG_FPS_`. See audio.h for details.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sample_format_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>max_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>rate_family_flags</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### ClearFormatRanges {:#ClearFormatRanges}

 Remove the minimal format range that is added by default to all
 configurations. As with `AddFormatRange()`, this method must be called
 before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetFifoDepth {:#SetFifoDepth}

 Set the virtual audio device's fifo depth, in bytes. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, the depth of its FIFO is returned by the driver in response
 to an `AUDIO_RB_CMD_GET_FIFO_DEPTH` command on the ring buffer channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fifo_depth_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetExternalDelay {:#SetExternalDelay}

 Set the virtual audio device's external delay, in nanoseconds. This must
 be called before calling `Add()`, or after `Remove()`. Once the device
 is activated, this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_SET_FORMAT` command.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SetRingBufferRestrictions {:#SetRingBufferRestrictions}

 Set restrictions for the device ring buffer. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, the
 ring buffer and its size are returned by the driver in response to an
 `AUDIO_RB_CMD_GET_BUFFER` command on the ring buffer channel.
 Note: both min_frames and max_frames must be multiples of modulo_frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>modulo_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetGainProperties {:#SetGainProperties}

 Set gain properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, gain
 information is returned by the driver in an
 `audio_stream_cmd_get_gain_resp` struct, in response to an
 `AUDIO_STREAM_CMD_GET_GAIN` command. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioGainInfo` struct by `GetDeviceGain()` and the
 `->OnDeviceGainChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>max_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>gain_step_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>can_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetPlugProperties {:#SetPlugProperties}

 Set plug properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, plug
 information is returned by the driver in response to an
 `AUDIO_STREAM_CMD_PLUG_DETECT` command. This information is used by the
 system when determining which device is default. This in turn is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: in
 `GetDevices()`, `GetDefaultInputDevice()`/`GetDefaultOutputDevice()` and
 the `->OnDefaultDeviceChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plug_change_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>plugged</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>hardwired</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_notify</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### ResetConfiguration {:#ResetConfiguration}

 Return a configuration to its default settings. This call has no effect
 on active devices. In other words, it must be called before calling
 `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Add {:#Add}

 Activate (`DdkAdd`) the virtual audio device as currently configured. A
 device node will be published and detected by the AudioDeviceManager,
 and a driver for the virtual device will be loaded and queried. Device
 arrivals are exposed to clients by the
 `fuchsia.media.AudioDeviceEnumerator` protocol, in `GetDevices()` and
 the `->OnDeviceAdded()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Remove {:#Remove}

 Deactivate (`DdkRemove`) the active virtual audio device, but retain its
 configuration for future activation. The driver for the virtual device
 will be unloaded, and the device node closed. Device removals are
 exposed to clients by `fuchsia.media.AudioDeviceEnumerator`, in
 `GetDevices()` and `->OnDeviceRemoved()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetFormat {:#GetFormat}

 Return the format selected by the client, when that client issued an
 `AUDIO_STREAM_CMD_SET_FORMAT` command. This can only occur after a
 device has been added, and is only allowed to occur before the device's
 ring buffer has been returned (i.e., before an
 `AUDIO_RB_CMD_GET_BUFFER` command).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>sample_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>num_channels</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnSetFormat {:#OnSetFormat}

 Notify all subscribed listeners when the above format is set or changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>sample_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>num_channels</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### GetGain {:#GetGain}

 Return the current gain state for this device. After a device has been
 added, a client can call this at any time -- even before the ring buffer
 has been established, or before the format has been set.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### OnSetGain {:#OnSetGain}

 Notify all subscribed listeners when the above gain is set or changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### GetBuffer {:#GetBuffer}

 Return details about the ring buffer that was established in response
 to a client `AUDIO_RB_CMD_GET_BUFFER` command. This will only occur
 after the client sets the format and retrieves other driver information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>num_ring_buffer_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### OnBufferCreated {:#OnBufferCreated}

 Notify all subscribed listeners when the above buffer has been created.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>num_ring_buffer_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetNotificationFrequency {:#SetNotificationFrequency}

 Override the position notification frequency set by AudioCore for this
 stream, with the given value. Although this method can be called at any
 time (including before this Input|Output is added, or after it is
 started), logically it makes most sense to call this immediately after
 receiving details about the just-created ring buffer, via `GetBuffer` or
 the `->OnBufferCreated` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnStart {:#OnStart}

 Notify all subscribed listeners when the device is commanded to Start
 streaming. This can only occur after a device is fully configured
 (format is set; ring buffer is established and fetched).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnStop {:#OnStop}

 Notify all subscribed listeners when the device is commanded to Stop
 streaming. This can only occur when the device is already Started. Stop
 returns the device to a fully-configured state. Upon this command, the
 already-set format and ring buffer are retained without change, but
 position will re-begin at 0, if the device is again Started.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stop_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetPosition {:#GetPosition}

 Return the current position (in bytes) within the ring buffer. This can
 only be called after the ring buffer is established. If the device has
 not yet Started streaming, then zero will always be returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>clock_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnPositionNotify {:#OnPositionNotify}

 Notify all subscribed listeners, when any `AUDIO_RB_POSITION_NOTIFY`
 position notification is issued by the driver. The frequency of these
 per-stream notifications is set by AudioCore, reported to VAD clients
 via `GetBuffer` or the `->OnBufferCreated` event. VirtualAudioDevice
 clients can enable an alternate notification frequency for a given
 stream by calling `SetNotificationFrequency`.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>clock_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### ChangePlugState {:#ChangePlugState}

 Hot-plug or hot-unplug an active virtual device, at the specified time.
 For devices marked as capable of asynchronously notifying the system of
 plug changes, the driver will now send the values using
 `AUDIO_STREAM_PLUG_DETECT_NOTIFY`. Else, values will be reflected when
 the driver is next sent an `AUDIO_STREAM_CMD_PLUG_DETECT` command. This
 information is used by the system when determining which device is
 default. This, in turn, is exposed to clients by the
 `fuchsia.media.AudioDeviceEnumerator` protocol: in `GetDevices()`,
 `GetDefaultInputDevice()`/`GetDefaultOutputDevice()` and the
 `->OnDefaultDeviceChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plug_change_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>plugged</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## Device {:#Device}
*Defined in [fuchsia.virtualaudio/virtual_audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualaudio/virtual_audio.fidl#97)*

 This protocol represents the base functionality of active Input and Output
 audio devices -- methods that are common to both protocols. This protocol,
 as well as the contents of Output and Input, represent actions that can be
 taken by an active device -- actions that should be immediately detected and
 reacted upon by the audio subsystem.

### SetDeviceName {:#SetDeviceName}

 Set the virtual audio device's name. This corresponds to the value
 associated with the device node for this virtual device. This must be
 called before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetManufacturer {:#SetManufacturer}

 Set the virtual audio device's manufacturer name. This must be called
 before calling `Add()`, or after `Remove()`. Once a device is activated,
 this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_MANUFACTURER`. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioDeviceInfo` struct by `GetDevices()` and the
 `->OnDeviceAdded()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>manufacturer_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetProduct {:#SetProduct}

 Set the virtual audio device's product name. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, this
 value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_PRODUCT`. This information is exposed to clients by
 the `fuchsia.media.AudioDeviceEnumerator` protocol: returned in an
 `AudioDeviceInfo` struct by `GetDevices()` and the `->OnDeviceAdded()`
 event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>product_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetUniqueId {:#SetUniqueId}

 Set the virtual audio device's unique ID, a 16-character string. This
 must be called before calling `Add()`, or after `Remove()`. Once the
 device is activated, this value is returned by the driver in response
 to an `AUDIO_STREAM_CMD_GET_UNIQUE_ID` command. This value is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol:
 returned in an `AudioDeviceInfo` struct by `GetDevices()` or
 `->OnDeviceAdded()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>unique_id</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
        </tr></table>



### AddFormatRange {:#AddFormatRange}

 Add a supported format range for this audio device. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, format ranges are returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_FORMATS` command. sample_format_flags is of type
 audio_sample_format_t, and rate_family_flags is a bit field of possible
 constants beginning with `ASF_RANGE_FLAG_FPS_`. See audio.h for details.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sample_format_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>max_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>rate_family_flags</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### ClearFormatRanges {:#ClearFormatRanges}

 Remove the minimal format range that is added by default to all
 configurations. As with `AddFormatRange()`, this method must be called
 before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetFifoDepth {:#SetFifoDepth}

 Set the virtual audio device's fifo depth, in bytes. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, the depth of its FIFO is returned by the driver in response
 to an `AUDIO_RB_CMD_GET_FIFO_DEPTH` command on the ring buffer channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fifo_depth_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetExternalDelay {:#SetExternalDelay}

 Set the virtual audio device's external delay, in nanoseconds. This must
 be called before calling `Add()`, or after `Remove()`. Once the device
 is activated, this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_SET_FORMAT` command.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SetRingBufferRestrictions {:#SetRingBufferRestrictions}

 Set restrictions for the device ring buffer. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, the
 ring buffer and its size are returned by the driver in response to an
 `AUDIO_RB_CMD_GET_BUFFER` command on the ring buffer channel.
 Note: both min_frames and max_frames must be multiples of modulo_frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>modulo_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetGainProperties {:#SetGainProperties}

 Set gain properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, gain
 information is returned by the driver in an
 `audio_stream_cmd_get_gain_resp` struct, in response to an
 `AUDIO_STREAM_CMD_GET_GAIN` command. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioGainInfo` struct by `GetDeviceGain()` and the
 `->OnDeviceGainChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>max_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>gain_step_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>can_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetPlugProperties {:#SetPlugProperties}

 Set plug properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, plug
 information is returned by the driver in response to an
 `AUDIO_STREAM_CMD_PLUG_DETECT` command. This information is used by the
 system when determining which device is default. This in turn is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: in
 `GetDevices()`, `GetDefaultInputDevice()`/`GetDefaultOutputDevice()` and
 the `->OnDefaultDeviceChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plug_change_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>plugged</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>hardwired</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_notify</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### ResetConfiguration {:#ResetConfiguration}

 Return a configuration to its default settings. This call has no effect
 on active devices. In other words, it must be called before calling
 `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Add {:#Add}

 Activate (`DdkAdd`) the virtual audio device as currently configured. A
 device node will be published and detected by the AudioDeviceManager,
 and a driver for the virtual device will be loaded and queried. Device
 arrivals are exposed to clients by the
 `fuchsia.media.AudioDeviceEnumerator` protocol, in `GetDevices()` and
 the `->OnDeviceAdded()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### Remove {:#Remove}

 Deactivate (`DdkRemove`) the active virtual audio device, but retain its
 configuration for future activation. The driver for the virtual device
 will be unloaded, and the device node closed. Device removals are
 exposed to clients by `fuchsia.media.AudioDeviceEnumerator`, in
 `GetDevices()` and `->OnDeviceRemoved()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### GetFormat {:#GetFormat}

 Return the format selected by the client, when that client issued an
 `AUDIO_STREAM_CMD_SET_FORMAT` command. This can only occur after a
 device has been added, and is only allowed to occur before the device's
 ring buffer has been returned (i.e., before an
 `AUDIO_RB_CMD_GET_BUFFER` command).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>sample_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>num_channels</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnSetFormat {:#OnSetFormat}

 Notify all subscribed listeners when the above format is set or changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>sample_format</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>num_channels</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### GetGain {:#GetGain}

 Return the current gain state for this device. After a device has been
 added, a client can call this at any time -- even before the ring buffer
 has been established, or before the format has been set.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### OnSetGain {:#OnSetGain}

 Notify all subscribed listeners when the above gain is set or changed.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### GetBuffer {:#GetBuffer}

 Return details about the ring buffer that was established in response
 to a client `AUDIO_RB_CMD_GET_BUFFER` command. This will only occur
 after the client sets the format and retrieves other driver information.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>num_ring_buffer_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### OnBufferCreated {:#OnBufferCreated}

 Notify all subscribed listeners when the above buffer has been created.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr><tr>
            <td><code>num_ring_buffer_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### SetNotificationFrequency {:#SetNotificationFrequency}

 Override the position notification frequency set by AudioCore for this
 stream, with the given value. Although this method can be called at any
 time (including before this Input|Output is added, or after it is
 started), logically it makes most sense to call this immediately after
 receiving details about the just-created ring buffer, via `GetBuffer` or
 the `->OnBufferCreated` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>notifications_per_ring</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnStart {:#OnStart}

 Notify all subscribed listeners when the device is commanded to Start
 streaming. This can only occur after a device is fully configured
 (format is set; ring buffer is established and fetched).



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>start_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnStop {:#OnStop}

 Notify all subscribed listeners when the device is commanded to Stop
 streaming. This can only occur when the device is already Started. Stop
 returns the device to a fully-configured state. Upon this command, the
 already-set format and ring buffer are retained without change, but
 position will re-begin at 0, if the device is again Started.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stop_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>

### GetPosition {:#GetPosition}

 Return the current position (in bytes) within the ring buffer. This can
 only be called after the ring buffer is established. If the device has
 not yet Started streaming, then zero will always be returned.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>clock_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### OnPositionNotify {:#OnPositionNotify}

 Notify all subscribed listeners, when any `AUDIO_RB_POSITION_NOTIFY`
 position notification is issued by the driver. The frequency of these
 per-stream notifications is set by AudioCore, reported to VAD clients
 via `GetBuffer` or the `->OnBufferCreated` event. VirtualAudioDevice
 clients can enable an alternate notification frequency for a given
 stream by calling `SetNotificationFrequency`.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>ring_position</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>clock_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### ChangePlugState {:#ChangePlugState}

 Hot-plug or hot-unplug an active virtual device, at the specified time.
 For devices marked as capable of asynchronously notifying the system of
 plug changes, the driver will now send the values using
 `AUDIO_STREAM_PLUG_DETECT_NOTIFY`. Else, values will be reflected when
 the driver is next sent an `AUDIO_STREAM_CMD_PLUG_DETECT` command. This
 information is used by the system when determining which device is
 default. This, in turn, is exposed to clients by the
 `fuchsia.media.AudioDeviceEnumerator` protocol: in `GetDevices()`,
 `GetDefaultInputDevice()`/`GetDefaultOutputDevice()` and the
 `->OnDefaultDeviceChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plug_change_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>plugged</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## Configuration {:#Configuration}
*Defined in [fuchsia.virtualaudio/virtual_audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.virtualaudio/virtual_audio.fidl#202)*

 This protocol is conceptually a base protocol to Device. It exposes the
 methods used to specify the properties of a virtual audio device (its
 configuration), before the virtual device is instantiated by the call to
 `Add()`. Although the non-Add methods on this protocol can be called after
 calling `Add()` (i.e., after Configuration has been converted into active
 Device), this only changes how future Devices will be created; it has no
 effect on already-created Devices.

### SetDeviceName {:#SetDeviceName}

 Set the virtual audio device's name. This corresponds to the value
 associated with the device node for this virtual device. This must be
 called before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetManufacturer {:#SetManufacturer}

 Set the virtual audio device's manufacturer name. This must be called
 before calling `Add()`, or after `Remove()`. Once a device is activated,
 this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_MANUFACTURER`. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioDeviceInfo` struct by `GetDevices()` and the
 `->OnDeviceAdded()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>manufacturer_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetProduct {:#SetProduct}

 Set the virtual audio device's product name. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, this
 value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_STRING` command of string ID
 `AUDIO_STREAM_STR_ID_PRODUCT`. This information is exposed to clients by
 the `fuchsia.media.AudioDeviceEnumerator` protocol: returned in an
 `AudioDeviceInfo` struct by `GetDevices()` and the `->OnDeviceAdded()`
 event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>product_name</code></td>
            <td>
                <code>string</code>
            </td>
        </tr></table>



### SetUniqueId {:#SetUniqueId}

 Set the virtual audio device's unique ID, a 16-character string. This
 must be called before calling `Add()`, or after `Remove()`. Once the
 device is activated, this value is returned by the driver in response
 to an `AUDIO_STREAM_CMD_GET_UNIQUE_ID` command. This value is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol:
 returned in an `AudioDeviceInfo` struct by `GetDevices()` or
 `->OnDeviceAdded()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>unique_id</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
        </tr></table>



### AddFormatRange {:#AddFormatRange}

 Add a supported format range for this audio device. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, format ranges are returned by the driver in response to an
 `AUDIO_STREAM_CMD_GET_FORMATS` command. sample_format_flags is of type
 audio_sample_format_t, and rate_family_flags is a bit field of possible
 constants beginning with `ASF_RANGE_FLAG_FPS_`. See audio.h for details.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>sample_format_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frame_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>min_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>max_channels</code></td>
            <td>
                <code>uint8</code>
            </td>
        </tr><tr>
            <td><code>rate_family_flags</code></td>
            <td>
                <code>uint16</code>
            </td>
        </tr></table>



### ClearFormatRanges {:#ClearFormatRanges}

 Remove the minimal format range that is added by default to all
 configurations. As with `AddFormatRange()`, this method must be called
 before calling `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetFifoDepth {:#SetFifoDepth}

 Set the virtual audio device's fifo depth, in bytes. This must be called
 before calling `Add()`, or after `Remove()`. Once the device is
 activated, the depth of its FIFO is returned by the driver in response
 to an `AUDIO_RB_CMD_GET_FIFO_DEPTH` command on the ring buffer channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>fifo_depth_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetExternalDelay {:#SetExternalDelay}

 Set the virtual audio device's external delay, in nanoseconds. This must
 be called before calling `Add()`, or after `Remove()`. Once the device
 is activated, this value is returned by the driver in response to an
 `AUDIO_STREAM_CMD_SET_FORMAT` command.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>external_delay</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### SetRingBufferRestrictions {:#SetRingBufferRestrictions}

 Set restrictions for the device ring buffer. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, the
 ring buffer and its size are returned by the driver in response to an
 `AUDIO_RB_CMD_GET_BUFFER` command on the ring buffer channel.
 Note: both min_frames and max_frames must be multiples of modulo_frames.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>max_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>modulo_frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetGainProperties {:#SetGainProperties}

 Set gain properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, gain
 information is returned by the driver in an
 `audio_stream_cmd_get_gain_resp` struct, in response to an
 `AUDIO_STREAM_CMD_GET_GAIN` command. This information is exposed to
 clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: returned
 in an `AudioGainInfo` struct by `GetDeviceGain()` and the
 `->OnDeviceGainChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>max_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>gain_step_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>current_gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>can_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>current_agc</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetPlugProperties {:#SetPlugProperties}

 Set plug properties for this virtual device. This must be called before
 calling `Add()`, or after `Remove()`. Once the device is activated, plug
 information is returned by the driver in response to an
 `AUDIO_STREAM_CMD_PLUG_DETECT` command. This information is used by the
 system when determining which device is default. This in turn is exposed
 to clients by the `fuchsia.media.AudioDeviceEnumerator` protocol: in
 `GetDevices()`, `GetDefaultInputDevice()`/`GetDefaultOutputDevice()` and
 the `->OnDefaultDeviceChanged()` event.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>plug_change_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>plugged</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>hardwired</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>can_notify</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### ResetConfiguration {:#ResetConfiguration}

 Return a configuration to its default settings. This call has no effect
 on active devices. In other words, it must be called before calling
 `Add()`, or after `Remove()`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

















