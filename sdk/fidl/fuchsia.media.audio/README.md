[TOC]

# fuchsia.media.audio


## **PROTOCOLS**

## GainControl {#GainControl}
*Defined in [fuchsia.media.audio/gain_control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#17)*

<p>Enables control and monitoring of audio gain. This interface is typically
a tear-off of other interfaces. For example, <code>fuchsia.media.audio.Renderer</code>
has a <code>BindGainControl</code> method that binds to a gain control that controls
gain for the renderer.</p>

### SetGain {#SetGain}

<p>Sets the gain in decibels.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetGainWithRamp {#SetGainWithRamp}

<p>Smoothly changes gain from its current value to specified value, over the
specified duration (in milliseconds). If 'duration_ns' is 0, gain changes
immediately. Otherwise, gain changes only while the stream is running.</p>
<p>Any active or pending ramp is cancelled by subsequent call to SetGain.</p>
<p>There can be at most 1 active ramp at any time. Any active or pending
ramp is replaced by a later call to SetGainWithRamp (even if duration is
0). In this case gain would ramps directly from its most recent
(mid-ramp) value to the newly-specified one, over the new duration,
using the new easing.</p>
<p>Usage example (using time in seconds):
Time 0
SetGainWithRamp(<code>MUTED_GAIN_DB</code>, 0, SCALE_LINEAR)         // Ramp 1
SetGainWithRamp(0.0f, <code>ZX_SEC</code>(4), SCALE_LINEAR)          // Ramp 2
Time 3
PlayNoReply(kNoTimestamp, any_media_time)
Time 4
PauseNoReply()
Time 7
PlayNoReply(kNoTimestamp, any_media_time)
Time 8
SetGainWithRamp(<code>MUTED_GAIN_DB</code>, ZX_SEC(1), SCALE_LINEAR) // Ramp 3</p>
<p>Time 0: Ramp 1 completes immediately, changing the gain to <code>MUTED_GAIN_DB</code>.
Ramp 2 is pending, since we are not in playback.
Time 3, Ramp 2 begins ramping from <code>MUTED_GAIN_DB</code> to 0 dB
(scale 0.0=&gt;1.0).
Time 4: Ramp 2 pauses (3s remain). Per <code>SCALE_LINEAR</code>, scale is approx.
0.25.
Time 7: Ramp 2 resumes from most recent value toward the target.
Time 8: Ramp 3 replaces Ramp 2 and starts from current scale
(approx 0.5).
Time 9: Ramp 3 completes; current scale value is now 0.0 (<code>MUTED_GAIN_DB</code>).</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>duration</code></td>
            <td>
                <code><a class='link' href='../zx/'>zx</a>/<a class='link' href='../zx/#duration'>duration</a></code>
            </td>
        </tr><tr>
            <td><code>rampType</code></td>
            <td>
                <code><a class='link' href='#RampType'>RampType</a></code>
            </td>
        </tr></table>



### SetMute {#SetMute}

<p>Sets the mute value. Ramping and mute are fully independent, although
they both affect the scaling that is applied.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnGainMuteChanged {#OnGainMuteChanged}

<p>Notifies the client of changes in the current gain/mute values.</p>



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

## VolumeControl {#VolumeControl}
*Defined in [fuchsia.media.audio/volume_control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/volume_control.fidl#14)*

<p>A protocol for controlling volume.</p>

### SetVolume {#SetVolume}

<p>Sets the volume of the audio element to the given value in
[0.0, 1.0]. If the value is provided is outside of [0.0, 1.0],
the value is clamped before application.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>volume</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetMute {#SetMute}

<p>Sets whether the controlled element is muted. Mute is not the same
as setting volume to 0.0; volume will persist for the duration of
a mute. If volume was 0.5 before mute, volume will resume at 0.5
following unmute.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>mute</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnVolumeMuteChanged {#OnVolumeMuteChanged}

<p>Emitted when the volume or mute state of the audio element changes.</p>



#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>new_volume</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>new_muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>





## **ENUMS**

### RampType {#RampType}
Type: <code>uint16</code>

*Defined in [fuchsia.media.audio/gain_control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#83)*

<p>Enumerates gain control ramp types.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SCALE_LINEAR</code></td>
            <td><code>1</code></td>
            <td><p>Amplitude scale changes at a fixed rate across the ramp duration.</p>
</td>
        </tr></table>











## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr id="MUTED_GAIN_DB">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#77">MUTED_GAIN_DB</a></td>
            <td>
                    <code>-160</code>
                </td>
                <td><code>float32</code></td>
            <td><p>Gain value producing silence. Gain values less than this value are permitted,
but produce the same effect as this value.</p>
</td>
        </tr>
    <tr id="MAX_GAIN_DB">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#80">MAX_GAIN_DB</a></td>
            <td>
                    <code>24</code>
                </td>
                <td><code>float32</code></td>
            <td><p>Maximum permitted gain value.</p>
</td>
        </tr>
    <tr id="MAX_VOLUME">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/volume_control.fidl#8">MAX_VOLUME</a></td>
            <td>
                    <code>1</code>
                </td>
                <td><code>float32</code></td>
            <td><p>The volume value representing the maximum loudness.</p>
</td>
        </tr>
    <tr id="MIN_VOLUME">
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/volume_control.fidl#11">MIN_VOLUME</a></td>
            <td>
                    <code>0</code>
                </td>
                <td><code>float32</code></td>
            <td><p>The volume value representing silence.</p>
</td>
        </tr>
    
</table>



