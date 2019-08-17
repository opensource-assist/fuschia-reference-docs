Project: /_project.yaml
Book: /_book.yaml

# fuchsia.media


## **PROTOCOLS**

## Audio {:#Audio}
*Defined in [fuchsia.media/audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio.fidl#8)*


### CreateAudioRenderer {:#CreateAudioRenderer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>audio_renderer_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AudioRenderer'>AudioRenderer</a>&gt;</code>
            </td>
        </tr></table>



### CreateAudioCapturer {:#CreateAudioCapturer}

 Create an AudioCapturer which either captures from the current default
 audio input device, or loops-back from the current default audio output
 device based on value passed for the loopback flag.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>audio_capturer_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AudioCapturer'>AudioCapturer</a>&gt;</code>
            </td>
        </tr><tr>
            <td><code>loopback</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetSystemMute {:#SetSystemMute}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetSystemGain {:#SetSystemGain}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SystemGainMuteChanged {:#SystemGainMuteChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### SetRoutingPolicy {:#SetRoutingPolicy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>policy</code></td>
            <td>
                <code><a class='link' href='#AudioOutputRoutingPolicy'>AudioOutputRoutingPolicy</a></code>
            </td>
        </tr></table>



## AudioCapturer {:#AudioCapturer}
*Defined in [fuchsia.media/audio_capturer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_capturer.fidl#260)*

 AudioCapturer

 An AudioCapturer is an interface returned from an fuchsia.media.Audio's
 CreateAudioCapturer method, which may be used by clients to capture audio
 from either the current default audio input device, or the current default
 audio output device depending on the flags passed during creation.

 ** Format support **

 See (Get|Set)StreamType below. By default, the captured stream type will be
 initially determined by the currently configured stream type of the source
 that the AudioCapturer was bound to at creation time. Users may either fetch
 this type using GetStreamType, or they may choose to have the media
 resampled or converted to a type of their choosing by calling SetStreamType.
 Note: the stream type may only be set while the system is not running,
 meaning that there are no pending capture regions (specified using CaptureAt)
 and that the system is not currently running in 'async' capture mode.

 ** Buffers and memory management **

 Audio data is captured into a shared memory buffer (a VMO) supplied by the
 user to the AudioCapturer during the AddPayloadBuffer call.  Please note the
 following requirements related to the management of the payload buffer.

 ++ The payload buffer must be supplied before any capture operation may
    start.  Any attempt to start capture (via either CaptureAt or
    StartAsyncCapture) before a payload buffer has been established is an
    error.
 ++ The payload buffer may not be changed while there are any capture
    operations pending.
 ++ The stream type may not be changed after the payload buffer has been set.
 ++ The payload buffer must be an integral number of audio frame sizes (in
    bytes)
 ++ When running in 'async' mode (see below), the payload buffer must be at
    least as large as twice the frames_per_packet size specified during
    StartAsyncCapture.
 ++ The handle to the payload buffer supplied by the user must be readable,
    writable, and mappable.
 ++ Users should always treat the payload buffer as read-only.

 ** Synchronous vs. Asynchronous capture mode **

 The AudioCapturer interface can be used in one of two mutually exclusive
 modes: Synchronous and Asynchronous.  A description of each mode and their
 tradeoffs is given below.

 ** Synchronous mode **

 By default, AudioCapturer instances are running in 'sync' mode.  They will
 only capture data when a user supplies at least one region to capture into
 using the CaptureAt method.  Regions supplied in this way will be filled in
 the order that they are received and returned to the client as StreamPackets
 via the return value of the CaptureAt method.  If an AudioCapturer instance
 has data to capture, but no place to put it (because there are no more
 pending regions to fill), the next payload generated will indicate that their
 has been an overflow by setting the Discontinuity flag on the next produced
 StreamPacket.  Synchronous mode may not be used in conjunction with
 Asynchronous mode.  It is an error to attempt to call StartAsyncCapture while
 the system still regions supplied by CaptureAt waiting to be filled.

 If a user has supplied regions to be filled by the AudioCapturer instance in
 the past, but wishes to reclaim those regions, they may do so using the
 DiscardAllPackets method.  Calling the DiscardAllPackets method will cause
 all pending regions to be returned, but with `NO_TIMESTAMP` as their
 StreamPacket's PTS.  See "Timing and Overflows", below, for a discussion of
 timestamps and discontinuity flags. After a DiscardAllPackets operation,
 an OnEndOfStream event will be produced.  While an AudioCapturer will never
 overwrite any region of the payload buffer after a completed region is
 returned, it may overwrite the unfilled portions of a partially filled
 buffer which has been returned as a result of a DiscardAllPackets operation.

 ** Asynchronous mode **

 While running in 'async' mode, clients do not need to explicitly supply
 shared buffer regions to be filled by the AudioCapturer instance. Instead, a
 client enters into 'async' mode by calling StartAsyncCapture and supplying a
 callback interface and the number of frames to capture per-callback. Once
 running in async mode, the AudioCapturer instance will identify which
 payload buffer regions to capture into, capture the specified number of
 frames, then deliver those frames as StreamPackets using the OnPacketCapture
 FIDL event. Users may stop capturing and return the AudioCapturer instance to
 'sync' mode using the StopAsyncCapture method.

 It is considered an error to attempt any of the following operations.

 ++ To attempt to enter 'async' capture mode when no payload buffer has been
    established.
 ++ To specify a number of frames to capture per payload which does not permit
    at least two contiguous capture payloads to exist in the established
    shared payload buffer simultaneously.
 ++ To send a region to capture into using the CaptureAt method while the
    AudioCapturer instance is running in 'async' mode.
 ++ To attempt to call DiscardAllPackets while the AudioCapturer instance is
    running in 'async' mode.
 ++ To attempt to re-start 'async' mode capturing without having first
    stopped.
 ++ To attempt any operation except for SetGain while in the process of
    stopping.

 ** Synchronizing with a StopAsyncCapture operation **

 Stopping asynchronous capture mode and returning to synchronous capture mode
 is an operation which takes time.  Aside from SetGain, users may not call any
 other methods on the AudioCapturer interface after calling StopAsyncCapture
 (including calling StopAsyncCapture again) until after the stop operation has
 completed.  Because of this, it is important for users to be able to
 synchronize with the stop operation.  Two mechanisms are provided for doing
 so.

 The first is to use the StopAsyncCaptureWithCallback method.  When the user's
 callback has been called, they can be certain that stop operation is complete
 and that the AudioCapturer instance has returned to synchronous operation
 mode.

 The second way to determine that a stop operation has completed is to use the
 flags on the packets which get delivered via the user-supplied
 AudioCapturerCallback interface after calling StopAsyncCapture.  When
 asked to stop, any partially filled packet will be returned to the user, and
 the final packet returned will always have the end-of-stream flag (kFlagsEos)
 set on it to indicate that this is the final frame in the sequence.  If
 there is no partially filled packet to return, the AudioCapturer will
 synthesize an empty packet with no timestamp, and offset/length set to zero,
 in order to deliver a packet with the end-of-stream flag set on it.  Once
 users have seen the end-of-stream flag after calling stop, the AudioCapturer
 has finished the stop operation and returned to synchronous operating mode.

 ** Timing and Overflows **

 All media packets produced by an AudioCapturer instance will have their PTS
 field filled out with the capture time of the audio expressed as a timestamp
 given by the `CLOCK_MONOTONIC` timeline.  Note: this timestamp is actually a
 capture timestamp, not a presentation timestamp (it is more of a CTS than a
 PTS) and is meant to represent the underlying system's best estimate of the
 capture time of the first frame of audio, including all outboard and hardware
 introduced buffering delay.  As a result, all timestamps produced by an
 AudioCapturer should be expected to be in the past relative to 'now' on the
 `CLOCK_MONOTONIC` timeline.

 The one exception to the "everything has an explicit timestamp" rule is when
 discarding submitted regions while operating in synchronous mode. Discarded
 packets have no data in them, but FIDL demands that all pending
 method-return-value callbacks be executed.  Because of this, the regions will
 be returned to the user, but their timestamps will be set to
 `NO_TIMESTAMP`, and their payload sizes will be set to zero.  Any
 partially filled payload will have a valid timestamp, but a payload size
 smaller than originally requested.  The final discarded payload (if there
 were any to discard) will be followed by an OnEndOfStream event.

 Two StreamPackets delivered by an AudioCapturer instance are 'continuous' if
 the first frame of audio contained in the second packet was capture exactly
 one nominal frame time after the final frame of audio in the first packet.
 If this relationship does not hold, the second StreamPacket will have the
 'kFlagDiscontinuous' flag set in it's flags field.

 Even though explicit timestamps are provided on every StreamPacket produced,
 users who have very precise timing requirements are encouraged to always
 reason about time by counting frames delivered since the last discontinuity
 instead of simply using the raw capture timestamps.  This is because the
 explicit timestamps written on continuous packets may have a small amount of
 rounding error based on whether or not the units of the capture timeline
 (`CLOCK_MONOTONIC`) are divisible by the chosen audio frame rate.

 Users should always expect the first StreamPacket produced by an
 AudioCapturer to have the discontinuous flag set on it (as there is no
 previous packet to be continuous with). Similarly, the first StreamPacket
 after a DiscardAllPackets or a Stop/Start cycle will always be
 discontinuous. After that, there are only two reasons that a StreamPacket
 will ever be discontinuous:

 1) The user is operating an synchronous mode and does not supply regions to
    be filled quickly enough.  If the next continuous frame of data has not
    been captured by the time it needs to be purged from the source buffers,
    an overflow has occurred and the AudioCapturer will flag the next captured
    region as discontinuous.
 2) The user is operating in asynchronous mode and some internal error
    prevents the AudioCapturer instance from capturing the next frame of audio
    in a continuous fashion.  This might be high system load or a hardware
    error, but in general it is something which should never normally happen.
    In practice, however, if it does, the next produced packet will be flagged
    as being discontinuous.

 ** Synchronous vs. Asynchronous Trade-offs **

 The choice of operating in synchronous vs. asynchronous mode is up to the
 user, and depending on the user's requirements, there are some advantages and
 disadvantages to each choice.

 Synchronous mode requires only a single Zircon channel under the hood and can
 achieve some small savings because of this.  In addition, the user has
 complete control over the buffer management.  Users specify exactly where
 audio will be captured to and in what order.  Because of this, if users do
 not need to always be capturing, it is simple to stop and restart the capture
 later (just by ceasing to supply packets, then resuming later on).  Payloads
 do not need to be uniform in size either, clients may specify payloads of
 whatever granularity is appropriate.

 The primary downside of operating in synchronous mode is that two messages
 will need to be sent for every packet to be captured.  One to inform the
 AudioCapturer of the instance to capture into, and one to inform the user
 that the packet has been captured.  This may end up increasing overhead and
 potentially complicating client designs.

 Asynchronous mode has the advantage requiring only 1/2 of the messages,
 however, when operating in 'async' mode, AudioCapturer instances have no way
 of knowing if a user is processing the StreamPackets being sent in a timely
 fashion, and no way of automatically detecting an overflow condition.  Users
 of 'async' mode should be careful to use a buffer large enough to ensure that
 they will be able to process their data before an AudioCapturer will be
 forced to overwrite it.


### AddPayloadBuffer {:#AddPayloadBuffer}

 Adds a payload buffer to the current buffer set associated with the
 connection. A `StreamPacket` struct reference a payload buffer in the
 current set by ID using the `StreamPacket.payload_buffer_id` field.

 A buffer with ID `id` must not be in the current set when this method is
 invoked, otherwise the service will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>payload_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>



### RemovePayloadBuffer {:#RemovePayloadBuffer}

 Removes a payload buffer from the current buffer set associated with the
 connection.

 A buffer with ID `id` must exist in the current set when this method is
 invoked, otherwise the service will will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### OnPacketProduced {:#OnPacketProduced}

 Delivers a packet produced by the service. When the client is done with
 the payload memory, the client must call `ReleasePacket` to release the
 payload memory.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>

### OnEndOfStream {:#OnEndOfStream}

 Indicates that the stream has ended.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### ReleasePacket {:#ReleasePacket}

 Releases payload memory associated with a packet previously delivered
 via `OnPacketProduced`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>



### DiscardAllPackets {:#DiscardAllPackets}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### DiscardAllPacketsNoReply {:#DiscardAllPacketsNoReply}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetPcmStreamType {:#SetPcmStreamType}

 Sets the stream type of the stream to be delivered.  Causes the source
 material to be reformatted/resampled if needed in order to produce the
 requested stream type. Note that the stream type may not be changed
 after the payload buffer has been established.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_type</code></td>
            <td>
                <code><a class='link' href='#AudioStreamType'>AudioStreamType</a></code>
            </td>
        </tr></table>



### CaptureAt {:#CaptureAt}

 Explicitly specify a region of the shared payload buffer for the audio
 input to capture into.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>payload_buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>payload_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>frames</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>captured_packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>

### StartAsyncCapture {:#StartAsyncCapture}

 Place the AudioCapturer into 'async' capture mode and begin to produce
 packets of exactly 'frames_per_packet' number of frames each. The
 OnPacketProduced event (of StreamSink) will be used to inform the client
 of produced packets.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>frames_per_packet</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### StopAsyncCapture {:#StopAsyncCapture}

 Stop capturing in 'async' capture mode and (optionally) deliver a
 callback that may be used by the client if explicit synchronization
 is needed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### StopAsyncCaptureNoReply {:#StopAsyncCaptureNoReply}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### BindGainControl {:#BindGainControl}

 Binds to the gain control for this AudioCapturer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#GainControl'>GainControl</a>&gt;</code>
            </td>
        </tr></table>



### SetUsage {:#SetUsage}

 Sets the usage of the capture stream.  This may be changed on the fly, but
 packets in flight may be affected by the new usage.  By default the
 Capturer is created with the FOREGROUND usage.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#AudioCaptureUsage'>AudioCaptureUsage</a></code>
            </td>
        </tr></table>



### GetStreamType {:#GetStreamType}

 Gets the currently configured stream type. Note: for an AudioCapturer
 which was just created and has not yet had its stream type explicitly
 set, this will retrieve the stream type -- at the time the AudioCapturer
 was created -- of the source (input or looped-back output) to which the
 AudioCapturer is bound.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_type</code></td>
            <td>
                <code><a class='link' href='#StreamType'>StreamType</a></code>
            </td>
        </tr></table>

## AudioCore {:#AudioCore}
*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#8)*


### CreateAudioRenderer {:#CreateAudioRenderer}

 Create an AudioRenderer which outputs audio to the default device.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>audio_out_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AudioRenderer'>AudioRenderer</a>&gt;</code>
            </td>
        </tr></table>



### CreateAudioCapturer {:#CreateAudioCapturer}

 Create an AudioCapturer which either captures from the current default
 audio input device, or loops-back from the current default audio output
 device based on value passed for the loopback flag.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>loopback</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>audio_in_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#AudioCapturer'>AudioCapturer</a>&gt;</code>
            </td>
        </tr></table>



### SetSystemGain {:#SetSystemGain}

 System Gain and Mute

 Fuchsia clients control the volume of individual audio streams via the
 fuchsia.media.audio.GainControl protocol. System Gain and Mute affect
 all audio output, and are controlled with methods that use the same
 concepts as GainControl, namely: independent gain and mute, with change
 notifications. Setting System Mute to true leads to the same outcome as
 setting System Gain to MUTED_GAIN_DB: all audio output across the system
 is silenced.
 Sets the systemwide gain in decibels. `gain_db` values are clamped to
 the range -160 db to 0 db, inclusive. This setting is applied to all
 audio output devices. Audio input devices are unaffected.
 Does not affect System Mute.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetSystemMute {:#SetSystemMute}

 Sets/clears the systemwide 'Mute' state for audio output devices.
 Audio input devices are unaffected. Changes to the System Mute state do
 not affect the value of System Gain.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SystemGainMuteChanged {:#SystemGainMuteChanged}

 Provides current values for systemwide Gain and Mute. When a client
 connects to AudioCore, the system immediately sends that client a
 SystemGainMuteChanged event with the current system Gain|Mute settings.
 Subsequent events will be sent when these Gain|Mute values change.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### SetRoutingPolicy {:#SetRoutingPolicy}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>policy</code></td>
            <td>
                <code><a class='link' href='#AudioOutputRoutingPolicy'>AudioOutputRoutingPolicy</a></code>
            </td>
        </tr></table>



### EnableDeviceSettings {:#EnableDeviceSettings}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### SetRenderUsageGain {:#SetRenderUsageGain}

 Set the Usage gain applied to Renderers. By default, the gain for all
 render usages is set to Unity (0 db).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#AudioRenderUsage'>AudioRenderUsage</a></code>
            </td>
        </tr><tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetCaptureUsageGain {:#SetCaptureUsageGain}

 Set the Usage gain applied to Capturers. By default, the gain for all
 capture usages is set to Unity (0 db).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#AudioCaptureUsage'>AudioCaptureUsage</a></code>
            </td>
        </tr><tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



## AudioDeviceEnumerator {:#AudioDeviceEnumerator}
*Defined in [fuchsia.media/audio_device_enumerator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#34)*


### GetDevices {:#GetDevices}

 Obtain the list of currently active audio devices.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>devices</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AudioDeviceInfo'>AudioDeviceInfo</a>&gt;</code>
            </td>
        </tr></table>

### OnDeviceAdded {:#OnDeviceAdded}

 Events sent when devices are added or removed, or when properties of a
 device change.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device</code></td>
            <td>
                <code><a class='link' href='#AudioDeviceInfo'>AudioDeviceInfo</a></code>
            </td>
        </tr></table>

### OnDeviceRemoved {:#OnDeviceRemoved}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### OnDeviceGainChanged {:#OnDeviceGainChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>gain_info</code></td>
            <td>
                <code><a class='link' href='#AudioGainInfo'>AudioGainInfo</a></code>
            </td>
        </tr></table>

### OnDefaultDeviceChanged {:#OnDefaultDeviceChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>old_default_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>new_default_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### GetDeviceGain {:#GetDeviceGain}

 Gain/Mute/AGC control

 Note that each of these operations requires a device_token in order to
 target the proper input/output.

 The Get command returns the device_token of the device whose gain is
 being reported, or `ZX_KOID_INVALID` in the case that the requested
 device_token was invalid or the device had been removed from the system
 before the Get command could be processed.

 Set commands which are given an invalid device token are ignored and
 have no effect on the system. In addition, users do not need to control
 all of the gain settings for an audio device with each call. Only the
 settings with a corresponding flag set in the set_flags parameter will
 be affected. For example, passing SetAudioGainFlag_MuteValid will cause
 a SetDeviceGain call to care only about the mute setting in the
 gain_info structure, while passing (SetAudioGainFlag_GainValid |
 SetAudioGainFlag_MuteValid) will cause both the mute and the gain
 status to be changed simultaneously.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>gain_info</code></td>
            <td>
                <code><a class='link' href='#AudioGainInfo'>AudioGainInfo</a></code>
            </td>
        </tr></table>

### SetDeviceGain {:#SetDeviceGain}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>gain_info</code></td>
            <td>
                <code><a class='link' href='#AudioGainInfo'>AudioGainInfo</a></code>
            </td>
        </tr><tr>
            <td><code>set_flags</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### GetDefaultInputDevice {:#GetDefaultInputDevice}

 Default Device

 Fetch the device ID of the current default input or output device, or
 `ZX_KOID_INVALID` if no such device exists.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### GetDefaultOutputDevice {:#GetDefaultOutputDevice}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_token</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>

### AddDeviceByChannel {:#AddDeviceByChannel}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_channel</code></td>
            <td>
                <code>handle&lt;channel&gt;</code>
            </td>
        </tr><tr>
            <td><code>device_name</code></td>
            <td>
                <code>string[256]</code>
            </td>
        </tr><tr>
            <td><code>is_input</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



## AudioRenderer {:#AudioRenderer}
*Defined in [fuchsia.media/audio_renderer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_renderer.fidl#23)*


 AudioRenderers can be in one of two states at any point in time, either
 the configurable state or the operational state. A renderer is considered
 to be operational any time it has packets queued and waiting to be
 rendered; otherwise it is considered to be in the configurable state. When an
 AudioRenderer has entered the operational state of its life, any attempt to
 call a config method in the interface is considered to be illegal and will
 result in termination of the interface's connection to the audio service.

 If an AudioRenderer must be reconfigured, it is best practice to always call
 `DiscardAllPackets` on the AudioRenderer, before starting to reconfigure it.


### AddPayloadBuffer {:#AddPayloadBuffer}

 Adds a payload buffer to the current buffer set associated with the
 connection. A `StreamPacket` struct reference a payload buffer in the
 current set by ID using the `StreamPacket.payload_buffer_id` field.

 A buffer with ID `id` must not be in the current set when this method is
 invoked, otherwise the service will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>payload_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>



### RemovePayloadBuffer {:#RemovePayloadBuffer}

 Removes a payload buffer from the current buffer set associated with the
 connection.

 A buffer with ID `id` must exist in the current set when this method is
 invoked, otherwise the service will will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SendPacket {:#SendPacket}

 Sends a packet to the service. The response is sent when the service is
 done with the associated payload memory.

 `packet` must be valid for the current buffer set, otherwise the service
 will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SendPacketNoReply {:#SendPacketNoReply}

 Sends a packet to the service. This interface doesn't define how the
 client knows when the sink is done with the associated payload memory.
 The inheriting interface must define that.

 `packet` must be valid for the current buffer set, otherwise the service
 will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>



### EndOfStream {:#EndOfStream}

 Indicates the stream has ended. The precise semantics of this method are
 determined by the inheriting interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### DiscardAllPackets {:#DiscardAllPackets}

 Discards packets previously sent via `SendPacket` or `SendPacketNoReply`
 and not yet released. The response is sent after all packets have been
 released.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### DiscardAllPacketsNoReply {:#DiscardAllPacketsNoReply}

 Discards packets previously sent via `SendPacket` or `SendPacketNoReply`
 and not yet released.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### SetPcmStreamType {:#SetPcmStreamType}

 Sets the type of the stream to be delivered by the client. Using this
 method implies that the stream encoding is `AUDIO_ENCODING_LPCM`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#AudioStreamType'>AudioStreamType</a></code>
            </td>
        </tr></table>



### SetStreamType {:#SetStreamType}

 Sets the stream type to be delivered by the client. This method is used
 for compressed pass-through. The media_specific field must be of type
 audio.
 NOTE: Not currently implemented.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#StreamType'>StreamType</a></code>
            </td>
        </tr></table>



### SetPtsUnits {:#SetPtsUnits}

 Sets the units used by the presentation (media) timeline. By default, PTS
 units are nanoseconds (as if this were called with values of 1e9 and 1).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>tick_per_second_numerator</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>tick_per_second_denominator</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SetPtsContinuityThreshold {:#SetPtsContinuityThreshold}

 Sets the maximum threshold (in frames) between an explicit PTS (user-
 provided) and an expected PTS (determined using interpolation). Beyond
 this threshold, a stream is no longer considered 'continuous' by the
 renderer.

 Defaults to RoundUp((AudioFPS/PTSTicksPerSec) / 2.0) / AudioFPS
 Most users should not need to change this value from its default.

 Example:
 A user is playing back 48KHz audio from a container, which also contains
 video and needs to be synchronized with the audio. The timestamps are
 provided explicitly per packet by the container, and expressed in mSec
 units. This means that a single tick of the media timeline (1 mSec)
 represents exactly 48 frames of audio. The application in this scenario
 delivers packets of audio to the AudioRenderer, each with exactly 470
 frames of audio, and each with an explicit timestamp set to the best
 possible representation of the presentation time (given this media
 clock's resolution). So, starting from zero, the timestamps would be..

 [ 0, 10, 20, 29, 39, 49, 59, 69, 78, 88, ... ]

 In this example, attempting to use the presentation time to compute the
 starting frame number of the audio in the packet would be wrong the
 majority of the time. The first timestamp is correct (by definition), but
 it will be 24 packets before the timestamps and frame numbers come back
 into alignment (the 24th packet would start with the 11280th audio frame
 and have a PTS of exactly 235).

 One way to fix this situation is to set the PTS continuity threshold
 (henceforth, CT) for the stream to be equal to 1/2 of the time taken by
 the number of frames contained within a single tick of the media clock,
 rounded up. In this scenario, that would be 24.0 frames of audio, or 500
 uSec. Any packets whose expected PTS was within +/-CT frames of the
 explicitly provided PTS would be considered to be a continuation of the
 previous frame of audio.

 Other possible uses:
 Users who are scheduling audio explicitly, relative to a clock which has
 not been configured as the reference clock, can use this value to control
 the maximum acceptable synchronization error before a discontinuity is
 introduced. E.g., if a user is scheduling audio based on a recovered
 common media clock, and has not published that clock as the reference
 clock, and they set the CT to 20mSec, then up to 20mSec of drift error
 can accumulate before the AudioRenderer deliberately inserts a
 presentation discontinuity to account for the error.

 Users whose need to deal with a container where their timestamps may be
 even less correct than +/- 1/2 of a PTS tick may set this value to
 something larger. This should be the maximum level of inaccuracy present
 in the container timestamps, if known. Failing that, it could be set to
 the maximum tolerable level of drift error before absolute timestamps are
 explicitly obeyed. Finally, a user could set this number to a very large
 value (86400.0 seconds, for example) to effectively cause *all*
 timestamps to be ignored after the first, thus treating all audio as
 continuous with previously delivered packets. Conversely, users who wish
 to *always* explicitly schedule their audio packets exactly may specify
 a CT of 0.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>threshold_seconds</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetReferenceClock {:#SetReferenceClock}

 Set the reference clock used to control playback rate.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reference_clock</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
        </tr></table>



### Play {:#Play}

 Immediately put the AudioRenderer into a playing state. Start the advance
 of the media timeline, using specific values provided by the caller (or
 default values if not specified). In an optional callback, return the
 timestamp values ultimately used -- these set the ongoing relationship
 between the media and reference timelines (i.e., how to translate between
 the domain of presentation timestamps, and the realm of local system
 time).

 Local system time is specified in units of nanoseconds; media_time is
 specified in the units defined by the user in the `SetPtsUnits` function,
 or nanoseconds if `SetPtsUnits` is not called.

 The act of placing an AudioRenderer into the playback state establishes a
 relationship between 1) the user-defined media (or presentation) timeline
 for this particular AudioRenderer, and 2) the real-world system reference
 timeline. To communicate how to translate between timelines, the Play()
 callback provides an equivalent timestamp in each time domain. The first
 value ('reference_time') is given in terms of the local system clock; the
 second value ('media_time') is what media instant exactly corresponds to
 that local time. Restated, the frame at 'media_time' in the audio stream
 should be presented at system local time 'reference_time'.

 Note: on calling this API, media_time immediately starts advancing. It is
 possible (if uncommon) for a caller to specify a system time that is
 far in the past, or far into the future. This, along with the specified
 media time, is simply used to determine what media time corresponds to
 'now', and THAT media time is then intersected with presentation
 timestamps of packets already submitted, to determine which media frames
 should be presented next.

 With the corresponding reference_time and media_time values, a user can
 translate arbitrary time values from one timeline into the other. After
 calling `SetPtsUnits(pts_per_sec_numerator, pts_per_sec_denominator)` and
 given the 'ref_start' and 'media_start' values from `Play()`, then for
 any 'ref_time':

 media_time = ( (ref_time - ref_start) / 1e9
                * (pts_per_sec_numerator / pts_per_sec_denominator) )
              + media_start

 Conversely, for any presentation timestamp 'media_time':

 ref_time = ( (media_time - media_start)
              * (pts_per_sec_denominator / pts_per_sec_numerator)
              * 1e9 )
            + ref_start

 Users, depending on their use case, may optionally choose not to specify
 one or both of these timestamps. A timestamp may be omitted by supplying
 the special value '`NO_TIMESTAMP`'. The AudioRenderer automatically deduces
 any omitted timestamp value using the following rules:

 Reference Time
 If 'reference_time' is omitted, the AudioRenderer will select a "safe"
 reference time to begin presentation, based on the minimum lead times for
 the output devices that are currently bound to this AudioRenderer. For
 example, if an AudioRenderer is bound to an internal audio output
 requiring at least 3 mSec of lead time, and an HDMI output requiring at
 least 75 mSec of lead time, the AudioRenderer might (if 'reference_time'
 is omitted) select a reference time 80 mSec from now.

 Media Time
 If media_time is omitted, the AudioRenderer will select one of two
 values.
 - If the AudioRenderer is resuming from the paused state, and packets
 have not been discarded since being paused, then the AudioRenderer will
 use a media_time corresponding to the instant at which the presentation
 became paused.
 - If the AudioRenderer is being placed into a playing state for the first
 time following startup or a 'discard packets' operation, the initial
 media_time will be set to the PTS of the first payload in the pending
 packet queue. If the pending queue is empty, initial media_time will be
 set to zero.

 Return Value
 When requested, the AudioRenderer will return the 'reference_time' and
 'media_time' which were selected and used (whether they were explicitly
 specified or not) in the return value of the play call.

 Examples
 1. A user has queued some audio using `SendPacket` and simply wishes them
 to start playing as soon as possible. The user may call Play without
 providing explicit timestamps -- `Play(NO_TIMESTAMP, NO_TIMESTAMP)`.

 2. A user has queued some audio using `SendPacket`, and wishes to start
 playback at a specified 'reference_time', in sync with some other media
 stream, either initially or after discarding packets. The user would call
 `Play(reference_time, NO_TIMESTAMP)`.

 3. A user has queued some audio using `SendPacket`. The first of these
 packets has a PTS of zero, and the user wishes playback to begin as soon
 as possible, but wishes to skip all of the audio content between PTS 0
 and PTS 'media_time'. The user would call
 `Play(NO_TIMESTAMP, media_time)`.

 4. A user has queued some audio using `SendPacket` and want to present
 this media in synch with another player in a different device. The
 coordinator of the group of distributed players sends an explicit
 message to each player telling them to begin presentation of audio at
 PTS 'media_time', at the time (based on the group's shared reference
 clock) 'reference_time'. Here the user would call
 `Play(reference_time, media_time)`.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reference_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>media_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reference_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>media_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### PlayNoReply {:#PlayNoReply}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reference_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>media_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>



### Pause {:#Pause}

 Immediately put the AudioRenderer into the paused state and then report
 the relationship between the media and reference timelines which was
 established (if requested).


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reference_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>media_time</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### PauseNoReply {:#PauseNoReply}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### EnableMinLeadTimeEvents {:#EnableMinLeadTimeEvents}

 Enable or disable notifications about changes to the minimum clock lead
 time (in nanoseconds) for this AudioRenderer. Calling this method with
 'enabled' set to true will trigger an immediate `OnMinLeadTimeChanged`
 event with the current minimum lead time for the AudioRenderer. If the
 value changes, an `OnMinLeadTimeChanged` event will be raised with the
 new value. This behavior will continue until the user calls
 `EnableMinLeadTimeEvents(false)`.

 The minimum clock lead time is the amount of time ahead of the reference
 clock's understanding of "now" that packets needs to arrive (relative to
 the playback clock transformation) in order for the mixer to be able to
 mix packet. For example...

 ++ Let the PTS of packet X be P(X)
 ++ Let the function which transforms PTS -> RefClock be R(p) (this
    function is determined by the call to Play(...)
 ++ Let the minimum lead time be MLT

 If R(P(X)) < RefClock.Now() + MLT
 Then the packet is late, and some (or all) of the packet's payload will
 need to be skipped in order to present the packet at the scheduled time.


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnMinLeadTimeChanged {:#OnMinLeadTimeChanged}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_lead_time_nsec</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### GetMinLeadTime {:#GetMinLeadTime}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>min_lead_time_nsec</code></td>
            <td>
                <code>int64</code>
            </td>
        </tr></table>

### BindGainControl {:#BindGainControl}

 Binds to the gain control for this AudioRenderer.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_control_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#GainControl'>GainControl</a>&gt;</code>
            </td>
        </tr></table>



### SetUsage {:#SetUsage}

 Sets the usage of the render stream.  This may be changed on the fly, but
 packets in flight may be affected by the new usage.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#AudioRenderUsage'>AudioRenderUsage</a></code>
            </td>
        </tr></table>



## StreamBufferSet {:#StreamBufferSet}
*Defined in [fuchsia.media/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#15)*

 Manages a set of payload buffers for a stream. This interface is typically
 inherited along with `StreamSink` or `StreamSource` to enable the transport
 of elementary streams between clients and services.

### AddPayloadBuffer {:#AddPayloadBuffer}

 Adds a payload buffer to the current buffer set associated with the
 connection. A `StreamPacket` struct reference a payload buffer in the
 current set by ID using the `StreamPacket.payload_buffer_id` field.

 A buffer with ID `id` must not be in the current set when this method is
 invoked, otherwise the service will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>payload_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>



### RemovePayloadBuffer {:#RemovePayloadBuffer}

 Removes a payload buffer from the current buffer set associated with the
 connection.

 A buffer with ID `id` must exist in the current set when this method is
 invoked, otherwise the service will will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



## StreamSink {:#StreamSink}
*Defined in [fuchsia.media/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#36)*

 Consumes a stream of packets. This interface is typically inherited along
 with `StreamBufferSet` to enable the transport of elementary streams from
 clients to services.

### SendPacket {:#SendPacket}

 Sends a packet to the service. The response is sent when the service is
 done with the associated payload memory.

 `packet` must be valid for the current buffer set, otherwise the service
 will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SendPacketNoReply {:#SendPacketNoReply}

 Sends a packet to the service. This interface doesn't define how the
 client knows when the sink is done with the associated payload memory.
 The inheriting interface must define that.

 `packet` must be valid for the current buffer set, otherwise the service
 will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>



### EndOfStream {:#EndOfStream}

 Indicates the stream has ended. The precise semantics of this method are
 determined by the inheriting interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### DiscardAllPackets {:#DiscardAllPackets}

 Discards packets previously sent via `SendPacket` or `SendPacketNoReply`
 and not yet released. The response is sent after all packets have been
 released.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### DiscardAllPacketsNoReply {:#DiscardAllPacketsNoReply}

 Discards packets previously sent via `SendPacket` or `SendPacketNoReply`
 and not yet released.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## StreamSource {:#StreamSource}
*Defined in [fuchsia.media/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#70)*

 Produces a stream of packets. This interface is typically inherited along
 with `StreamBufferSet` to enable the transport of elementary streams from
 services to clients.

### OnPacketProduced {:#OnPacketProduced}

 Delivers a packet produced by the service. When the client is done with
 the payload memory, the client must call `ReleasePacket` to release the
 payload memory.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>

### OnEndOfStream {:#OnEndOfStream}

 Indicates that the stream has ended.



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### ReleasePacket {:#ReleasePacket}

 Releases payload memory associated with a packet previously delivered
 via `OnPacketProduced`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>



### DiscardAllPackets {:#DiscardAllPackets}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### DiscardAllPacketsNoReply {:#DiscardAllPacketsNoReply}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## SimpleStreamSink {:#SimpleStreamSink}
*Defined in [fuchsia.media/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#97)*

 A StreamSink that uses StreamBufferSet for buffer management.

### AddPayloadBuffer {:#AddPayloadBuffer}

 Adds a payload buffer to the current buffer set associated with the
 connection. A `StreamPacket` struct reference a payload buffer in the
 current set by ID using the `StreamPacket.payload_buffer_id` field.

 A buffer with ID `id` must not be in the current set when this method is
 invoked, otherwise the service will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr><tr>
            <td><code>payload_buffer</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
        </tr></table>



### RemovePayloadBuffer {:#RemovePayloadBuffer}

 Removes a payload buffer from the current buffer set associated with the
 connection.

 A buffer with ID `id` must exist in the current set when this method is
 invoked, otherwise the service will will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>id</code></td>
            <td>
                <code>uint32</code>
            </td>
        </tr></table>



### SendPacket {:#SendPacket}

 Sends a packet to the service. The response is sent when the service is
 done with the associated payload memory.

 `packet` must be valid for the current buffer set, otherwise the service
 will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SendPacketNoReply {:#SendPacketNoReply}

 Sends a packet to the service. This interface doesn't define how the
 client knows when the sink is done with the associated payload memory.
 The inheriting interface must define that.

 `packet` must be valid for the current buffer set, otherwise the service
 will close the connection.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#StreamPacket'>StreamPacket</a></code>
            </td>
        </tr></table>



### EndOfStream {:#EndOfStream}

 Indicates the stream has ended. The precise semantics of this method are
 determined by the inheriting interface.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### DiscardAllPackets {:#DiscardAllPackets}

 Discards packets previously sent via `SendPacket` or `SendPacketNoReply`
 and not yet released. The response is sent after all packets have been
 released.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### DiscardAllPacketsNoReply {:#DiscardAllPacketsNoReply}

 Discards packets previously sent via `SendPacket` or `SendPacketNoReply`
 and not yet released.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



## StreamProcessor {:#StreamProcessor}
*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#1025)*


### EnableOnStreamFailed {:#EnableOnStreamFailed}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnStreamFailed {:#OnStreamFailed}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#StreamError'>StreamError</a></code>
            </td>
        </tr></table>

### OnStreamFailed2 {:#OnStreamFailed2}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>error</code></td>
            <td>
                <code><a class='link' href='#StreamError'>StreamError</a></code>
            </td>
        </tr></table>

### OnInputConstraints {:#OnInputConstraints}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input_constraints</code></td>
            <td>
                <code><a class='link' href='#StreamBufferConstraints'>StreamBufferConstraints</a></code>
            </td>
        </tr></table>

### SetInputBufferSettings {:#SetInputBufferSettings}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input_settings</code></td>
            <td>
                <code><a class='link' href='#StreamBufferSettings'>StreamBufferSettings</a></code>
            </td>
        </tr></table>



### AddInputBuffer {:#AddInputBuffer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='#StreamBuffer'>StreamBuffer</a></code>
            </td>
        </tr></table>



### SetInputBufferPartialSettings {:#SetInputBufferPartialSettings}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>input_settings</code></td>
            <td>
                <code><a class='link' href='#StreamBufferPartialSettings'>StreamBufferPartialSettings</a></code>
            </td>
        </tr></table>



### OnOutputConstraints {:#OnOutputConstraints}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_config</code></td>
            <td>
                <code><a class='link' href='#StreamOutputConstraints'>StreamOutputConstraints</a></code>
            </td>
        </tr></table>

### OnOutputFormat {:#OnOutputFormat}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_format</code></td>
            <td>
                <code><a class='link' href='#StreamOutputFormat'>StreamOutputFormat</a></code>
            </td>
        </tr></table>

### SetOutputBufferSettings {:#SetOutputBufferSettings}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_settings</code></td>
            <td>
                <code><a class='link' href='#StreamBufferSettings'>StreamBufferSettings</a></code>
            </td>
        </tr></table>



### AddOutputBuffer {:#AddOutputBuffer}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer</code></td>
            <td>
                <code><a class='link' href='#StreamBuffer'>StreamBuffer</a></code>
            </td>
        </tr></table>



### SetOutputBufferPartialSettings {:#SetOutputBufferPartialSettings}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_settings</code></td>
            <td>
                <code><a class='link' href='#StreamBufferPartialSettings'>StreamBufferPartialSettings</a></code>
            </td>
        </tr></table>



### CompleteOutputBufferPartialSettings {:#CompleteOutputBufferPartialSettings}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### FlushEndOfStreamAndCloseStream {:#FlushEndOfStreamAndCloseStream}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



### CloseCurrentStream {:#CloseCurrentStream}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>release_input_buffers</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>release_output_buffers</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### Sync {:#Sync}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnOutputPacket {:#OnOutputPacket}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>output_packet</code></td>
            <td>
                <code><a class='link' href='#Packet'>Packet</a></code>
            </td>
        </tr><tr>
            <td><code>error_detected_before</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr><tr>
            <td><code>error_detected_during</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### RecycleOutputPacket {:#RecycleOutputPacket}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>available_output_packet</code></td>
            <td>
                <code><a class='link' href='#PacketHeader'>PacketHeader</a></code>
            </td>
        </tr></table>



### OnOutputEndOfStream {:#OnOutputEndOfStream}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>error_detected_before</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### QueueInputFormatDetails {:#QueueInputFormatDetails}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr><tr>
            <td><code>format_details</code></td>
            <td>
                <code><a class='link' href='#FormatDetails'>FormatDetails</a></code>
            </td>
        </tr></table>



### QueueInputPacket {:#QueueInputPacket}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>packet</code></td>
            <td>
                <code><a class='link' href='#Packet'>Packet</a></code>
            </td>
        </tr></table>



### OnFreeInputPacket {:#OnFreeInputPacket}




#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>free_input_packet</code></td>
            <td>
                <code><a class='link' href='#PacketHeader'>PacketHeader</a></code>
            </td>
        </tr></table>

### QueueInputEndOfStream {:#QueueInputEndOfStream}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>





## **STRUCTS**

### AudioGainInfo {:#AudioGainInfo}
*Defined in [fuchsia.media/audio_device_enumerator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#11)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AudioDeviceInfo {:#AudioDeviceInfo}
*Defined in [fuchsia.media/audio_device_enumerator.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>unique_id</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>token_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_input</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>gain_info</code></td>
            <td>
                <code><a class='link' href='#AudioGainInfo'>AudioGainInfo</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>is_default</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Metadata {:#Metadata}
*Defined in [fuchsia.media/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#8)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>properties</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Property'>Property</a>&gt;</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Property {:#Property}
*Defined in [fuchsia.media/metadata.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#12)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>label</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StreamPacket {:#StreamPacket}
*Defined in [fuchsia.media/stream.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#103)*



 Describes a packet consumed by `StreamSink` or produced by `StreamSource`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pts</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> Time at which the packet is to be presented, according to the
 presentation clock.
</td>
            <td><a class='link' href='#NO_TIMESTAMP'>NO_TIMESTAMP</a></td>
        </tr><tr>
            <td><code>payload_buffer_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> ID of the payload buffer used for this packet.

 When this struct is used with `StreamBufferSet`, this field is the ID of
 a payload buffer provided via `StreamBufferSet.AddPayloadBuffer`. In
 that case, this value must identify a payload buffer in the current set.
 Other interfaces may define different semantics for this field.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>payload_offset</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Offset of the packet payload in the payload buffer.

 This value plus the `payload_size` value must be less than or equal to
 the size of the referenced payload buffer.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>payload_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Size in bytes of the payload.

 This value plus the `payload_offest` value must be less than or equal to
 the size of the referenced payload buffer.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>flags</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> An bitwise-or'ed set of flags (see constants below) describing
 properties of this packet.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>buffer_config</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The buffer configuration associated with this packet. The semantics of
 this field depend on the interface with which this struct is used.
 In many contexts, this field is not used. This field is intended for
 situations in which buffer configurations (i.e. sets of payload buffers)
 are explicitly identified. In such cases, the `payload_buffer_id` refers
 to a payload buffer in the buffer configuration identified by this
 field.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>stream_segment_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The stream segment associated with this packet. The semantics of this
 field depend on the interface with which this struct is used. In many
 contexts, this field is not used. This field is intended to distinguish
 contiguous segments of the stream where stream properties (e.g.
 encoding) may differ from segment to segment.
</td>
            <td>0</td>
        </tr>
</table>

### Parameter {:#Parameter}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#33)*



 Parameter

 Generic parameter.

 We want to minimize use of this generic "Parameter" structure by natively
 defining as many stream-specific parameter semantics as we can.



<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>scope</code></td>
            <td>
                <code>string</code>
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
        </tr><tr>
            <td><code>value</code></td>
            <td>
                <code><a class='link' href='#Value'>Value</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### AudioCompressedFormatAac {:#AudioCompressedFormatAac}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#89)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AudioCompressedFormatSbc {:#AudioCompressedFormatSbc}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#92)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### PcmFormat {:#PcmFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#151)*



 PcmFormat

 PCM audio format details.



<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pcm_mode</code></td>
            <td>
                <code><a class='link' href='#AudioPcmMode'>AudioPcmMode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bits_per_sample</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channel_map</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AudioChannelId'>AudioChannelId</a>&gt;[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VideoUncompressedFormat {:#VideoUncompressedFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#232)*



 VideoUncompressedFormat

 Uncompressed video format details.



<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>image_format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#ImageFormat_2'>ImageFormat_2</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>fourcc</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_width_pixels</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_height_pixels</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>secondary_width_pixels</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>secondary_height_pixels</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>planar</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>swizzled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_line_stride_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>secondary_line_stride_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_start_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>secondary_start_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>tertiary_start_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_pixel_stride</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>secondary_pixel_stride</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_display_width_pixels</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>primary_display_height_pixels</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>has_pixel_aspect_ratio</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
            <td>false</td>
        </tr><tr>
            <td><code>pixel_aspect_ratio_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>1</td>
        </tr><tr>
            <td><code>pixel_aspect_ratio_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>1</td>
        </tr>
</table>

### KeyId {:#KeyId}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#338)*



 KeyId

 An encryption key identifier.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>data</code></td>
            <td>
                <code>uint8[16]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SubsampleEntry {:#SubsampleEntry}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#347)*



 SubsampleEntry

 A subsample is a byte range within a sample consisting of a clear byte range
 followed by an encrypted byte range. This structure specifies the size of
 each range in the subsample.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>clear_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>encrypted_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### EncryptionPattern {:#EncryptionPattern}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#358)*



 EncryptionPattern

 Pattern encryption utilizes a pattern of encrypted and clear 16 byte blocks
 over the protected range of a subsample (the encrypted_bytes of a
 `SubsampleEntry`). This structure specifies the number of encrypted data
 blocks followed by the number of clear data blocks.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>clear_blocks</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>encrypted_blocks</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SbcEncoderSettings {:#SbcEncoderSettings}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#472)*



 Settings for an SBC Encoder.

 SBC Encoders take signed little endian 16 bit linear PCM samples and
 return encoded SBC frames. SBC encoder PCM data in batches of
 `sub_bands * block_count` PCM frames. This encoder will accept PCM data on
 arbitrary frame boundaries, but the output flushed when EOS is queued may be
 zero-padded to make a full batch for encoding.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sub_bands</code></td>
            <td>
                <code><a class='link' href='#SbcSubBands'>SbcSubBands</a></code>
            </td>
            <td></td>
            <td><a class='link' href='#SbcSubBands.SUB_BANDS_8'>SbcSubBands.SUB_BANDS_8</a></td>
        </tr><tr>
            <td><code>allocation</code></td>
            <td>
                <code><a class='link' href='#SbcAllocation'>SbcAllocation</a></code>
            </td>
            <td></td>
            <td><a class='link' href='#SbcAllocation.ALLOC_LOUDNESS'>SbcAllocation.ALLOC_LOUDNESS</a></td>
        </tr><tr>
            <td><code>block_count</code></td>
            <td>
                <code><a class='link' href='#SbcBlockCount'>SbcBlockCount</a></code>
            </td>
            <td></td>
            <td><a class='link' href='#SbcBlockCount.BLOCK_COUNT_4'>SbcBlockCount.BLOCK_COUNT_4</a></td>
        </tr><tr>
            <td><code>channel_mode</code></td>
            <td>
                <code><a class='link' href='#SbcChannelMode'>SbcChannelMode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bit_pool</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> SBC bit pool value.
</td>
            <td>No default</td>
        </tr>
</table>

### AacTransportRaw {:#AacTransportRaw}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#482)*



 Raw AAC access units.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### AacConstantBitRate {:#AacConstantBitRate}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#494)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>bit_rate</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Bits per second
</td>
            <td>No default</td>
        </tr>
</table>

### AacEncoderSettings {:#AacEncoderSettings}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#521)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>transport</code></td>
            <td>
                <code><a class='link' href='#AacTransport'>AacTransport</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channel_mode</code></td>
            <td>
                <code><a class='link' href='#AacChannelMode'>AacChannelMode</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>bit_rate</code></td>
            <td>
                <code><a class='link' href='#AacBitRate'>AacBitRate</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>aot</code></td>
            <td>
                <code><a class='link' href='#AacAudioObjectType'>AacAudioObjectType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### StreamType {:#StreamType}
*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#14)*



 Describes the type of an elementary stream.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>medium_specific</code></td>
            <td>
                <code><a class='link' href='#MediumSpecificStreamType'>MediumSpecificStreamType</a></code>
            </td>
            <td> Medium-specific type information.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>encoding</code></td>
            <td>
                <code>string[255]</code>
            </td>
            <td> Encoding (see constants below). This value is represented as a string
 so that new encodings can be introduced without modifying this file.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>encoding_parameters</code></td>
            <td>
                <code>vector&lt;uint8&gt;?</code>
            </td>
            <td> Encoding-specific parameters, sometimes referred to as 'out-of-band
 data'. Typically, this data is associated with a compressed stream and
 provides parameters required to decompress the stream. This data is
 generally opaque to all parties except the producer and consumer of the
 stream.
</td>
            <td>No default</td>
        </tr>
</table>

### AudioStreamType {:#AudioStreamType}
*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#66)*



 Describes the type of an audio elementary stream.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>sample_format</code></td>
            <td>
                <code><a class='link' href='#AudioSampleFormat'>AudioSampleFormat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>channels</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>frames_per_second</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### VideoStreamType {:#VideoStreamType}
*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#92)*



 Describes the type of a video elementary stream.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>pixel_format</code></td>
            <td>
                <code><a class='link' href='../fuchsia.images/index.html'>fuchsia.images</a>/<a class='link' href='../fuchsia.images/index.html#PixelFormat'>PixelFormat</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>color_space</code></td>
            <td>
                <code><a class='link' href='#ColorSpace'>ColorSpace</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Dimensions of the video frames as displayed in pixels.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>coded_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Dimensions of the video frames as encoded in pixels. These values must
 be equal to or greater than the respective width/height values.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>coded_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_aspect_ratio_width</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The aspect ratio of a single pixel as frames are intended to be
 displayed.
</td>
            <td>No default</td>
        </tr><tr>
            <td><code>pixel_aspect_ratio_height</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>stride</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The number of bytes per 'coded' row in the primary video plane.
</td>
            <td>No default</td>
        </tr>
</table>

### TextStreamType {:#TextStreamType}
*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#128)*



 Describes the type of a text elementary stream.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### SubpictureStreamType {:#SubpictureStreamType}
*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#136)*



 Describes the type of a subpicture elementary stream.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### TimelineFunction {:#TimelineFunction}
*Defined in [fuchsia.media/timeline_function.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/timeline_function.fidl#42)*



 A TimelineFunction represents a relationship between a subject timeline and a
 reference timeline with a linear relation.

 For example, consider a common use case in which reference time is the
 monotonic clock of a system and subject time is intended presentation time
 for some media such as a video.

 `reference_time` is the value of the monotonic clock at the beginning of
 playback. `subject_time` is 0 assuming playback starts at the beginning of
 the media. We then choose a `reference_delta` and `subject_delta` so that
 `subject_delta` / `reference_delta` represents the desired playback rate,
 e.g. 0/1 for paused and 1/1 for normal playback.

 ## Formulas

 With a function we can determine the subject timeline value `s` in terms of
 reference timeline value `r` with this formula (where `reference_delta` > 0):

   s = (r - reference_time) * (subject_delta / reference_delta) + subject_time

 And similarly we can find the reference timeline value `r` in terms of
 subject timeline value `s` with this formula (where `subject_delta` > 0):

   r = (s - subject_time) * (reference_delta / subject_delta) + referenc_time

 ## Choosing time values

 Time values can be arbitrary and our linear relation will of course be the
 same, but we can use them to represent the bounds of pieces in a piecewise
 linear relation.

 For example, if a user performs skip-chapter, we might want to describe
 this with a TimelineFunction whose `subject_time` is the time to skip to,
 `reference_time` is now plus some epsilon, and delta ratio is 1/1 for normal
 playback rate.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>subject_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> A value from the subject timeline that correlates to reference_time.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>reference_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td> A value from the reference timeline that correlates to subject_time.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>subject_delta</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The change in the subject timeline corresponding to reference_delta.
</td>
            <td>0</td>
        </tr><tr>
            <td><code>reference_delta</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The change in the reference timeline corresponding to subject_delta.
 Cannot be zero.
</td>
            <td>1</td>
        </tr>
</table>



## **ENUMS**

### AudioRenderUsage {:#AudioRenderUsage}
Type: <code>uint32</code>

*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#81)*

 Usage annotating the purpose of the stream being used to render audio.
 An AudioRenderer's usage cannot be changed after creation.  The
 AudioRenderUsage is used by audio policy to dictate how audio streams
 interact with each other.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BACKGROUND</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>MEDIA</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INTERRUPTION</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_AGENT</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMUNICATION</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### AudioCaptureUsage {:#AudioCaptureUsage}
Type: <code>uint32</code>

*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#108)*

 Usages annotating the purpose of the stream being used to capture audio. The
 AudioCaptureUsage is used by audio policy to dictate how audio streams
 interact with each other.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BACKGROUND</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>FOREGROUND</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SYSTEM_AGENT</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>COMMUNICATION</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### AudioOutputRoutingPolicy {:#AudioOutputRoutingPolicy}
Type: <code>uint32</code>

*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#139)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ALL_PLUGGED_OUTPUTS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LAST_PLUGGED_OUTPUT</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### StreamError {:#StreamError}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#47)*

 StreamError

 This error code encapsulates various errors that might emanate from a
 StreamProcessor server. It can be sent either as an OnStreamFailed event or
 as an epitaph for the channel.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>INVALID_INPUT_FORMAT_DETAILS</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>INCOMPATIBLE_BUFFERS_PROVIDED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>DECODER_UNKNOWN</code></td>
            <td><code>16777217</code></td>
            <td></td>
        </tr><tr>
            <td><code>ENCODER_UNKNOWN</code></td>
            <td><code>33554433</code></td>
            <td></td>
        </tr><tr>
            <td><code>DECRYPTOR_UNKNOWN</code></td>
            <td><code>50331649</code></td>
            <td></td>
        </tr><tr>
            <td><code>DECRYPTOR_NO_KEY</code></td>
            <td><code>50331650</code></td>
            <td></td>
        </tr></table>

### AudioBitrateMode {:#AudioBitrateMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#79)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSPECIFIED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CBR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>VBR</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### AudioPcmMode {:#AudioPcmMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#99)*

 AudioPcmMode



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>LINEAR</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALAW</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>MULAW</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### AudioChannelId {:#AudioChannelId}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#123)*

 AudioChannelId

 Used in specifying which audio channel is for which speaker location / type.

 TODO(dustingreen): Do we need more channel IDs than this?



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SKIP</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>LF</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>RF</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CF</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>LS</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>RS</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>LFE</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>CS</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr><tr>
            <td><code>LR</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>RR</code></td>
            <td><code>9</code></td>
            <td></td>
        </tr><tr>
            <td><code>END_DEFINED</code></td>
            <td><code>10</code></td>
            <td></td>
        </tr><tr>
            <td><code>EXTENDED_CHANNEL_ID_BASE</code></td>
            <td><code>1862270976</code></td>
            <td></td>
        </tr><tr>
            <td><code>MAX</code></td>
            <td><code>2147483647</code></td>
            <td></td>
        </tr></table>

### VideoColorSpace {:#VideoColorSpace}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#220)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>INVALID</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### SbcSubBands {:#SbcSubBands}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#441)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SUB_BANDS_4</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>SUB_BANDS_8</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr></table>

### SbcBlockCount {:#SbcBlockCount}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#446)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BLOCK_COUNT_4</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLOCK_COUNT_8</code></td>
            <td><code>8</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLOCK_COUNT_12</code></td>
            <td><code>12</code></td>
            <td></td>
        </tr><tr>
            <td><code>BLOCK_COUNT_16</code></td>
            <td><code>16</code></td>
            <td></td>
        </tr></table>

### SbcAllocation {:#SbcAllocation}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#453)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ALLOC_LOUDNESS</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ALLOC_SNR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### SbcChannelMode {:#SbcChannelMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#458)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>MONO</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DUAL</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>STEREO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>JOINT_STEREO</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### AacChannelMode {:#AacChannelMode}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#489)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>MONO</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>STEREO</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### AacVariableBitRate {:#AacVariableBitRate}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#503)*

 Variable bit rate modes. The actual resulting bitrate
 varies based on input signal and other encoding settings.

 See https://wiki.hydrogenaud.io/index.php?title=Fraunhofer_FDK_AAC#Bitrate_Modes


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>V1</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>V2</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>V3</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>V4</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>V5</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr></table>

### AacAudioObjectType {:#AacAudioObjectType}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#516)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>MPEG2_AAC_LC</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr></table>

### AudioSampleFormat {:#AudioSampleFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#74)*

 Enumerates the supported audio sample formats.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSIGNED_8</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>SIGNED_16</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>SIGNED_24_IN_32</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>FLOAT</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### ColorSpace {:#ColorSpace}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#116)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>NOT_APPLICABLE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>JPEG</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>HD_REC709</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>SD_REC601</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### EncryptedFormat {:#EncryptedFormat}


*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#369)*

 EncryptedFormat

 The stream format details payload of a decrypting stream processor. This is
 a sparsely populated table to specify parameters necessary for decryption
 other than the data stream. It is only necessary to update fields if they
 changed, but not an error if the same value is repeated.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>mode</code></td>
            <td>
                <code>string</code>
            </td>
            <td> `mode` specifies which encryption scheme to use, such as
 `fuchsia.media.ENCRYPTION_MODE_CENC`.
 Usage:
  - It is required to be set prior to delivery of input packets.
  - This should only be changed at the beginning of a data stream.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>key_id</code></td>
            <td>
                <code><a class='link' href='#KeyId'>KeyId</a></code>
            </td>
            <td> `key_id` identifies the key that should be used for decrypting
 subsequent data.
 Usage:
  - It is required to be set prior to delivery of input packets to a
    decryptor.
  - This may be changed multiple times during a data stream.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>init_vector</code></td>
            <td>
                <code>vector&lt;uint8&gt;[16]</code>
            </td>
            <td> `init_vector` is used in combination with a key and a block of content
 to create the first cipher block in a chain and derive subsequent cipher
 blocks in a cipher block chain.
 Usage:
  - It is required to be set prior to the delivery of input packets to a
    decryptor.
  - This may be changed multiple times during a data stream.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>subsamples</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SubsampleEntry'>SubsampleEntry</a>&gt;</code>
            </td>
            <td> `subsamples` is used to identify the clear and encrypted portions of a
 subsample.
 Usage:
  - For whole sample encryption, this parameter should not be sent.
  - This may be changed multiple times during a data stream.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>pattern</code></td>
            <td>
                <code><a class='link' href='#EncryptionPattern'>EncryptionPattern</a></code>
            </td>
            <td> `pattern` is used to identify the clear and encrypted blocks for pattern
 based encryption.
 Usage:
 - This is not allowed for CENC and CBC1 and required for CENS and CBCS.
 - If required, it must be set prior to the delivery of input packets to
   a decryptor.
 - This may be changed multiple times during a data stream.
</td>
        </tr></table>

### DecryptedFormat {:#DecryptedFormat}


*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#416)*

 DecryptedFormat

 This describes the format of the decrypted content. It is required to be
 sent by the StreamProcessor server prior to the delivery of output packets.
 Currently, there is no additional format details for decrypted output.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>ignore_this_field</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### FormatDetails {:#FormatDetails}


*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#560)*

 FormatDetails

 This describes/details the format on input or output of a StreamProcessor
 (separate instances for input vs. output).


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>format_details_version_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>mime_type</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>oob_bytes</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>domain</code></td>
            <td>
                <code><a class='link' href='#DomainFormat'>DomainFormat</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>pass_through_parameters</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#Parameter'>Parameter</a>&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>encoder_settings</code></td>
            <td>
                <code><a class='link' href='#EncoderSettings'>EncoderSettings</a></code>
            </td>
            <td> Instructs an encoder on how to encode raw data.

 Decoders may ignore this field but are entitled to rejected requests with
 this field set because it doesn't make sense.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>timebase</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The number of ticks of the timebase of input packet timestamp_ish values
 per second.

 The timebase is only used used for optional extrapolation of timestamp_ish
 values when an input timestamp which applies to byte 0 of the valid portion
 of the input packet does not correspond directly to byte 0 of the valid
 portion of any output packet.

 Leave unset if timestamp extrapolation is not needed, either due to lack of
 timestamps on input, or due to input being provided in increments of the
 encoder's input chunk size (based on the encoder settings and calculated
 independently by the client).  Set if timestamp extrapolation is known to be
 needed or known to be acceptable to the client.
</td>
        </tr></table>

### StreamBufferConstraints {:#StreamBufferConstraints}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#73)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_constraints_version_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>default_settings</code></td>
            <td>
                <code><a class='link' href='#StreamBufferSettings'>StreamBufferSettings</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>per_packet_buffer_bytes_min</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>per_packet_buffer_bytes_recommended</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>per_packet_buffer_bytes_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>packet_count_for_server_min</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>packet_count_for_server_recommended</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>packet_count_for_server_recommended_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>9</td>
            <td><code>packet_count_for_server_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>10</td>
            <td><code>packet_count_for_client_min</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>11</td>
            <td><code>packet_count_for_client_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>12</td>
            <td><code>single_buffer_mode_allowed</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>13</td>
            <td><code>is_physically_contiguous_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>14</td>
            <td><code>very_temp_kludge_bti_handle</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td></td>
        </tr></table>

### StreamOutputConstraints {:#StreamOutputConstraints}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#282)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_constraints_action_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>buffer_constraints</code></td>
            <td>
                <code><a class='link' href='#StreamBufferConstraints'>StreamBufferConstraints</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamOutputFormat {:#StreamOutputFormat}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#334)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>format_details</code></td>
            <td>
                <code><a class='link' href='#FormatDetails'>FormatDetails</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamOutputConfig {:#StreamOutputConfig}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#413)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_constraints_action_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>buffer_constraints</code></td>
            <td>
                <code><a class='link' href='#StreamBufferConstraints'>StreamBufferConstraints</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>format_details</code></td>
            <td>
                <code><a class='link' href='#FormatDetails'>FormatDetails</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamBufferSettings {:#StreamBufferSettings}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#469)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_constraints_version_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>packet_count_for_server</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>packet_count_for_client</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>per_packet_buffer_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>single_buffer_mode</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>

### StreamBufferPartialSettings {:#StreamBufferPartialSettings}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#599)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_constraints_version_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>single_buffer_mode</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>packet_count_for_server</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> When single_buffer_mode is false:

 The actual packet count will be
 max(packet_count_for_server + packet_count_for_client, sysmem_buffers).
 The sysmem_buffers is BufferCollectionInfo.buffer_count from sysmem if
 using sysmem, or 0 if not using sysmem.

 When single_buffer_mode is true:

 The actual packet count is packet_count_for_server +
 packet_count_for_client.

 If not using sysmem, or if using single_buffer_mode, these fields must be
 set and consistent with correpsonding fields in StreamBufferConstraints.

 If single_buffer_mode false and using sysmem, these fields can both be
 non-set, or can both be set and consistent with correpsonding fields in
 StreamBufferConstraints.  If not set, the value used for the fields in
 the "max" expression above is 0, so buffer_count.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>packet_count_for_client</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>sysmem_token</code></td>
            <td>
                <code><a class='link' href='../fuchsia.sysmem/index.html'>fuchsia.sysmem</a>/<a class='link' href='../fuchsia.sysmem/index.html#BufferCollectionToken'>BufferCollectionToken</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamBuffer {:#StreamBuffer}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#703)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#StreamBufferData'>StreamBufferData</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamBufferDataVmo {:#StreamBufferDataVmo}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#755)*

 StreamBufferDataVmo

 Details for a buffer backed by a VMO.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>vmo_handle</code></td>
            <td>
                <code>handle&lt;vmo&gt;</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>vmo_usable_start</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>vmo_usable_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr></table>

### PacketHeader {:#PacketHeader}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#779)*

 PacketHeader

 When referring to a free packet, we use PacketHeader alone instead of
 Packet, since while a packet is free it doesn't really have meaningful
 offset or length etc.

 A populated Packet also has a PacketHeader.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>packet_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### Packet {:#Packet}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#837)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>header</code></td>
            <td>
                <code><a class='link' href='#PacketHeader'>PacketHeader</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Which buffer this packet refers to.  For single-buffer mode this will
 always be 0, but for multi-buffer mode, a given in-flight interval of a
 packet can refer to any buffer.  The packet has an associated buffer only
 while the packet is in-flight, not while the packet is free.

 The default value makes accidental inappropriate use of index 0 less
 likely (will tend to complain in an obvious way if not filled out
 instead of a non-obvious data corruption when decoding buffer 0
 repeatedly instead of the correct buffers).

 TODO(dustingreen): Try to make FIDL table defaults have meaning, and not
 complain about !has when accessing the field.  For now the default
 specified here does nothing.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>start_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>valid_length_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>timestamp_ish</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>start_access_unit</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>8</td>
            <td><code>known_end_access_unit</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr></table>



## **UNIONS**

### Usage {:#Usage}
*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#132)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>render_usage</code></td>
            <td>
                <code><a class='link' href='#AudioRenderUsage'>AudioRenderUsage</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>capture_usage</code></td>
            <td>
                <code><a class='link' href='#AudioCaptureUsage'>AudioCaptureUsage</a></code>
            </td>
            <td></td>
        </tr></table>

### Value {:#Value}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#15)*

 Value

 Generic "value" for use within generic "Parameter" struct.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>bool_value</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uint64_value</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>int64_value</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>string_value</code></td>
            <td>
                <code>string</code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>bytes_value</code></td>
            <td>
                <code>vector&lt;uint8&gt;</code>
            </td>
            <td></td>
        </tr></table>

### AudioUncompressedFormat {:#AudioUncompressedFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#192)*

 AudioUncompressedFormat


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>pcm</code></td>
            <td>
                <code><a class='link' href='#PcmFormat'>PcmFormat</a></code>
            </td>
            <td></td>
        </tr></table>

### AudioFormat {:#AudioFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#199)*

 AudioFormat


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>compressed</code></td>
            <td>
                <code><a class='link' href='#AudioCompressedFormat'>AudioCompressedFormat</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uncompressed</code></td>
            <td>
                <code><a class='link' href='#AudioUncompressedFormat'>AudioUncompressedFormat</a></code>
            </td>
            <td></td>
        </tr></table>

### VideoCompressedFormat {:#VideoCompressedFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#211)*

 VideoCompressedFormat

 Compressed video format details.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>temp_field_todo_remove</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
        </tr></table>

### VideoFormat {:#VideoFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#330)*

 VideoFormat

 Video (compress or uncompressed) format details.  In this context,
 "uncompressed" can include block-based image compression formats that still
 permit fairly fast random access to image data.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>compressed</code></td>
            <td>
                <code><a class='link' href='#VideoCompressedFormat'>VideoCompressedFormat</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>uncompressed</code></td>
            <td>
                <code><a class='link' href='#VideoUncompressedFormat'>VideoUncompressedFormat</a></code>
            </td>
            <td></td>
        </tr></table>

### DomainFormat {:#DomainFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#433)*

 DomainFormat


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>audio</code></td>
            <td>
                <code><a class='link' href='#AudioFormat'>AudioFormat</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>video</code></td>
            <td>
                <code><a class='link' href='#VideoFormat'>VideoFormat</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>crypto</code></td>
            <td>
                <code><a class='link' href='#CryptoFormat'>CryptoFormat</a></code>
            </td>
            <td></td>
        </tr></table>

### AacBitRate {:#AacBitRate}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#511)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>constant</code></td>
            <td>
                <code><a class='link' href='#AacConstantBitRate'>AacConstantBitRate</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>variable</code></td>
            <td>
                <code><a class='link' href='#AacVariableBitRate'>AacVariableBitRate</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamBufferData {:#StreamBufferData}
*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#746)*

 StreamBufferData

 For the moment, a VMO per buffer is the only type of buffer.

 This is extremely likely to change significantly when adding gralloc stuff,
 but the idea with this union is to have a struct per logical way of storing
 the data.  Any multi-domain storage within a gralloc buffer will likely be
 only indirectly represented here.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>vmo</code></td>
            <td>
                <code><a class='link' href='#StreamBufferDataVmo'>StreamBufferDataVmo</a></code>
            </td>
            <td></td>
        </tr></table>

### MediumSpecificStreamType {:#MediumSpecificStreamType}
*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#31)*

 A union of all medium-specific stream type structs.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>audio</code></td>
            <td>
                <code><a class='link' href='#AudioStreamType'>AudioStreamType</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>video</code></td>
            <td>
                <code><a class='link' href='#VideoStreamType'>VideoStreamType</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>text</code></td>
            <td>
                <code><a class='link' href='#TextStreamType'>TextStreamType</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>subpicture</code></td>
            <td>
                <code><a class='link' href='#SubpictureStreamType'>SubpictureStreamType</a></code>
            </td>
            <td></td>
        </tr></table>



## **XUNIONS**

### AudioCompressedFormat {:#AudioCompressedFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#74)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>aac</code></td>
            <td>
                <code><a class='link' href='#AudioCompressedFormatAac'>AudioCompressedFormatAac</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>sbc</code></td>
            <td>
                <code><a class='link' href='#AudioCompressedFormatSbc'>AudioCompressedFormatSbc</a></code>
            </td>
            <td></td>
        </tr></table>

### CryptoFormat {:#CryptoFormat}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#425)*

 CryptoFormat

 Crypto (encrypted or decrypted) format details.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>encrypted</code></td>
            <td>
                <code><a class='link' href='#EncryptedFormat'>EncryptedFormat</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>decrypted</code></td>
            <td>
                <code><a class='link' href='#DecryptedFormat'>DecryptedFormat</a></code>
            </td>
            <td></td>
        </tr></table>

### AacTransport {:#AacTransport}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#485)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>raw</code></td>
            <td>
                <code><a class='link' href='#AacTransportRaw'>AacTransportRaw</a></code>
            </td>
            <td></td>
        </tr></table>

### EncoderSettings {:#EncoderSettings}
*Defined in [fuchsia.media/stream_common.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#530)*

 Settings for encoders that tell them how to encode raw
 formats.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>sbc</code></td>
            <td>
                <code><a class='link' href='#SbcEncoderSettings'>SbcEncoderSettings</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>aac</code></td>
            <td>
                <code><a class='link' href='#AacEncoderSettings'>AacEncoderSettings</a></code>
            </td>
            <td></td>
        </tr></table>





## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio.fidl#32">MIN_PCM_CHANNEL_COUNT</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Permitted ranges for AudioRenderer and AudioCapturer
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio.fidl#33">MAX_PCM_CHANNEL_COUNT</a></td>
            <td>
                    <code>8</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio.fidl#34">MIN_PCM_FRAMES_PER_SECOND</a></td>
            <td>
                    <code>1000</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio.fidl#35">MAX_PCM_FRAMES_PER_SECOND</a></td>
            <td>
                    <code>192000</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#103">RENDER_USAGE_COUNT</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#130">CAPTURE_USAGE_COUNT</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#7">AudioGainInfoFlag_Mute</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#8">AudioGainInfoFlag_AgcSupported</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#9">AudioGainInfoFlag_AgcEnabled</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#29">SetAudioGainFlag_GainValid</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#30">SetAudioGainFlag_MuteValid</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_device_enumerator.fidl#31">SetAudioGainFlag_AgcValid</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#17">METADATA_LABEL_TITLE</a></td>
            <td><code>fuchsia.media.title</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#18">METADATA_LABEL_ARTIST</a></td>
            <td><code>fuchsia.media.artist</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#19">METADATA_LABEL_ALBUM</a></td>
            <td><code>fuchsia.media.album</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#20">METADATA_LABEL_PUBLISHER</a></td>
            <td><code>fuchsia.media.publisher</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#21">METADATA_LABEL_GENRE</a></td>
            <td><code>fuchsia.media.genre</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#22">METADATA_LABEL_COMPOSER</a></td>
            <td><code>fuchsia.media.composer</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#26">METADATA_SOURCE_TITLE</a></td>
            <td><code>fuchsia.media.source_title</code></td>
                    <td><code>String</code></td>
            <td> The title of the source of the media, e.g. a player, streaming service, or
 website.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#154">NO_TIMESTAMP</a></td>
            <td>
                    <code>9223372036854775807</code>
                </td>
                <td><code>int64</code></td>
            <td> When used as a `StreamPacket.pts` value, indicates that the packet has no
 specific presentation timestamp. The effective presentation time of such a
 packet depends on the context in which the `StreamPacket` is used.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#159">STREAM_PACKET_FLAG_KEY_FRAME</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates that the packet can be understood without reference to other
 packets in the stream. This is typically used in compressed streams to
 identify packets that contain key frames.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#165">STREAM_PACKET_FLAG_DROPPABLE</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates that all other packets in the stream can be understood without
 reference to this packet. This is typically used in compressed streams to
 identify packets containing frames that may be discarded without affecting
 other frames.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream.fidl#170">STREAM_PACKET_FLAG_DISCONTINUITY</a></td>
            <td>
                    <code>4</code>
                </td>
                <td><code>uint32</code></td>
            <td> Indicates a discontinuity in an otherwise continuous-in-time sequence of
 packets. The precise semantics of this flag depend on the context in which
 the `StreamPacket` is used.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#9">KEY_ID_SIZE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#10">MAX_INIT_VECTOR_SIZE</a></td>
            <td>
                    <code>16</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_common.fidl#439">kMaxOobBytesSize</a></td>
            <td>
                    <code>8192</code>
                </td>
                <td><code>uint64</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#449">kDefaultInputPacketCountForClient</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#451">kDefaultOutputPacketCountForClient</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#458">kDefaultInputIsSingleBufferMode</a></td>
            <td>
                    <code>false</code>
                </td>
                <td><code>bool</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#459">kDefaultOutputIsSingleBufferMode</a></td>
            <td>
                    <code>false</code>
                </td>
                <td><code>bool</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#39">AUDIO_ENCODING_AAC</a></td>
            <td><code>fuchsia.media.aac</code></td>
                    <td><code>String</code></td>
            <td> Audio encodings.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#40">AUDIO_ENCODING_AMRNB</a></td>
            <td><code>fuchsia.media.amrnb</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#41">AUDIO_ENCODING_AMRWB</a></td>
            <td><code>fuchsia.media.amrwb</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#42">AUDIO_ENCODING_APTX</a></td>
            <td><code>fuchsia.media.aptx</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#43">AUDIO_ENCODING_FLAC</a></td>
            <td><code>fuchsia.media.flac</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#44">AUDIO_ENCODING_GSMMS</a></td>
            <td><code>fuchsia.media.gsmms</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#45">AUDIO_ENCODING_LPCM</a></td>
            <td><code>fuchsia.media.lpcm</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#46">AUDIO_ENCODING_MP3</a></td>
            <td><code>fuchsia.media.mp3</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#47">AUDIO_ENCODING_PCMALAW</a></td>
            <td><code>fuchsia.media.pcmalaw</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#48">AUDIO_ENCODING_PCMMULAW</a></td>
            <td><code>fuchsia.media.pcmmulaw</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#49">AUDIO_ENCODING_SBC</a></td>
            <td><code>fuchsia.media.sbc</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#50">AUDIO_ENCODING_VORBIS</a></td>
            <td><code>fuchsia.media.vorbis</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#53">VIDEO_ENCODING_H263</a></td>
            <td><code>fuchsia.media.h263</code></td>
                    <td><code>String</code></td>
            <td> Video encodings.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#54">VIDEO_ENCODING_H264</a></td>
            <td><code>fuchsia.media.h264</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#55">VIDEO_ENCODING_MPEG4</a></td>
            <td><code>fuchsia.media.mpeg4</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#56">VIDEO_ENCODING_THEORA</a></td>
            <td><code>fuchsia.media.theora</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#57">VIDEO_ENCODING_UNCOMPRESSED</a></td>
            <td><code>fuchsia.media.uncompressed_video</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#58">VIDEO_ENCODING_VP3</a></td>
            <td><code>fuchsia.media.vp3</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#59">VIDEO_ENCODING_VP8</a></td>
            <td><code>fuchsia.media.vp8</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#60">VIDEO_ENCODING_VP9</a></td>
            <td><code>fuchsia.media.vp9</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    
</table>

