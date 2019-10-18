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
*Defined in [fuchsia.media/audio_capturer.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_capturer.fidl#256)*

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
*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#82)*


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



### BindUsageVolumeControl {:#BindUsageVolumeControl}

 Binds to a volume control protocol for the given usage.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#Usage'>Usage</a></code>
            </td>
        </tr><tr>
            <td><code>volume_control</code></td>
            <td>
                <code>request&lt;<a class='link' href='../fuchsia.media.audio/index.html'>fuchsia.media.audio</a>/<a class='link' href='../fuchsia.media.audio/index.html#VolumeControl'>VolumeControl</a>&gt;</code>
            </td>
        </tr></table>



### SetInteraction {:#SetInteraction}

 SetInteraction allows changing how audio_core handles interactions of multiple active
 streams simultaneously.  If streams of Usage `active` are processing audio, and streams of
 Usage `affected` are as well, the Behavior specified will be applied to the streams of Usage
 `affected`.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>active</code></td>
            <td>
                <code><a class='link' href='#Usage'>Usage</a></code>
            </td>
        </tr><tr>
            <td><code>affected</code></td>
            <td>
                <code><a class='link' href='#Usage'>Usage</a></code>
            </td>
        </tr><tr>
            <td><code>behavior</code></td>
            <td>
                <code><a class='link' href='#Behavior'>Behavior</a></code>
            </td>
        </tr></table>



### ResetInteractions {:#ResetInteractions}

 Re-initializes the set of rules that are currently governing the interaction of streams in
 audio_core.  The default behavior is 'NONE'.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### LoadDefaults {:#LoadDefaults}

 Re-loads the platform policy configuration.  Falls back to a default config if the platform
 does not provide a config.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



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
*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#931)*

 Overview of operation:

 1. Create
   * create via CodecFactory - see CodecFactory
   * create via LicenseSession - see LicenseSession
 2. Get input constraints
   * OnInputConstraints() - sent unsolicited by stream processor shortly after
     stream processor creation.
 3. Provide input buffers
   * SetInputBufferPartialSettings() (current way)
   * SetInputBufferSettings() / AddInputBuffer() (old deprecated way)
 4. Deliver input data
   * QueueInputPacket() + OnFreeInputPacket(), for as long as it takes,
     possibly working through all input packets repeatedly before...
 5. Get output constraints and format
   * OnOutputConstraints()
   * This is not sent until after at least one QueueInput* message is sent by
     the client, even if the underlying processor behind the StreamProcessor
     doesn't fundamentally need any input data to determine its output
     constraints.  This server behavior prevents clients taking an incorrect
     dependency on the output constraints showing up before input is
     delivered.
   * A client must tolerate this arriving as late as after substantial input
     data has been delivered, including lots of input packet recycling via
     OnFreeInputPacket().
   * This message can arrive more than once before the first output data.
 6. Provide output buffers
   * SetOutputBufferPartialSettings() / CompleteOutputBufferPartialSettings()
     (current way)
   * SetOutputBufferSettings() / AddOutputBuffer()
     (old deprecated way)
 7. Data flows, with optional EndOfStream
   * OnOutputPacket() / RecycleOutputPacket() / QueueInputPacket() /
     OnFreeInputPacket() / QueueInputEndOfStream() / OnOutputEndOfStream()

 Semi-trusted StreamProcessor server - SW decoders run in an isolate (with
 very few capabilities) just in case the decoding SW has a vulnerability
 which could be used to take over the StreamProcessor server.  Clients of the
 stream processor interface using decoders and processing streams of separate
 security contexts, to a greater extent than some other interfaces, need to
 protect themselves against invalid server behavior, such as double-free of a
 packet_index and any other invalid server behavior.  Having fed in
 compressed data of one security context, don't place too much trust in a
 single StreamProcessor instance to not mix data among any buffers that
 StreamProcessor server has ever been told about.  Instead, create separate
 StreamProcessor instances for use by security-separate client-side contexts.
 While the picture for HW-based decoders looks somewhat different and is out
 of scope of this paragraph, the client should always use separate
 StreamProcessor instances for security-separate client-side contexts.

 Descriptions of actions taken by methods of this protocol and the states of
 things are given as if the methods are synchronously executed by the stream
 processor server, but in reality, as is typical of FIDL interfaces, the
 message processing is async.  The states described are to be read as the
 state from the client's point of view unless otherwise stated.  Events
 coming back from the server are of course delivered async, and a client that
 processes more than one stream per StreamProcessor instance needs to care
 whether a given event is from the current stream vs. some older
 soon-to-be-gone stream.

 The Sync() method's main purpose is to enable the client to robustly prevent
 having both old and new buffers allocated in the system at the same time,
 since media buffers can be significantly large, depending. The Sync() method
 achieves this by only delivering it's response when all previous calls to
 the StreamProcessor protocol have actually taken effect in the
 StreamControl ordering domain. Sync() can also be used to wait for the
 stream processor server to catch up if there's a possibility that a client
 might otherwise get too far ahead of the StreamProcessor server, by for
 example requesting creation of a large number of streams in a row.  It can
 also be used during debugging to ensure that a stream processor server
 hasn't gotten stuck.  Calling Sync() is entirely optional and never required
 for correctness - only potentially required to de-overlap resource usage.

 It's possible to re-use a StreamProcessor instance for another stream, and
 doing so can sometimes skip over re-allocation of buffers. This can be a
 useful thing to do for cases like seeking to a new location - at the
 StreamProcessor interface that can look like switching to a new stream.

### EnableOnStreamFailed {:#EnableOnStreamFailed}

 Permit the server to use OnStreamFailed() instead of the server just
 closing the whole StreamProcessor channel on stream failure.

 If the server hasn't seen this message by the time a stream fails, the
 server will close the StreamProcessor channel instead of sending
 OnStreamFailed().

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### OnStreamFailed {:#OnStreamFailed}

 The stream has failed, but the StreamProcessor instance is still usable
 for a new stream.

 This message is only ever sent by the server if the client previously
 sent EnableOnStreamFailed().  If the client didn't send
 EnableOnStreamFailed() then the server closes the StreamProcessor
 channel instead.

 StreamProcessor server implementations are encouraged to handle stream
 errors (and ideally to also report them via error_ bools of
 OnOutputPacket() and OnOutputEndOfStream()) without failing the whole
 stream, but if a stream processor server is unable to do that, but still
 can cleanly contain the failure to the stream, the stream processor
 server can (assuming EnableOnStreamFailed() was called) use
 OnStreamFailed() to indicate the stream failure to the client without
 closing the StreamProcessor channel.

 An ideal StreamProcessor server handles problems with input data without
 sending this message, but sending this message is preferred vs. closing
 the server end of the StreamProcessor channel if the StreamProcessor
 server can 100% reliably contain the stream failure to the stream,
 without any adverse impact to any later stream.

 No further messages will arrive from the server regarding the failed
 stream.  This includes any OnOutputEndOfStream() that the client would
 have otherwise expected.



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

 The server sends this shortly after StreamProcessor creation to indicate
 input buffer constraints.  The "min" and "max" input constraints don't
 change for the life of the StreamProcessor.

 The "max" values for buffer size and count are large enough to support
 the most demanding format the server supports on input.  The
 "recommended" values should be workable for use with the input
 FormatDetails conveyed during StreamProcessor creation.  The
 "recommended" values are not necessarily suitable if the client uses
 QueueInputFormatDetails() to change the input format.  In that case it's
 up to the client to determine suitable values, either by creating a new
 StreamProcessor instance instead, or knowing suitable values outside the
 scope of this protocol.

 See comments on StreamBufferConstraints.

 This message is guaranteed to be sent unsolicited to the StreamProcessor
 client during or shortly after StreamProcessor creation.  Clients should
 not depend on this being the very first message to arrive at the client.

 The "min" and "max" input constraints are guaranteed not to change for a
 given StreamProcessor instance.  The "recommended" values may
 effectively change when the server processes QueueInputFormatDetails().
 There is not any way in the protocol short of creating a new
 StreamProcessor instance for the client to get those new "recommended"
 values.



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

 Clients should use SetInputBufferPartialSettings() instead.

 Configuring input buffers (the old way) consists of calling
 SetInputBufferSettings() followed by a number of calls to
 AddInputBuffer() equal to the number of buffers set via
 SetInputBufferSettings().  In buffer-per-packet mode, this is the same as
 the number of packets.  In single-buffer mode, this is 1.

 After OnInputConstraints(), the client uses these two methods to set up
 input buffers and packets.

 Configuring input buffers is required before QueueInputPacket().

 The client can also re-set-up input buffers any time there is no current
 stream.  The client need not wait until all previously-set-up input
 buffers are with the client via OnFreeInputPacket().  The old
 buffer_lifetime_ordinal just ends.

 The recommended way to de-overlap resource usage (when/if the client
 wants to) is to send CloseCurrentStream() with release_input_buffers
 true then send Sync() and wait for its response before allocating any
 new buffers. How to cause other parts of the system to release their
 references on low-level buffers is outside the scope of this interface.

 This call ends any previous buffer_lifetime_ordinal, and starts a new
 one.

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

 The client is required to add all the input buffers before sending any
 message that starts a new stream else the stream processor will close
 the StreamProcessor channel.

 When the last buffer is added with this message, all the input packets
 effectively jump from non-existent to free with the client.  The
 StreamProcessor will not generate an OnFreeInputPacket() for each new
 input packet.  The client can immediately start sending
 QueueInputPacket() after sending the last AddInputBuffer().

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

 This is the replacement for SetInputBufferSettings().

 When the client is using sysmem to allocate buffers, this message is
 used instead of SetInputBufferSettings()+AddInputBuffer().  Instead, a
 single SetInputBufferPartialSettings() provides the StreamProcessor with
 the client-specified input settings and a BufferCollectionToken which
 the StreamProcessor will use to convey constraints to sysmem.  Both the
 client and the StreamProcessor will be informed of the allocated buffers
 directly by sysmem via their BufferCollection channel (not via the
 StreamProcessor channel).

 The client must not QueueInput...() until after sysmem informs the client
 that buffer allocation has completed and was successful.

 The server should be prepared to see QueueInput...() before the server
 has necessarily heard from sysmem that the buffers are allocated - the
 server must tolerate either ordering, as the QueueInput...() and
 notification of sysmem allocation completion arrive on different
 channels, so the client having heard that allocation is complete doesn't
 mean the server knows that allocation is complete yet.  However, the
 server can expect that allocation is in fact complete and can expect to
 get the allocation information from sysmem immediately upon requesting
 the information from sysmem.

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

 This event informs the client of new output constraints.

 This message is ordered with respect to other output (such as output
 packets, output format, output end-of-stream).

 Before the first OnOutputPacket() of a stream, the server guarantees that
 at least one OnOutputConstraints() and exactly one OnOutputFormat() will
 be sent.  The server may not set buffer_constraints_action_required true
 in OnOutputConstraints() if the buffer config is already suitable for the
 stream (buffer_constraints_action_required false means the buffer config
 is already fine).  The client must tolerate multiple
 OnOutputConstraints() (and 1 OnOutputFormat() message) before the first
 output packet.  As long as the client hasn't moved to a new stream, the
 server won't send another OnOutputConstraints() until after the client
 has configured output buffers.

 This message can be sent mid-stream by a server.  If
 buffer_constraints_action_required false, the message is safe to
 ignore, but a client may choose to stash the new constraints for
 later use the next time the client wants to unilaterally re-configure
 buffers (when allowed).  If later the server needs the output config to
 change, the server may send a new OnOutputConstraints() with
 buffer_constraints_action_required true.

 On buffer_constraints_action_required true, a client that does not wish
 to fully handle mid-stream output buffer config changes should either
 give up completely on the processing, or at least re-config the output
 as specified before starting a new stream (and possibly re-delivering
 input data, if the client wants).  This avoids useless retry with a new
 stream starting from just before the output buffer config change which
 would hit the same mid-stream output config change again.

 Similarly, some servers may only partly support mid-stream format
 changes, or only support a mid-stream format change if the buffers are
 already large enough to handle both before and after the format change.
 Such servers should still indicate buffer_constraints_action_required
 true, but then send OnStreamFailed() after the client has re-configured
 output buffers (seamlessly dealing with the mid-stream output config
 change is even better of course, but is not always feasible depending on
 format).  When the client retries with a new stream starting from a
 nearby location in the client's logical overall media timeline, the
 output buffers will already be suitable for the larger size output, so
 the new stream will not need any mid-stream output buffer re-config,
 only a mid-stream OnOutputFormat().  This strategy avoids the problem
 that would otherwise occur if a client were to retry with a new stream
 starting just before the mid-stream output buffer config change (the
 retry wouldn't be effective since the same need for an output buffer
 config change would be hit again).  Servers are discouraged from sending
 OnStreamFailed() solely due to a mid-stream need for different output
 buffer config without first sending OnOutputConstraints() with
 buffer_constraints_action_required true and waiting for the client to
 re-configure output buffers (to avoid the useless client retry with a
 new stream from a logical location before the config change).

 When buffer_constraints_action_required true, the server will not send
 any OnOutputPacket() for this stream until after the client has
 configured/re-configured output buffers.

 A client that gives up on processing a stream on any mid-stream
 OnOutputConstraints() or mid-stream OnOutputFormat() should completely
 ignore any OnOutputConstraints() with buffer_constraints_action_required
 false.  Otherwise the client may needlessly fail processing, or server
 implementations might not be able to use
 buffer_constraints_action_required false for fear of simpler clients
 just disconnecting.

 All clients, even those which don't want to support any mid-stream
 output buffer re-config or mid-stream OnOutputFormat() are required to
 deal with 1..multiple OnOutputConstraints() messages before the first
 output packet, and 1 OnOutputFormat() messages before the first output
 packet.

 This message is ordered with respect to output packets, and with respect
 to OnOutputFormat().



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

 This message is sent by the server before the first output packet of any
 stream, and potentially mid-stream between output packets of the stream,
 ordered with respect to output packets, and ordered with respect to
 OnOutputConstraints().

 The server guarantees that the first packet of every stream will be
 preceeded by an OnOutputFormat().

 The server guarantees that there will be an OnOutputFormat() between an
 OnOutputConstraints() with buffer_constraints_action_required true and an
 OnOutputPacket().  In other words, the client is essentially allowed to
 forget what the output format is on any OnOutputConstraints() with
 buffer_constraints_action_required true, because the server promises a
 subsequent OnOutputFormat() before any OnOutputPacket().

 If the server sets buffer_constraints_action_required true in
 OnOutputConstraints(), the server won't send OnOutputFormat() (and
 therefore also won't send OnOutputPacket()) until the client has
 re-configured output buffers.

 The server is allowed to send an OnOutputFormat() mid-stream between two
 output packets.

 A server won't send two adjacent OnOutputFormat() messages without any
 output packet in between.  However an OnOutputFormat() message doesn't
 guarantee a subsequent packet, because for example the server could send
 OnOutputEndOfStream() or OnStreamFailed() instead.

 A client that does not wish to seamlessly handle mid-stream output format
 changes should either ensure that no stream processed by the client
 ever has any mid-stream format change, or the client should ensure that
 any retry of processing starts the new attempt at a point logically at or
 after the point where the old format has ended and the new format starts,
 else the client could just hit the same mid-stream format change again.

 An example of this message being sent mid-stream is mid-stream change
 of dimensions of video frames output from a video decoder.

 Not all servers will support seamless handling of format change.  Those
 that do support seamless handling of format change may require that the
 format change not also require output buffer re-config, in order for the
 handling to be seamless.  See the comment block for OnOutputConstraints()
 for more discussion of how servers and clients should behave - in
 particular when they don't seamlessly handle output constraint change
 and/or output format change.

 If this message isn't being sent by the server when expected at the
 start of a stream, the most common reason is that a OnOutputConstraints()
 with buffer_constraints_action_required true hasn't been processed by the
 client (by configuring output buffers using
 SetOutputBufferPartialSettings() etc).



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

 These are not permitted until after the first OnOutputConstraints().

 Roughly speaking, these messages are sent in response to
 OnOutputConstraints() with buffer_constraints_action_required true.

 Configuring output buffers consists of calling SetOutputBufferSettings()
 followed by a number of calls to AddOutputBuffer() equal to the number
 of buffers set via SetOutputBufferSettings().  In buffer-per-packet
 mode, this is the same as the number of packets.  In single-buffer mode,
 this is 1.

 Configuring output buffers is _required_ after OnOutputConstraints() is
 received by the client with buffer_constraints_action_required true and
 stream_lifetime_ordinal equal to the client's current
 stream_lifetime_ordinal (even if there is an active stream), and is
 _permitted_ any time there is no current stream.

 Closing the current stream occurs on the StreamControl ordering domain,
 so after a CloseCurrentStream() or FlushEndOfStreamAndCloseStream(), a
 subsequent Sync() completion must be received by the client before the
 client knows that there's no longer a current stream.

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

 This is the replacement for SetOutputBufferSettings().

 When the client is using sysmem to allocate buffers, this message is
 used instead of SetOutputBufferSettings()+AddOutputBuffer(). Instead, a
 single SetOutputBufferPartialSettings() provides the StreamProcessor
 with the client-specified output settings and a BufferCollectionToken
 which the StreamProcessor will use to convey constraints to sysmem.
 Both the client and the StreamProcessor will be informed of the
 allocated buffers directly by sysmem via their BufferCollection channel
 (not via the StreamProcessor channel).

 Configuring output buffers is _required_ after OnOutputConstraints() is
 received by the client with buffer_constraints_action_required true and
 stream_lifetime_ordinal equal to the client's current
 stream_lifetime_ordinal (even if there is an active stream), and is
 _permitted_ any time there is no current stream.

 Closing the current stream occurs on the StreamControl ordering domain,
 so after a CloseCurrentStream() or FlushEndOfStreamAndCloseStream(), a
 subsequent Sync() completion must be received by the client before the
 client knows that there's no longer a current stream.

 See also CompleteOutputBufferPartialSettings().

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

 After SetOutputBufferPartialSettings(), the server won't send
 OnOutputConstraints(), OnOutputFormat(), OnOutputPacket(), or
 OnOutputEndOfStream() until after the client sends
 CompleteOutputBufferPartialSettings().

 Some clients may be able to send
 CompleteOutputBufferPartialSettings() immediately after
 SetOutputBufferPartialSettings() - in that case the client needs to be
 prepared to receive output without knowing the buffer count or packet
 count yet - such clients may internally delay processing the received
 output until the client has heard from sysmem (which is when the client
 will learn the buffer count and packet count).

 Other clients may first wait for sysmem to allocate, prepare to receive
 output, and then send CompleteOutputBufferPartialSettings().

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

 This message is optional.

 This message is only valid after QueueInputEndOfStream() for this stream.
 The stream_lifetime_ordinal input parameter must match the
 stream_lifetime_ordinal of the QueueInputEndOfStream(), else the server
 will close the channel.

 A client can use this message to flush through (not discard) the last
 input data of a stream so that the stream processor server generates
 corresponding output data for all the input data before the server moves
 on to the next stream, without forcing the client to wait for
 OnOutputEndOfStream() before queueing data of another stream.

 The difference between QueueInputEndOfStream() and
 FlushEndOfStreamAndCloseStream():  QueueInputEndOfStream() is a promise
 from the client that there will not be any more input data for the
 stream (and this info is needed by some stream processors for the stream
 processor to ever emit the very last output data).  The
 QueueInputEndOfStream() having been sent doesn't prevent the client from
 later completely discarding the rest of the current stream by closing
 the current stream (with or without a stream switch).  In contrast,
 FlushEndOfStreamAndCloseStream() is a request from the client that all
 the previously-queued input data be processed including the logical
 "EndOfStream" showing up as OnOutputEndOfStream() (in success case)
 before moving on to any newer stream - this essentially changes the
 close-stream handling from discard to flush-through for this stream
 only.

 A client using this message can start providing input data for a new
 stream without that causing discard of old stream data.  That's the
 purpose of this message - to allow a client to flush through (not
 discard) the old stream's last data (instead of the default when closing
 or switching streams which is discard).

 Because the old stream is not done processing yet and the old stream's
 data is not being discarded, the client must be prepared to continue to
 process OnOutputConstraints() messages until the stream_lifetime_ordinal
 is done. The client will know the stream_lifetime_ordinal is done when
 OnOutputEndOfStream(), OnStreamFailed(), or the StreamProcessor channel
 closes.

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

 This "closes" the current stream, leaving no current stream.  In
 addition, this message can optionally release input buffers or output
 buffers.

 If there has never been any active stream, the stream_lifetime_ordinal
 must be zero or the server will close the channel.  If there has been an
 active stream, the stream_lifetime_ordinal must be the most recent
 active stream whether that stream is still active or not.  Else the
 server will close the channel.

 Multiple of this message without any new active stream in between is not
 to be considered an error, which allows a client to use this message to
 close the current stream to stop wasting processing power on a stream the
 user no longer cares about, then later decide that buffers should be
 released and send this message again with release_input_buffers and/or
 release_output_buffers true to get the buffers released, if the client is
 interested in trying to avoid overlap in resource usage between old
 buffers and new buffers (not all clients are).

 See also Sync().

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

 On completion, all previous StreamProcessor calls have done what they're
 going to do server-side, _except_ for processing of data queued using
 QueueInputPacket().

 The main purpose of this call is to enable the client to wait until
 CloseCurrentStream() with release_input_buffers and/or
 release_output_buffers set to true to take effect, before the client
 allocates new buffers and re-sets-up input and/or output buffers.  This
 de-overlapping of resource usage can be worthwhile for media buffers
 which can consume resource types whose overall pools aren't necessarily
 vast in comparison to resources consumed.  Especially if a client is
 reconfiguring buffers multiple times.

 Note that Sync() prior to allocating new media buffers is not alone
 sufficient to achieve non-overlap of media buffer resource usage system
 wide, but it can be a useful part of achieving that.

 The Sync() transits the Output ordering domain and the StreamControl
 ordering domain, but not the InputData ordering domain.

 This request can be used to avoid hitting kMaxInFlightStreams which is
 presently 10.  A client that stays <= 8 in-flight streams will
 comfortably stay under the limit of 10.  While the protocol permits
 repeated SetInputBufferSettings() and the like, a client that spams the
 channel can expect that the channel will just close if the server or the
 channel itself gets too far behind.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### OnOutputPacket {:#OnOutputPacket}

 This is how the stream processor emits an output packet to the stream
 processor client.

 Order is significant.

 The client should eventually call RecycleOutputPacket() (possibly after
 switching streams multiple times), unless the buffer_lifetime_ordinal
 has moved on.  A stream change doesn't change which packets are busy
 with the client vs. free with the server.

 The relevant buffer is always the one specified in the packet's buffer_index field.

 For low-level buffer types that support it, a StreamProcessor is free to
 emit an output packet before the low-level buffer actually has any
 usable data in the buffer, with the mechanism for signalling the
 presence of data separate from the OnOutputPacket() message.  For such
 low-level buffer types, downstream consumers of data from the emitted
 packet must participate in the low-level buffer signalling mechanism to
 know when it's safe to consume the data.  This is most likely to be
 relevant when using a video decoder and gralloc-style buffers.

 The error_ bool(s) allow (but do not require) a StreamProcessor server
 to report errors that happen during an AU or between AUs.

 The scope of error_detected_before starts at the end of the last
 delivered output packet on this stream, or the start of stream if there
 were no previous output packets on this stream.  The scope ends at the
 start of the output_packet.

 The error_detected_before bool is separate so that discontinuities can be
 indicated separately from whether the current packet is damaged.

 The scope of error_detected_during is from the start to the end of this
 output_packet.



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

 After the client is done with an output packet, the client needs to tell
 the stream processor that the output packet can be re-used for more
 output, via this method.

 It's not permitted to recycle an output packet that's already free with
 the stream processor server.  It's permitted but discouraged for a
 client to recycle an output packet that has been deallocated by an
 explicit or implicit output buffer de-configuration().  See
 buffer_lifetime_ordinal for more on that. A server must ignore any such
 stale RecycleOutputPacket() calls.

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

 After QueueInputEndOfStream() is sent by the StreamProcessor client,
 within a reasonable duration the corresponding OnOutputEndOfStream()
 will be sent by the StreamProcessor server.  Similar to
 QueueInputEndOfStream(), OnOutputEndOfStream() is sent a maximum of once
 per stream.

 No more stream data for this stream will be sent after this message.  All
 input data for this stream was processed.

 While a StreamProcessor client is not required to
 QueueInputEndOfStream() (unless the client wants to use
 FlushEndOfStreamAndCloseStream()), if a StreamProcessor server receives
 QueueInputEndOfStream(), and the client hasn't closed the stream, the
 StreamProcessor server must generate a corresponding
 OnOutputEndOfStream() if nothing went wrong, or must send
 OnStreamFailed(), or must close the server end of the StreamProcessor
 channel.  An ideal StreamProcessor server would handle and report stream
 errors via the error_ flags and complete stream processing without
 sending OnStreamFailed(), but in any case, the above-listed options are
 the only ways that an OnOutputEndOfStream() won't happen after
 QueueInputEndOfStream().

 There will be no more OnOutputPacket() or OnOutputConstraints() messages
 for this stream_lifetime_ordinal after this message - if a server doesn't
 follow this rule, a client should close the StreamProcessor channel.

 The error_detected_before bool has the same semantics as the
 error_detected_before bool in OnOutputPacket().



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

 If the input format details are still the same as specified during
 StreamProcessor creation, this message is unnecessary and does not need
 to be sent.

 If the stream doesn't exist yet, this message creates the stream.

 The server won't send OnOutputConstraints() until after the client has
 sent at least one QueueInput* message.

 All servers must permit QueueInputFormatDetails() at the start of a
 stream without failing, as long as the new format is supported by the
 StreamProcessor instance.  Technically this allows for a server to only
 support the exact input format set during StreamProcessor creation, and
 that is by design.  A client that tries to switch formats and gets a
 StreamProcessor channel failure should try again one more time with a
 fresh StreamProcessor instance created with CodecFactory using the new
 input format during creation, before giving up.

 These format details override the format details specified during stream
 processor creation for this stream only.  The next stream will default
 back to the format details set during stream processor creation.

 This message is permitted at the start of the first stream (just like at
 the start of any stream).  The format specified need not match what was
 specified during stream processor creation, but if it doesn't match, the
 StreamProcessor channel might close as described above.

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

 This message queues input data to the stream processor for processing.

 If the stream doesn't exist yet, this message creates the new stream.

 The server won't send OnOutputConstraints() until after the client has
 sent at least one QueueInput* message.

 The client must continue to deliver input data via this message even if
 the stream processor has not yet generated the first OnOutputConstraints(),
 and even if the StreamProcessor is generating OnFreeInputPacket() for
 previously-queued input packets.  The input data must continue as long
 as there are free packets to be assured that the server will ever
 generate the first OnOutputConstraints().

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

 The server sends this message when the stream processor is done
 consuming this packet and the packet can be re-filled by the client.

 This is not sent for all packets when a new buffer_lifetime_ordinal
 starts as in that case all the packets are initially free with the
 client.

 After receiving the available input buffer via this event, the stream
 processor client can call later call QueueInputBuffer with appropriate
 offset and length set.



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

 Inform the server that all QueueInputPacket() messages for this stream
 have been sent.

 If the stream isn't closed first (by the client, or by OnStreamFailed(),
 or StreamProcessor channel closing), there will later be a corresponding
 OnOutputEndOfStream().

 The corresponding OnOutputEndOfStream() message will be generated only if
 the server finishes processing the stream before the server sees the
 client close the stream (such as by starting a new stream).  A way to
 force the server to finish the stream before closing is to use
 FlushEndOfStreamAndCloseStream() after QueueInputEndOfStream() before any
 new stream.  Another way to force the server to finish the stream before
 closing is to wait for the OnOutputEndOfStream() before taking any action
 that closes the stream.

 In addition to serving as an "EndOfStream" marker to make it obvious
 client-side when all input data has been processed, if a client never
 sends QueueInputEndOfStream(), no amount of waiting will necessarily
 result in all input data getting processed through to the output.  Some
 stream processors have some internally-delayed data which only gets
 pushed through by additional input data _or_ by this EndOfStream marker.
 In that sense, this message can be viewed as a flush-through at
 InputData domain level, but the flush-through only takes effect if the
 stream processor even gets that far before the stream is just closed at
 StreamControl domain level.  This message is not alone sufficient to act
 as an overall flush-through at StreamControl level. For that, send this
 message first and then send FlushEndOfStreamAndCloseStream() (at which
 point it becomes possible to queue input data for a new stream without
 causing discard of this older stream's data), or wait for the
 OnOutputEndOfStream() before closing the current stream.

 If a client sends QueueInputPacket(), QueueInputFormatDetails(),
 QueueInputEndOfStream() for this stream after the first
 QueueInputEndOfStream() for this stream, a server should close the
 StreamProcessor channel.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
        </tr></table>



## UsageWatcher {:#UsageWatcher}
*Defined in [fuchsia.media/usage_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/usage_reporter.fidl#34)*

 A protocol for listening to changes to the policy state of an audio usage.

 User actions, such as lowering the volume or muting a stream, are not reflected in this
 API.

### OnStateChanged {:#OnStateChanged}

 Called on first connection and whenever the watched usage changes. The provided
 usage will always be the bound usage; it is provided so that an implementation of
 this protocol may be bound to more than one usage.

 Clients must respond to acknowledge the event. Clients that do not acknowledge their
 events will eventually be disconnected.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#Usage'>Usage</a></code>
            </td>
        </tr><tr>
            <td><code>state</code></td>
            <td>
                <code><a class='link' href='#UsageState'>UsageState</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## UsageReporter {:#UsageReporter}
*Defined in [fuchsia.media/usage_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/usage_reporter.fidl#46)*

 A protocol for setting up watchers of audio usages.

### Watch {:#Watch}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>usage</code></td>
            <td>
                <code><a class='link' href='#Usage'>Usage</a></code>
            </td>
        </tr><tr>
            <td><code>usage_watcher</code></td>
            <td>
                <code><a class='link' href='#UsageWatcher'>UsageWatcher</a></code>
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

*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#13)*

 Usage annotating the purpose of the stream being used to render audio.
 An AudioRenderer's usage cannot be changed after creation.  The
 AudioRenderUsage is used by audio policy to dictate how audio streams
 interact with each other.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BACKGROUND</code></td>
            <td><code>0</code></td>
            <td> Stream is intended to be used for ambient or background sound. Streams
 that can be interrupted without consequence should use this.
</td>
        </tr><tr>
            <td><code>MEDIA</code></td>
            <td><code>1</code></td>
            <td> Stream is intended to be used for normal functionality. Streams that
 are part of normal functionality should use this.
</td>
        </tr><tr>
            <td><code>INTERRUPTION</code></td>
            <td><code>2</code></td>
            <td> Stream is intended to interrupt any ongoing function of the device.
 Streams that are used for interruptions like notifications should use
 this.
</td>
        </tr><tr>
            <td><code>SYSTEM_AGENT</code></td>
            <td><code>3</code></td>
            <td> Stream is for interaction with a system agent.  This should be used
 in response to a user initiated trigger.
</td>
        </tr><tr>
            <td><code>COMMUNICATION</code></td>
            <td><code>4</code></td>
            <td> Stream is intended to be used for some form of real time user to user
 communication. Voice/Video chat should use this.
</td>
        </tr></table>

### AudioCaptureUsage {:#AudioCaptureUsage}
Type: <code>uint32</code>

*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#40)*

 Usages annotating the purpose of the stream being used to capture audio. The
 AudioCaptureUsage is used by audio policy to dictate how audio streams
 interact with each other.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>BACKGROUND</code></td>
            <td><code>0</code></td>
            <td> Stream is used to capture audio while in the background.  These streams
 may be active at any the time and are considered privileged.
 Example: Listening for Hotwords
</td>
        </tr><tr>
            <td><code>FOREGROUND</code></td>
            <td><code>1</code></td>
            <td> Stream is intended to be used for normal capture functionality. Streams
 that are used for audio capture while the stream creator is in the
 foreground should use this.
 Example: Voice Recorder
</td>
        </tr><tr>
            <td><code>SYSTEM_AGENT</code></td>
            <td><code>2</code></td>
            <td> Stream is for interaction with a system agent.  This should only be used
 once a user has signalled their intent to have the interaction with an
 interested party.
 Examples: Assistant, Siri, Alexa
</td>
        </tr><tr>
            <td><code>COMMUNICATION</code></td>
            <td><code>3</code></td>
            <td> Stream is intended to be used for some form of real time user to user
 communication. Voice/Video chat should use this.
</td>
        </tr></table>

### Behavior {:#Behavior}
Type: <code>uint32</code>

*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#65)*

 The behaviors applied to streams when multiple are active.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td> Mix the streams.
</td>
        </tr><tr>
            <td><code>DUCK</code></td>
            <td><code>1</code></td>
            <td> Apply a gain to duck the volume of one of the streams. (-14.0db)
</td>
        </tr><tr>
            <td><code>MUTE</code></td>
            <td><code>2</code></td>
            <td> Apply a gain to mute one of the streams. (-160.0db)
</td>
        </tr></table>

### AudioOutputRoutingPolicy {:#AudioOutputRoutingPolicy}
Type: <code>uint32</code>

*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#171)*



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
            <td> An internal error with an unspecified reason.
</td>
        </tr><tr>
            <td><code>INVALID_INPUT_FORMAT_DETAILS</code></td>
            <td><code>2</code></td>
            <td> The client provided invalid input format details.
</td>
        </tr><tr>
            <td><code>INCOMPATIBLE_BUFFERS_PROVIDED</code></td>
            <td><code>3</code></td>
            <td> The server received buffers that are not suitable for the operation to
 be performed. An example of this would be if a Decoder received output
 buffers that are too small to decode a frame into.
</td>
        </tr><tr>
            <td><code>DECODER_UNKNOWN</code></td>
            <td><code>16777217</code></td>
            <td> An internal decoder error with an unspecified reason.
</td>
        </tr><tr>
            <td><code>ENCODER_UNKNOWN</code></td>
            <td><code>33554433</code></td>
            <td> An internal encoder error with an unspecified reason.
</td>
        </tr><tr>
            <td><code>DECRYPTOR_UNKNOWN</code></td>
            <td><code>50331649</code></td>
            <td> An internal decryptor error with an unspecified reason.
</td>
        </tr><tr>
            <td><code>DECRYPTOR_NO_KEY</code></td>
            <td><code>50331650</code></td>
            <td> The requested KeyId is not available for use by the Decryptor. The
 client may try again later if that key becomes available.
</td>
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
            <td> MPEG-2 Low Complexity
</td>
        </tr></table>

### AudioSampleFormat {:#AudioSampleFormat}
Type: <code>uint32</code>

*Defined in [fuchsia.media/stream_type.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_type.fidl#74)*

 Enumerates the supported audio sample formats.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNSIGNED_8</code></td>
            <td><code>1</code></td>
            <td> 8-bit unsigned samples, sample size 1 byte.
</td>
        </tr><tr>
            <td><code>SIGNED_16</code></td>
            <td><code>2</code></td>
            <td> 16-bit signed samples, host-endian, sample size 2 bytes.
</td>
        </tr><tr>
            <td><code>SIGNED_24_IN_32</code></td>
            <td><code>3</code></td>
            <td> 24-bit signed samples in 32 bits, host-endian, sample size 4 bytes.
</td>
        </tr><tr>
            <td><code>FLOAT</code></td>
            <td><code>4</code></td>
            <td> 32-bit floating-point samples, sample size 4 bytes.
</td>
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


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#37)*

 StreamBufferConstraints

 This struct helps ensure that packet count and buffer space are sufficient
 to avoid major problems.  For example, a video decoder needs sufficient
 video frame buffers to hold all potential reference frames concurrently +
 one more video buffer to decode into.  Else, the whole video decode pipe can
 easily deadlock.

 The secondary purpose of this struct is to help ensure that packet count and
 buffer space are sufficient to achieve reasonably performant operation.

 There are separate instances of this struct for stream input and stream
 output.

 Notes about fields:

 For uncompressed video, separate and complete frames in their
 separate buffers (buffer-per-packet mode) are always a requirement.

 per_packet_buffer_bytes.*: These per-packet buffer bytes constraints apply to
 both buffer-per-packet mode and single-buffer mode (see `single_buffer_mode`).
 If buffer-per-packet mode, the constraints apply to each buffer separately.
 If single-buffer mode, the constraints need to be multiplied by the number
 of packets to determine the constraints on the single buffer.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_constraints_version_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> This is a version number the server sets on the constraints to allow the
 server to determine when the client has caught up with the latest
 constraints sent by the server.  The server won't emit output data until
 the client has configured output settings and buffers with a
 buffer_constraints_version_ordinal >= the latest
 buffer_constraints_version_ordinal that had
 buffer_constraints_action_required true.  See
 buffer_constraints_action_required comments for more.

 A buffer_constraints_version_ordinal of 0 is not permitted, to simplify
 initial state handling.  Other than 0, both odd and even version ordinals
 are allowed (in contrast to the stream_lifetime_ordinal, neither the
 client nor server ever has a reason to consider the latest version to be
 stale, so there would be no benefit to disallowing even values).
</td>
        </tr><tr>
            <td>2</td>
            <td><code>default_settings</code></td>
            <td>
                <code><a class='link' href='#StreamBufferSettings'>StreamBufferSettings</a></code>
            </td>
            <td> default_settings

 These settings are "default" settings, not "recommended" settings.

 These "default" settings can be passed to SetInputBufferSettings() /
 SetOutputBufferSettings() as-is without modification, but a client doing
 that must still obey the semantics of packet_count_for_client, despite
 the stream processor server not having any way to really know the proper
 setting for that field.

 For StreamBufferConstraints fields whose names end in "recommended", the
 default_settings will have the corresponding setting field set to that
 recommended value.

 The stream processor promises that these default settings as-is (except
 for buffer_lifetime_ordinal) are guaranteed to satisfy the constraints
 indicated by the other fields of StreamBufferConstraints.  While
 client-side checking that these settings are within the constraints is
 likely unnecessary in the client, the client should still check that
 these values are within client-side reasonable-ness bounds before using
 these values, to avoid letting a stream processor server cause problems
 for the client.

 This structure will always have `single_buffer_mode` false.  See
 `single_buffer_mode_allowed` for whether `single_buffer_mode` true is
 allowed.

 The client must set the buffer_lifetime_ordinal field to a proper value
 before sending back to the server.  The 0 initially in this field will
 be rejected by the server if sent back as-is.  See comments on
 StreamBufferSettings.buffer_lifetime_ordinal.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>per_packet_buffer_bytes_min</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> If a client is using buffer per packet mode, each buffer must be at least
 this large.  If a client is using single-buffer mode, the one buffer must
 be at least per_packet_buffer_bytes_min * packet_count_for_server_min in
 size.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>per_packet_buffer_bytes_recommended</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Must be >= per_packet_buffer_bytes_min.  Delivering more than
 this per input packet might not perform any better, and in fact might
 perform worse.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>per_packet_buffer_bytes_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Must be >= per_packet_buffer_bytes_recommended.  Can be 0xFFFFFFFF if
 there is no explicitly-enforced limit.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>packet_count_for_server_min</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Minimum number of packet_count_for_server.

 Re. input and output:

 This is a strict min for packet_count_for_server, but a client can use
 more packets overall if the client wants to, by using a larger value for
 packet_count_for_server and/or using a non-zero packets_for_client.  A
 good reason to do the former would be if the client might occasionally
 deliver a few not-very-full buffers - or to have a few
 extra packets within which to satisfy stream_input_bytes_min.  A good
 reason to do the latter would be if a client needs to hold onto some
 packets for any extra duration.

 If a client specifies a larger packet_count_for_server value than
 packet_count_for_server_min, a server is permitted (but not encouraged)
 to not make progress until packet_count_for_server are with the server,
 not merely packet_count_for_server_min.

 For decoder input and audio encoder input: The
 packet_count_for_server_min may or may not contain enough data to allow
 the stream processor to make progress without copying into an internal
 side buffer.  If there isn't enough data delivered in
 packet_count_for_server_min packets to permit progress, the stream
 processor must copy into its own side buffer internally to make
 progress.

 If a client intends to use extra packets for client-side purposes, the
 client should specify the extra packets in packets_for_client instead of
 packet_count_for_server, but packet_count_for_server must still be >=
 packet_count_for_server_min.
</td>
        </tr><tr>
            <td>7</td>
            <td><code>packet_count_for_server_recommended</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> This must be at least packet_count_for_server_min and at most
 packet_count_for_server_recommended_max.

 This value is likely to be used as-is by most clients, so if having one
 additional packet is a big performance win in a large percentage of
 scenarios, it can be good for the server to include that additional
 packet in this value.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>packet_count_for_server_recommended_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> This can be the same as packet_count_for_server_max or can be lower.
 Values above this value and <= packet_count_for_server_max are not
 recommended by the stream processor, but should still work given
 sufficient resources available to both the client and the stream
 processor.
</td>
        </tr><tr>
            <td>9</td>
            <td><code>packet_count_for_server_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> This can be 0xFFFFFFFF if there's no stream processor-enforced max, but
 stream processors are encouraged to set a large but still
 plausibly-workable max, and clients are encouraged to request a number
 of packets that isn't excessively large for the client's scenario.
</td>
        </tr><tr>
            <td>10</td>
            <td><code>packet_count_for_client_min</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Normally this would be an implicit 0, but for now we have a min so we can
 force the total number of packets to be a specific number that we know
 works for the moment.
</td>
        </tr><tr>
            <td>11</td>
            <td><code>packet_count_for_client_max</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The client must set packet_count_for_client to be <=
 packet_count_for_client_max.

 This value must be at least 1.  This can be 0xFFFFFFFF if there's no
 stream-processor-enforced max.  Clients are encouraged to request a
 number of packets that isn't excessively large for the client's
 scenario.
</td>
        </tr><tr>
            <td>12</td>
            <td><code>single_buffer_mode_allowed</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> `single_buffer_mode_allowed` false allows a stream processor that's not
 required to support single-buffer mode for a given input or output the
 ability to decline to support single-buffer mode on that input/output.

 All encoder output, regardless of audio or video: server support for
 single-buffer mode is optional.

 Audio decoder output: server support for single-buffer mode is required.

 Video decoder output: There is little reason for a video decoder to
 support single-buffer mode on output.  Nearly all video decoders will set
 this to false for their output.

 All decoder inputs: Servers must support single-buffer mode on input.
 The client is responsible for managing the input buffer space such that
 filling an input packet doesn't over-write any portion of an input
 packet already in flight to the stream processor.

 Encoder inputs: Server support for single-buffer mode on encoder input is
 optional.  This is more often useful for audio than for video.

 Support for buffer-per-packet mode is always required on both input and
 output, regardless of stream processor type.
</td>
        </tr><tr>
            <td>13</td>
            <td><code>is_physically_contiguous_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the buffers need to be physically contiguous pages, such as those
 allocated using zx_vmo_create_contiguous().
</td>
        </tr><tr>
            <td>14</td>
            <td><code>very_temp_kludge_bti_handle</code></td>
            <td>
                <code>handle&lt;handle&gt;</code>
            </td>
            <td> VERY TEMPORARY HACK / KLUDGE - we want the BufferAllocator (or one of
 the participant drivers that needs physically contiguous buffers) to
 call zx_vmo_create_contiguous(), definitely not the StreamProcessor
 client, but until the BufferAllocator can be reached from a driver, this
 is to grant the client special powers it really shouldn't have, very
 temporarily until BufferAllocator is hooked up properly at which point
 this can be removed. Strictly speaking we could reverse which end
 allocates buffers in the StreamProcessor interface to avoid this hack
 even before BufferAllocator, but the overall path seems shorter if we
 jump directly from this to using BufferAllocator.

</td>
        </tr></table>

### StreamOutputConstraints {:#StreamOutputConstraints}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#222)*

 The stream-processor-controlled output configuration, including both
 StreamBufferConstraints for the output and FormatDetails for the output.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A client which always immediately re-configures output buffers on
 receipt of OnOutputConstraints() with buffer_constraints_action_required
 true can safely ignore this field.

 A client is permitted to ignore an OnOutputConstraints() message even with
 buffer_constraints_action_required true if the client knows the server
 has already been told to discard the remainder of the stream with the
 same stream_lifetime_ordinal or if this stream_lifetime_ordinal field is
 set to 0.  The server is required to re-send needed output config via
 OnOutputConstraints() with new stream_lifetime_ordinal and
 buffer_constraints_action_required true, if the most recent completed
 server-side output config isn't what the server wants/needs yet for the
 new stream.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_constraints_action_required</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> When the buffer constraints are delivered, they indicate whether action
 is required.  A false value here permits delivery of constraints which
 are fresher without forcing a buffer reconfiguration.  If this is false,
 a client cannot assume that it's safe to immediately re-configure output
 buffers.  If this is true, the client can assume it's safe to
 immediately configure output buffers once.

 A client is permitted to ignore buffer constraint versions which have
 buffer_constraints_action_required false.  The server is not permitted
 to change buffer_constraints_action_required from false to true for the
 same buffer_constraints_version_ordinal.

 For each configuration, a client must use new buffers, never buffers
 that were previously used for anything else, and never buffers
 previously used for any other StreamProcessor purposes.  This rule
 exists for multiple good reasons, relevant to both mid-stream changes,
 and changes on stream boundaries. A client should just use new buffers
 each time.

 When this is true, the server has already de-refed as many low-level
 output buffers as the server can while still performing efficient
 transition to the new buffers and will de-ref the rest asap.  A Sync()
 is not necessary to achieve non-overlap of resource usage to the extent
 efficiently permitted by the formats involved.

 If buffer_constraints_action_required is true, the server _must_ not
 deliver more output data until after output buffers have been configured
 (or re-configured) by the client.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>buffer_constraints</code></td>
            <td>
                <code><a class='link' href='#StreamBufferConstraints'>StreamBufferConstraints</a></code>
            </td>
            <td></td>
        </tr></table>

### StreamOutputFormat {:#StreamOutputFormat}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#270)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> A client is permitted to ignore an OnOutputFormat() message even with
 buffer_constraints_action_required true if the client knows the server
 has already been told to discard the remainder of the stream with the
 same stream_lifetime_ordinal or if this stream_lifetime_ordinal field is
 set to 0.  The server is required to re-send needed output config via
 OnOutputConstraints() with new stream_lifetime_ordinal and
 buffer_constraints_action_required true, if the most recent completed
 server-side output config isn't what the server wants/needs yet for the
 new stream.

 The server is required to send an OnOutputFormat() before the first
 output packet of a stream.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>format_details</code></td>
            <td>
                <code><a class='link' href='#FormatDetails'>FormatDetails</a></code>
            </td>
            <td> If format_details.format_details_version_ordinal changes, the client
 should inspect the new format details and determine if it must adjust to
 the new format. The server guarantees that if the format has changed, then
 format_details.format_details_version_ordinal will change, but a change
 to format_details.format_details_version_ordinal does not guarantee that
 the format details actually changed.  Servers are strongly encouraged to
 not change format_details.format_details_version_ordinal other than
 before the first output data of a stream unless there is a real
 mid-stream format change in the stream.  Unnecessary mid-stream format
 changes can cause simpler clients that have no need to handle mid-stream
 format changes to just close the channel.  Format changes before the
 first output data of a stream are not "mid-stream" in this context -
 those can be useful for stream format detection / setup reasons.

 Note that in case output buffers don't really need to be re-configured
 despite a format change, a server is encouraged, but not required, to
 set buffer_constraints_action_required false on the message that conveys
 the new format details.  Simpler servers may just treat the whole output
 situation as one big thing and demand output buffer reconfiguration on
 any change in the output situation.

 A client may or may not actually handle a new buffer_constraints with
 buffer_constraints_action_required false, but the client should always
 track the latest format_details.

 An updated format_details is ordered with respect to emitted output
 packets, and applies to all subsequent packets until the next
 format_details with larger version_ordinal.  A simple client that does
 not intend to handle mid-stream format changes should still keep track
 of the most recently received format_details until the first output
 packet arrives, then lock down the format details, handle those format
 details, and verify that any
 format_details.format_details_version_ordinal received from the server
 is the same as the locked-down format_details, until the client is done
 with the stream.  Even such a simple client must tolerate
 format_details.format_details_version_ordinal changing multiple times
 before the start of data output from a stream (any stream - the first
 stream or a subsequent stream).  This allows a stream processor to
 request that output buffers and output format be configured
 speculatively, and for the output config to be optionally adjusted by
 the server before the first data output from a stream after the server
 knows everything it needs to know to fully establish the initial output
 format details.  This simplifies stream processor server implementation,
 and allows a clever stream processor server to guess it's output config
 for lower latency before any input data, while still being able to fix
 the output config (including format details) if the guess turns out to
 be wrong.

 Whether the format_details.format_details_version_ordinal will actually
 change mid-stream is a per-stream-processor and per-stream detail that
 is not specified in comments here, and in most cases also depends on
 whether the format changes on the input to the stream processor.
 Probably it'll be fairly common for a client to use a format which
 technically supports mid-stream format change, but the client happens to
 know that none of the streams the client intends to process will ever
 have a mid-stream format change.
</td>
        </tr></table>

### StreamOutputConfig {:#StreamOutputConfig}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#345)*



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


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#407)*

 See relevant corresponding constraints in StreamBufferConstraints.  The
 settings must satisfy the constraints.

 The client informs the stream processor of these settings and then
 separately informs the stream processor of each buffer.

 The total packet count is split into two pieces to disambiguate how many
 packets are allocated for the client to hold onto for whatever reason,
 vs. how many packets are allocated for the server to hold onto for
 whatever reason.

 Extra packets to provide slack for performance reasons can be in either
 category, but typically packet_count_for_server_recommended will already
 include any performance-relevant slack for the server's benefit.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The containing message starts a new buffer_lifetime_ordinal.

 There is a separate buffer_lifetime_ordinal for input vs. output.

 Re-use of the same value is not allowed.  Values must be odd.  Values
 must only increase (increasing by more than 2 is permitted).

 A buffer_lifetime_ordinal lifetime starts at SetInputBufferSettings() or
 SetOutputBufferSettings(), and ends at the earlier of
 CloseCurrentStream() with release_input_buffers/release_output_buffers
 set or SetOutputBufferSettings() with new buffer_lifetime_ordinal in the
 case of mid-stream output config change.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_constraints_version_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> This value indicates which version of constraints the client is/was aware
 of so far.

 For input, this must always be 0 because constraints don't change for
 input (settings can change, but there's no settings vs current
 constraints synchronization issue on input).

 For output, this allows the server to know when the client is
 sufficiently caught up before the server will generate any more output.

 When there is no active stream, a client is permitted to re-configure
 buffers again using the same buffer_constraints_version_ordinal.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>packet_count_for_server</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> How many packets the client is allocating for the stream processor
 server's use. This must be >=
 StreamBufferConstraints.packet_count_for_server_min.  If constraints
 change such that this would no longer be true, the server will send an
 OnOutputConstraints() event.

 The stream processor server is allowed to demand that all of
 packet_count_for_server become free before making further progress, even
 if packet_count_for_server is > packet_count_for_server_min.

 A reasonable value for this is
 StreamBufferConstraints.packet_count_for_server_recommended.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>packet_count_for_client</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> This must be at least 1.  The server will close the channel if this is 0.

 How many packets the client is allocating for the client's use.  The
 client may hold onto this many packets for arbitrarily-long duration
 without handing these packets to the stream processor, and despite doing
 so, the stream processor will continue to make progress and function
 normally without getting stuck.  The client holding onto additional
 packets transiently is ok, but the client needs to hand those additional
 packets back to the stream processor eventually if the client wants the
 stream processor to make further progress.

 In addition to this value needing to include at least as many packets as
 the client ever intends to concurrently camp on indefinitely, any extra
 slack to benefit client-side performance should also be included here.

 A typical value for this could be at least 2, but it depends strongly on
 client implementation and overall client buffering goals.  It is up to
 the client to determine how many packets are needed in this category by
 any parts of the overall system that will be holding onto packets for
 any reason.  Those parts of the system should have a documented and
 possibly queryable defined value to help determine this number.  Setting
 this value lower than it actually needs to be can result in the stream
 processor not making progress as it sits waiting for packets, with the
 client unable to recycle any more packets to the stream processor.  That
 situation can be difficult to diagnose, while excessively-large values
 here are wasteful, so care is warranted to set this value properly.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>per_packet_buffer_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> In buffer-per-packet mode, we require that each buffer have usable bytes
 equal to per_packet_buffer_bytes.  Use of differently-sized low-level
 buffers is possible, but the size of the portion used via the
 StreamProcessor interface per StreamBuffer must be the same for all the
 buffers.

 In single-buffer mode, we require the portion of the low-level buffer
 used via the StreamProcessor interface to be size
 (packet_count_for_server + packet_count_for_client) *
 per_packet_buffer_bytes.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>single_buffer_mode</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true there is only one buffer, with index 0, which all packets
 must explicitly refer to with buffer_index == 0.

 While it's possible to set up `single_buffer_mode` false with each buffer
 referring to the same underlying VMO, `single_buffer_mode` true is more
 efficient for that case since only one mapping is created.
</td>
        </tr></table>

### StreamBufferPartialSettings {:#StreamBufferPartialSettings}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#509)*

 This struct is used instead of StreamBufferSettings when sysmem is used to
 allocate buffers.  The settings in StreamBufferSettings that are missing from
 StreamBufferPartialSettings can be conveyed from the client directly to
 sysmem.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> The containing message starts a new buffer_lifetime_ordinal.

 There is a separate buffer_lifetime_ordinal for input vs. output.

 Re-use of the same value is not allowed.  Values must be odd.  Values
 must only increase (increasing by more than 2 is permitted).

 A buffer_lifetime_ordinal lifetime starts at SetInputBufferSettings() or
 SetOutputBufferSettings(), and ends at the earlier of
 CloseCurrentStream() with release_input_buffers/release_output_buffers
 set or SetOutputBufferSettings() with new buffer_lifetime_ordinal in the
 case of mid-stream output config change.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_constraints_version_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> This value indicates which version of constraints the client is/was aware
 of so far.

 For input, this must always be 0 because constraints don't change for
 input (settings can change, but there's no settings vs current
 constraints synchronization issue on input).

 For output, this allows the server to know when the client is
 sufficiently caught up before the server will generate any more output.

 When there is no active stream, a client is permitted to re-configure
 buffers again using the same buffer_constraints_version_ordinal.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>single_buffer_mode</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, there is only one buffer, but still typically more than one
 packet.  If false, the # of packets == the number of buffers.

 While it's possible to set up `single_buffer_mode` false with each buffer
 referring to the same underlying VMO, `single_buffer_mode` true is more
 efficient for that case since only one mapping is created.

 This setting is specified by the client, and influences the constraints
 delivered from the StreamProcessor to sysmem (whether there's more than
 one buffer allocated overall or not).  For `single_buffer_mode` true, the
 StreamProcessor is the one to ask sysmem for a buffer - the client should
 refrain from doing so or the StreamProcessor will just fail when more
 than one buffer gets allocated by sysmem.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>packet_count_for_server</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> When `single_buffer_mode` is false:

 The actual packet count will be
 max(packet_count_for_server + packet_count_for_client, sysmem_buffers).
 The sysmem_buffers is BufferCollectionInfo.buffer_count from sysmem if
 using sysmem, or 0 if not using sysmem.

 When `single_buffer_mode` is true:

 The actual packet count is packet_count_for_server +
 packet_count_for_client.

 If not using sysmem, or if using `single_buffer_mode`, these fields must be
 set and consistent with correpsonding fields in StreamBufferConstraints.

 If `single_buffer_mode` false and using sysmem, these fields can both be
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
            <td> The client end of a BufferCollectionToken channel, which the
 StreamProcessor will use to deliver constraints to sysmem and learn of
 buffers allocated by sysmem.

 The client guarantees that the token is already known to sysmem (via
 BufferCollectionToken.Sync(), BufferCollection.Sync(), or
 BufferCollectionEvents.OnDuplicatedTokensKnownByServer()).
</td>
        </tr></table>

### StreamBuffer {:#StreamBuffer}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#601)*

 The StreamBuffer struct represents a pre-configured buffer.

 Both input and output uses StreamBuffer(s), but the two sets of buffers are
 separate.

 The client uses SetInputBufferSettings() + AddInputBuffer() * N to inform
 the stream processor about all the input buffers.

 The client uses SetOutputBufferSettings() + AddOutputBuffer() * N to inform
 the stream processor about all the output buffers.

 When `single_buffer_mode` is true, there is only buffer_index 0 shared by all
 packet(s) of the relevant input or output.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>buffer_lifetime_ordinal</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> When using AddOutputBuffer()/AddInputBuffer(), this must match the
 buffer_lifetime_ordinal of the most recent
 SetOutputBufferSettings()/SetInputBufferSettings().
</td>
        </tr><tr>
            <td>2</td>
            <td><code>buffer_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Buffers must be added via AddOutputBuffer() / AddInputBuffer() in order
 by buffer_index. The buffer_index is always equal to 0 if
 `single_buffer_mode` is true.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>data</code></td>
            <td>
                <code><a class='link' href='#StreamBufferData'>StreamBufferData</a></code>
            </td>
            <td> For each new buffer_lifetime_ordinal, a client must use new low-level
 buffers.  This rule exists for multiple very good reasons, and is
 relevant to mid-stream changes, changes on stream boundaries, and both
 input and output buffers.  A new buffer_lifetime_ordinal needs new
 low-level buffers, not just new StreamBuffer(s).  If you find yourself
 copying compressed input data into new low-level input buffers solely
 due to this rule, consider asking the source of the data for the ability
 to directly fill new VMOs.  The rule exists for good reasons, even for
 input buffers.

 The previous paragraph does not prohibit carving up VMOs into sub-pieces
 and using different sub-pieces as different StreamBuffer(s), with some
 VMOs used for more than one StreamBuffer and possibly others used for
 only one StreamBuffer.  While this is permitted and enables some
 optimizations, it's not expected to be particularly common.
</td>
        </tr></table>

### StreamBufferDataVmo {:#StreamBufferDataVmo}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#645)*

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
            <td> The same VMO can be used by more than one StreamBuffer (only of the same
 buffer_lifetime_ordinal), but each vmo_handle must be a separate handle.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>vmo_usable_start</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> Offset within the VMO of the first usable byte.  Must be < the VMO's size
 in bytes.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>vmo_usable_size</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> VMO-relative offset that's one past the last usable byte.  This can point
 one byte beyond the end of the VMO if desired.  In other words, this can
 be equal to the VMO's size, to indicate that the last byte of the VMO is
 usable (and possibly many byte before that, depending on
 vmo_usable_start).
</td>
        </tr></table>

### PacketHeader {:#PacketHeader}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#669)*

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
            <td> This is which buffer configuration lifetime this header is referring to.

 A packet_index is only really meaningful with respect to a particular
 buffer_lifetime_ordinal.

 See StreamBufferSettings.buffer_lifetime_ordinal.

 For QueueInputPacket(), a server receiving a buffer_lifetime_ordinal that
 isn't the current input buffer_lifetime_ordinal will close the channel.

 For OnFreeInputPacket() and RecycleOutputPacket(), the receiver (client
 or server) must ignore a message with stale buffer_lifetime_ordinal.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>packet_index</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> The overall set of packet_index values is densely packed from 0..count-1
 for input and output separately.  They can be queued in any order.

 Both the client and server should validate the packet_index against the
 known bound and disconnect if it's out of bounds.

 When running in single-buffer mode, the buffer index is always 0.

 The packet_index values don't imply anything about order of use of
 packets. The client should not expect the ordering to remain the same
 over time - the stream processor is free to hold on to an input or
 output packet for a while during which other packet_index values may be
 used multiple times.

 For a given properly-functioning StreamProcessor instance, packet_index
 values will be unique among concurrently-outstanding packets.  Servers
 should validate that a client isn't double-using a packet and clients
 should validate as necessary to avoid undefined or unexpected client
 behavior.
</td>
        </tr></table>

### Packet {:#Packet}


*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#722)*

 A Packet represents a chunk of input or output data to or from a stream
 processor.

 stream processor output:

 While the Packet is outstanding with the client via OnOutputPacket(), the
 stream processor will avoid modifying the referenced output data.  After the
 client calls RecycleOutputPacket(packet_index), the stream processor is
 notified that the client is again ok with the referenced data changing.

 stream processor input:

 The client initially has all packet_index(es) available to fill, and later
 gets packet_index(s) that are again ready to fill via OnFreeInputPacket().
 The client must not modify the referenced data in between QueueInputPacket()
 and OnFreeInputPacket().


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
            <td> The value 1 is the lowest permitted value after stream processor
 creation.  Values sent by the client must be odd.  Values must only
 increase.

 A stream_lifetime_ordinal represents the lifetime of a stream.  All
 messages that are specific to a stream have the stream_lifetime_ordinal
 value and the value is the same for all messages relating to a given
 stream.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>start_offset</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> Which part of the relevant buffer is this packet using.  These are valid
 for input data that's in-flight to the stream processor, and are valid
 for output data from the stream processor.

 For compressed formats and uncompressed audio, the data in
 [start_offset, start_offset + valid_length_bytes) is the contiguously
 valid data referred to by this packet.

 For uncompressed video frames, FormatDetails is the primary means of
 determining which bytes are relevant.  The offsets in FormatDetails
 are relative to the start_offset here.  The valid_length_bytes must be
 large enough to include the full last line of pixel data, including the
 full line stride of the last line (not just the width in pixels of the
 last line).

 Despite these being filled out, some uncompressed video buffers are of
 types that are not readable by the CPU.  These fields being here don't
 imply there's any way for the CPU to read an uncompressed frame.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>valid_length_bytes</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td> This must be > 0.

 The semantics for valid data per packet vary depending on data type as
 follows.

 uncompressed video - A video frame can't be split across packets.  Each
 packet is one video frame.

 uncompressed audio - Regardless of float or int, linear or uLaw, or
 number of channels, a packet must contain an non-negative number of
 complete audio frames, where a single audio frame consists of data for
 all the channels for the same single point in time.  Any
 stream-processor-specific internal details re. lower rate sampling for
 LFE channel or the like should be hidden by the StreamProcessor server
 implementation.

 compressed data input - A packet must contain at least one byte of data.
 See also stream_input_bytes_min.  Splitting AUs at arbitrary byte
 boundaries is permitted, including at boundaries that are in AU headers.

 compressed data output - The stream processor is not required to fully
 fill each output packet's buffer.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>timestamp_ish</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td> This value is not strictly speaking a timestamp.  It is an arbitrary
 unsigned 64-bit number that, under some circumstances, will be passed by
 a stream processor unmodified from an input packet to the
 exactly-corresponding output packet.

 For timestamp_ish values to be propagated from input to output the
 following conditions must be true:
  * promise_separate_access_units_on_input must be true
  * has_timestamp_ish must be true for a given input packet, to have that
    timestamp_ish value (potentially) propagate through to an output
  * the StreamProcessor instance itself decides (async) that the input
    packet generates an output packet - if a given input never generates
    an output packet then the timestamp_ish value on the input will never
    show up on any output packet - depending on the characteristics of the
    input and output formats, and whether a decoder is willing to join
    mid-stream, etc this can be more or less likely to occur, but clients
    should be written to accommodate timestamp_ish values that are fed on
    input but never show up on output, at least to a reasonable degree
    (not crashing, not treating as an error).
</td>
        </tr><tr>
            <td>7</td>
            <td><code>start_access_unit</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> start_access_unit

 If promise_separate_access_units_on_input (TODO(dustingreen): or any
 similar mode for output) is true, this bool must be set appropriately
 depending on whether byte 0 _is_ or _is not_ the start of an access
 unit. The client is required to know, and required to set this boolean
 properly. The server is allowed to infer that when this boolean is
 false, byte 0 is the first byte of a continuation of a
 previously-started AU.  (The byte at start_offset is "byte 0".)

 If promise_separate_access_units_on_input is false, this boolean is
 ignored.
</td>
        </tr><tr>
            <td>8</td>
            <td><code>known_end_access_unit</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> known_end_access_unit

 A client is never required to set this boolean to true.

 If promise_separate_access_units_on_input is true, for input data, this
 boolean must be false if the last byte of this packet is not the last
 byte of an AU, and this boolean _may_ be true if the last byte of this
 packet is the last byte of an AU.  A client delivering one AU at a time
 that's interested in the lowest possible latency via the decoder should
 set this boolean to true when it can be set to true.

 If promise_separate_access_units_on_input is false, this boolean is
 ignored.
</td>
        </tr></table>

### UsageStateUnadjusted {:#UsageStateUnadjusted}


*Defined in [fuchsia.media/usage_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/usage_reporter.fidl#10)*

 A state of audio usages in which no policy actions are taken on any streams with the usage.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### UsageStateDucked {:#UsageStateDucked}


*Defined in [fuchsia.media/usage_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/usage_reporter.fidl#15)*

 A state of audio usages in which a policy decision has been made to temporarily
 lower the volume of all streams with this usage.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>

### UsageStateMuted {:#UsageStateMuted}


*Defined in [fuchsia.media/usage_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/usage_reporter.fidl#20)*

 A state of audio usages in which a policy decision has been made to temporarily
 mute the volume of all streams with this usage.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    </table>



## **UNIONS**

### Usage {:#Usage}
*Defined in [fuchsia.media/audio_core.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#76)*


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
*Defined in [fuchsia.media/stream_processor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#636)*

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

### UsageState {:#UsageState}
*Defined in [fuchsia.media/usage_reporter.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/usage_reporter.fidl#24)*

 The state of audio policy enforcement on a stream or set of streams.

<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>unadjusted</code></td>
            <td>
                <code><a class='link' href='#UsageStateUnadjusted'>UsageStateUnadjusted</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>ducked</code></td>
            <td>
                <code><a class='link' href='#UsageStateDucked'>UsageStateDucked</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>muted</code></td>
            <td>
                <code><a class='link' href='#UsageStateMuted'>UsageStateMuted</a></code>
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
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#35">RENDER_USAGE_COUNT</a></td>
            <td>
                    <code>5</code>
                </td>
                <td><code>uint8</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/audio_core.fidl#62">CAPTURE_USAGE_COUNT</a></td>
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
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#20">METADATA_LABEL_TRACK_NUMBER</a></td>
            <td><code>fuchsia.media.track_number</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#21">METADATA_LABEL_PUBLISHER</a></td>
            <td><code>fuchsia.media.publisher</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#22">METADATA_LABEL_GENRE</a></td>
            <td><code>fuchsia.media.genre</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#23">METADATA_LABEL_COMPOSER</a></td>
            <td><code>fuchsia.media.composer</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#24">METADATA_LABEL_SUBTITLE</a></td>
            <td><code>fuchsia.media.subtitle</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#25">METADATA_LABEL_RELEASE_DATE</a></td>
            <td><code>fuchsia.media.release_date</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#26">METADATA_LABEL_EPISODE</a></td>
            <td><code>fuchsia.media.episode</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#27">METADATA_LABEL_SEASON</a></td>
            <td><code>fuchsia.media.season</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#28">METADATA_LABEL_STUDIO</a></td>
            <td><code>fuchsia.media.studio</code></td>
                    <td><code>String</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/metadata.fidl#32">METADATA_SOURCE_TITLE</a></td>
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
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#381">kDefaultInputPacketCountForClient</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> Default values for input and output
 StreamBufferConstraints.default_settings.packet_count_for_server.

 These are defined as "const" in FIDL to avoid all server implementations
 needing to separately define their own values, and these should be
 reasonable as default values, but strictly speaking this is not intended to
 promise that this value won't change from build to build.  If a client cares
 about a specific number, the client should separately define what that
 number is and ensure that StreamBufferSettings.packet_count_for_client is
 at least large enough.

 In contrast to packet_count_for_client, the packet_count_for_server is much
 more stream-processor-specific, so this file has no numbers for that - each
 stream processor will set those as appropriate for the specific stream
 processor.

 These are not "recommended" values, only "default" values, in the sense that
 the stream processor doesn't really know what the correct setting for these
 values is for a given client, and if the default is not appropriate for a
 client, large problems could result such as deadlock.  See the comments on
 packet_count_for_client.

 Despite these defaults, every client should ideally care about the
 packet_count_for_client setting and should ensure that the setting is at
 least large enough to cover the number of packets the client might ever need
 to camp on for any non-transient duration concurrently.  The defaults are
 only intended to be plausible for some clients, not all clients.

 One for the client to be filling and one in transit.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#383">kDefaultOutputPacketCountForClient</a></td>
            <td>
                    <code>2</code>
                </td>
                <td><code>uint32</code></td>
            <td> One for the client to be rendering, and one in transit.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#390">kDefaultInputIsSingleBufferMode</a></td>
            <td>
                    <code>false</code>
                </td>
                <td><code>bool</code></td>
            <td> For input, this is the default on a fairly arbitrary basis.
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media/stream_processor.fidl#391">kDefaultOutputIsSingleBufferMode</a></td>
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

