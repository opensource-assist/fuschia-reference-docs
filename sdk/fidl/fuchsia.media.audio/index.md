Project: /_project.yaml
Book: /_book.yaml

# fuchsia.media.audio


## **PROTOCOLS**

## GainControl {:#GainControl}
*Defined in [fuchsia.media.audio/gain_control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#16)*

 Enables control and monitoring of audio gain. This interface is typically
 a tear-off of other interfaces. For example, `fuchsia.media.audio.Renderer`
 has a `BindGainControl` method that binds to a gain control that controls
 gain for the renderer.

### SetGain {:#SetGain}

 Sets the gain in decibels.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>gain_db</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### SetGainWithRamp {:#SetGainWithRamp}

 Smoothly changes gain from its current value to specified value, over the
 specified duration (in milliseconds). If 'duration_ns' is 0, gain changes
 immediately. Otherwise, gain changes only while the stream is running.

 Any active or pending ramp is cancelled by subsequent call to SetGain.

 There can be at most 1 active ramp at any time. Any active or pending
 ramp is replaced by a later call to SetGainWithRamp (even if duration is
 0). In this case gain would ramps directly from its most recent
 (mid-ramp) value to the newly-specified one, over the new duration,
 using the new easing.

 Usage example (using time in seconds):
  Time 0
      SetGainWithRamp(MUTED_GAIN_DB, 0, SCALE_LINEAR)         // Ramp 1
      SetGainWithRamp(0.0f, ZX_SEC(4), SCALE_LINEAR)          // Ramp 2
  Time 3
      PlayNoReply(kNoTimestamp, any_media_time)
  Time 4
      PauseNoReply()
  Time 7
      PlayNoReply(kNoTimestamp, any_media_time)
  Time 8
      SetGainWithRamp(MUTED_GAIN_DB, ZX_SEC(1), SCALE_LINEAR) // Ramp 3


 Time 0: Ramp 1 completes immediately, changing the gain to MUTED_GAIN_DB.
         Ramp 2 is pending, since we are not in playback.
 Time 3, Ramp 2 begins ramping from MUTED_GAIN_DB to 0 dB
         (scale 0.0=>1.0).
 Time 4: Ramp 2 pauses (3s remain). Per SCALE_LINEAR, scale is approx.
         0.25.
 Time 7: Ramp 2 resumes from most recent value toward the target.
 Time 8: Ramp 3 replaces Ramp 2 and starts from current scale
         (approx 0.5).
 Time 9: Ramp 3 completes; current scale value is now 0.0 (MUTED_GAIN_DB).


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
                <code>int64</code>
            </td>
        </tr><tr>
            <td><code>rampType</code></td>
            <td>
                <code><a class='link' href='#RampType'>RampType</a></code>
            </td>
        </tr></table>



### SetMute {:#SetMute}

 Sets the mute value. Ramping and mute are fully independent, although
 they both affect the scaling that is applied.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>



### OnGainMuteChanged {:#OnGainMuteChanged}

 Notifies the client of changes in the current gain/mute values.



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





## **ENUMS**

### RampType {:#RampType}
Type: <code>uint16</code>

*Defined in [fuchsia.media.audio/gain_control.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#82)*

 Enumerates gain control ramp types.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>SCALE_LINEAR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>











## **CONSTANTS**



<table>
    <tr><th>Name</th><th>Value</th><th>Type</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#76">MUTED_GAIN_DB</a></td>
            <td>
                    <code>-160</code>
                </td>
                <td><code>float32</code></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.media.audio/gain_control.fidl#79">MAX_GAIN_DB</a></td>
            <td>
                    <code>24</code>
                </td>
                <td><code>float32</code></td>
        </tr>
    
</table>

