[TOC]

# fuchsia.settings


## **PROTOCOLS**

## Accessibility {#Accessibility}
*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#11)*

 Modify or watch accessibility settings that are persisted.

### Watch {#Watch}

 Gets the current value of all accessibility settings. Returns
 immediately on first call; subsequent calls return when any of the
 values change.

 - `settings` all current values of the accessibility settings.
 * see <a class='link' href='#AccessibilitySettings'>AccessibilitySettings</a> for their meaning.

 This call may fail if AccessibilitySettings are not accessible, possibly because of file
 system errors, not being supported on this product, or general service failures.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Accessibility_Watch_Result'>Accessibility_Watch_Result</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Sets [AccessibilitySettings] settings. Any field not explicitly set in the table performs a
 no-op, and will not make any changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#AccessibilitySettings'>AccessibilitySettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Accessibility_Set_Result'>Accessibility_Set_Result</a></code>
            </td>
        </tr></table>

## Audio {#Audio}
*Defined in [fuchsia.settings/audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/audio.fidl#11)*

 Settings related to audio.

### Watch {#Watch}

 Gets the current [AudioSettings]. Returns immediately on first call;
 subsequent calls return when the value changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Audio_Watch_Result'>Audio_Watch_Result</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Sets audio settings. Any field not explicitly set in the table performs a
 no-op, and will not make any changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#AudioSettings'>AudioSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Audio_Set_Result'>Audio_Set_Result</a></code>
            </td>
        </tr></table>

## Device {#Device}
*Defined in [fuchsia.settings/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/device.fidl#8)*


### Watch {#Watch}

 Notifies of a change in information about the device.

 On a given connection, the first call will return the current `settings` value while
 subsequent calls will only return the new `settings` value upon a value change. This
 follows the hanging get pattern.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>device_settings</code></td>
            <td>
                <code><a class='link' href='#DeviceSettings'>DeviceSettings</a></code>
            </td>
        </tr></table>

## Display {#Display}
*Defined in [fuchsia.settings/display.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/display.fidl#9)*

 Settings related to display

### Watch {#Watch}

 Gets the current [DisplaySettings]. Returns immediately on first call;
 subsequent calls return when the value changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Display_Watch_Result'>Display_Watch_Result</a></code>
            </td>
        </tr></table>

### WatchLightSensor {#WatchLightSensor}

 Obtains the current data from the light sensor. Returns immediately on
 first call; subsequent calls return when the light sensor value changes
  by a certain amount measured in lux.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>delta</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Display_WatchLightSensor_Result'>Display_WatchLightSensor_Result</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Sets display settings. Any field not explicitly set in the table performs a
 no-op, and will not make any changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#DisplaySettings'>DisplaySettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Display_Set_Result'>Display_Set_Result</a></code>
            </td>
        </tr></table>

## DoNotDisturb {#DoNotDisturb}
*Defined in [fuchsia.settings/do_not_disturb.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/do_not_disturb.fidl#13)*

 Modify or watch do-not-disturb (DND) mode. While DND is active, distractions
 created by the device are reduced or eliminated. E.g. bootup is silent,
 incoming calls could be rejected or silent, and notifications could be
 paused, silent, or hidden. High-priority disruptions like alarms can be
 allowed.

### Watch {#Watch}

 Gets the current <a class='link' href='#DoNotDisturbSettings'>DoNotDisturbSettings</a>. Returns immediately on first
 call; subsequent calls return when the values change.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#DoNotDisturbSettings'>DoNotDisturbSettings</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Sets <a class='link' href='#DoNotDisturbSettings'>DoNotDisturbSettings</a> settings. Any field not explicitly set in
 the table performs a no-op, and will not make any changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#DoNotDisturbSettings'>DoNotDisturbSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#DoNotDisturb_Set_Result'>DoNotDisturb_Set_Result</a></code>
            </td>
        </tr></table>

## Intl {#Intl}
*Defined in [fuchsia.settings/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/intl.fidl#12)*

 Settings related to internationalization such as locale, time zone, and
 temperature units.

### Watch {#Watch}

 Gets the current [IntlSettings]. Returns immediately on first call;
 subsequent calls return when the value changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Intl_Watch_Result'>Intl_Watch_Result</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Sets [IntlSettings] settings. Any field not explicitly set in the table performs a
 no-op, and will not make any changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#IntlSettings'>IntlSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Intl_Set_Result'>Intl_Set_Result</a></code>
            </td>
        </tr></table>

## Privacy {#Privacy}
*Defined in [fuchsia.settings/privacy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/privacy.fidl#8)*


### Watch {#Watch}

 Notifies of a change in privacy settings.

 On a given connection, the first call will return the current `settings` value while
 subsequent calls will only return the new `settings` value upon a value change. This
 follows the hanging get pattern.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Privacy_Watch_Result'>Privacy_Watch_Result</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Sets the privacy settings.

 Any field not explicitly set in `settings` performs a no-op, and will not make any changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#PrivacySettings'>PrivacySettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Privacy_Set_Result'>Privacy_Set_Result</a></code>
            </td>
        </tr></table>

## Setup {#Setup}
*Defined in [fuchsia.settings/setup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/setup.fidl#9)*

 Settings that influence the device's setup behavior.

### Watch {#Watch}

 Gets the current [SetupSettings]. Returns immediately on first call;
 subsequent calls return when the value changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#SetupSettings'>SetupSettings</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Changes the settings specified in [SetupSettings]. Any field not set in
 the table will not perform any system operation. An error will be
 returned if the provided settings is an invalid change (for example, if
 it is empty).

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#SetupSettings'>SetupSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#Setup_Set_Result'>Setup_Set_Result</a></code>
            </td>
        </tr></table>

## System {#System}
*Defined in [fuchsia.settings/system.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/system.fidl#9)*

 Settings related to the general system.

### Watch {#Watch}

 Gets the current [SystemSettings]. Returns immediately on first call;
 subsequent calls return when the value changes.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#System_Watch_Result'>System_Watch_Result</a></code>
            </td>
        </tr></table>

### Set {#Set}

 Changes the settings specified in [SystemSettings]. Any field not set in the table will
 not perform any system operation.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#SystemSettings'>SystemSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='#System_Set_Result'>System_Set_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Accessibility_Watch_Response {#Accessibility_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#AccessibilitySettings'>AccessibilitySettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Accessibility_Set_Response {#Accessibility_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Audio_Watch_Response {#Audio_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#AudioSettings'>AudioSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Audio_Set_Response {#Audio_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Display_Watch_Response {#Display_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#DisplaySettings'>DisplaySettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Display_WatchLightSensor_Response {#Display_WatchLightSensor_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>light_sensor_data</code></td>
            <td>
                <code><a class='link' href='#LightSensorData'>LightSensorData</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Display_Set_Response {#Display_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### DoNotDisturb_Set_Response {#DoNotDisturb_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Intl_Watch_Response {#Intl_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#IntlSettings'>IntlSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Intl_Set_Response {#Intl_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Privacy_Watch_Response {#Privacy_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#PrivacySettings'>PrivacySettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Privacy_Set_Response {#Privacy_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Setup_Set_Response {#Setup_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### System_Watch_Response {#System_Watch_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='#SystemSettings'>SystemSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### System_Set_Response {#System_Set_Response}
*generated*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ColorBlindnessType {#ColorBlindnessType}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#50)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td> No color blindness.
</td>
        </tr><tr>
            <td><code>PROTANOMALY</code></td>
            <td><code>1</code></td>
            <td> Red-green color blindness due to reduced sensitivity to red light.
</td>
        </tr><tr>
            <td><code>DEUTERANOMALY</code></td>
            <td><code>2</code></td>
            <td> Red-green color blindness due to reduced sensitivity to green light.
</td>
        </tr><tr>
            <td><code>TRITANOMALY</code></td>
            <td><code>3</code></td>
            <td> Blue-yellow color blindness. It is due to reduced sensitivity to blue
 light.
</td>
        </tr></table>

### CaptionFontFamily {#CaptionFontFamily}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#97)*

 Font family groups for closed captions, specified by 47 CFR §79.102(k).


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>UNKNOWN</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>MONOSPACED_SERIF</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROPORTIONAL_SERIF</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>MONOSPACED_SANS_SERIF</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROPORTIONAL_SANS_SERIF</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr><tr>
            <td><code>CASUAL</code></td>
            <td><code>5</code></td>
            <td></td>
        </tr><tr>
            <td><code>CURSIVE</code></td>
            <td><code>6</code></td>
            <td></td>
        </tr><tr>
            <td><code>SMALL_CAPITALS</code></td>
            <td><code>7</code></td>
            <td></td>
        </tr></table>

### EdgeStyle {#EdgeStyle}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#109)*

 Edge style for fonts as specified in 47 CFR §79.103(c)(7)


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td> No border around fonts.
</td>
        </tr><tr>
            <td><code>DROP_SHADOW</code></td>
            <td><code>1</code></td>
            <td> A shadow "behind" and slightly offset from each edge.
</td>
        </tr><tr>
            <td><code>RAISED</code></td>
            <td><code>2</code></td>
            <td> A bevel that mimics a 3D raised effect.
</td>
        </tr><tr>
            <td><code>DEPRESSED</code></td>
            <td><code>3</code></td>
            <td> A bevel that mimics a 3D depressed effect.
</td>
        </tr><tr>
            <td><code>OUTLINE</code></td>
            <td><code>4</code></td>
            <td> A plain border around each shapes.
</td>
        </tr></table>

### AudioStreamSettingSource {#AudioStreamSettingSource}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/audio.fidl#22)*

 The source of the volume settings. The volume is set according to the source.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>USER</code></td>
            <td><code>0</code></td>
            <td> The volume is set by the user. When the |source| in AudioStreamSettings is
 set to this, the audio volume is set to |user_volume|.
</td>
        </tr><tr>
            <td><code>SYSTEM</code></td>
            <td><code>1</code></td>
            <td> The system takes control of the volume. This is used when the system constantly
 calculates and changes the volume. The volume is not stored for this source.
</td>
        </tr></table>

### Error {#Error}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/settings.fidl#8)*

 Common error code used across different settings.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>FAILED</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>UNSUPPORTED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr></table>

### LoginOverride {#LoginOverride}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/system.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/system.fidl#26)*

 What preferred login behavior has been set.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td> No override has been set.
</td>
        </tr><tr>
            <td><code>AUTOLOGIN_GUEST</code></td>
            <td><code>2</code></td>
            <td> Do not require an account and login always as guest.
</td>
        </tr><tr>
            <td><code>AUTH_PROVIDER</code></td>
            <td><code>3</code></td>
            <td> Requires a provisioned account through auth provider.
</td>
        </tr></table>



## **TABLES**

### AccessibilitySettings {#AccessibilitySettings}


*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#29)*

 Supported accessibility settings.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>audio_description</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> For videos, use an alternative audio track (akin to changing languages)
 that explains what is happening visually while there is no dialogue.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>screen_reader</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Read aloud elements of the screen selected by the user.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>color_inversion</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Invert colors on the screen.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>enable_magnification</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Interpret triple-tap on the touchscreen as a command to zoom in.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>color_correction</code></td>
            <td>
                <code><a class='link' href='#ColorBlindnessType'>ColorBlindnessType</a></code>
            </td>
            <td> What type of color-blindness, if any, to correct for.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>captions_settings</code></td>
            <td>
                <code><a class='link' href='#CaptionsSettings'>CaptionsSettings</a></code>
            </td>
            <td> What kind of sources get closed captions, and how they look.
</td>
        </tr></table>

### CaptionsSettings {#CaptionsSettings}


*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#66)*

 What kind of sources get closed captions, and how they look.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>for_media</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Closed captions enabled for media sources of audio.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>for_tts</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Closed captions enabled for Text-To-Speech sources of audio.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>font_style</code></td>
            <td>
                <code><a class='link' href='#CaptionFontStyle'>CaptionFontStyle</a></code>
            </td>
            <td> Font style and color used for the closed captions text.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>window_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgba'>ColorRgba</a></code>
            </td>
            <td> Border color used around the closed captions window.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>background_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgba'>ColorRgba</a></code>
            </td>
            <td> Background color of the closed captions window.
</td>
        </tr></table>

### CaptionFontStyle {#CaptionFontStyle}


*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#84)*

 Font, size, and color of closed captions text.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='#CaptionFontFamily'>CaptionFontFamily</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.ui.types/'>fuchsia.ui.types</a>/<a class='link' href='../fuchsia.ui.types/#ColorRgba'>ColorRgba</a></code>
            </td>
            <td> 47 CFR §79.103(c)(2) requires at least 3-bit RGB for user override of
 closed-captions color.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>relative_size</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Size of closed captions text relative to the default captions size. A
 range of [0.5, 2] is guaranteed to be supported (as 47 CFR §79.103(c)(4)
 establishes).
</td>
        </tr><tr>
            <td>4</td>
            <td><code>char_edge_style</code></td>
            <td>
                <code><a class='link' href='#EdgeStyle'>EdgeStyle</a></code>
            </td>
            <td></td>
        </tr></table>

### Volume {#Volume}


*Defined in [fuchsia.settings/audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/audio.fidl#33)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>level</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> The volume level ranged [0.0, 1.0]. The level maps to a dbfs value from a volume
 curve in the setting service.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> True if the volume should be muted. If this is true, then the volume is silent,
 regardless of |level|.
</td>
        </tr></table>

### AudioStreamSettings {#AudioStreamSettings}


*Defined in [fuchsia.settings/audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/audio.fidl#43)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>stream</code></td>
            <td>
                <code><a class='link' href='../fuchsia.media/'>fuchsia.media</a>/<a class='link' href='../fuchsia.media/#AudioRenderUsage'>AudioRenderUsage</a></code>
            </td>
            <td> The audio stream which the settings are applying to.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>source</code></td>
            <td>
                <code><a class='link' href='#AudioStreamSettingSource'>AudioStreamSettingSource</a></code>
            </td>
            <td> The volume of |stream| is set according to the volume settings from |source|.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>user_volume</code></td>
            <td>
                <code><a class='link' href='#Volume'>Volume</a></code>
            </td>
            <td> User level volume setting. If the |source| is USER, then the volume is set to
 |user_volume|.
</td>
        </tr></table>

### AudioSettings {#AudioSettings}


*Defined in [fuchsia.settings/audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/audio.fidl#55)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>streams</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#AudioStreamSettings'>AudioStreamSettings</a>&gt;[5]</code>
            </td>
            <td> Contains the volume setting for all audio stream settings. There should only be
 one AudioStreamSettings for each fuchsia.media.AudioRenderUsage.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>input</code></td>
            <td>
                <code><a class='link' href='#AudioInput'>AudioInput</a></code>
            </td>
            <td> Settings related to the audio input.
</td>
        </tr></table>

### AudioInput {#AudioInput}


*Defined in [fuchsia.settings/audio.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/audio.fidl#64)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>muted</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Whether the audio input is muted. Takes into consideration the hardware state.
</td>
        </tr></table>

### DeviceSettings {#DeviceSettings}


*Defined in [fuchsia.settings/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/device.fidl#18)*

 Information about the device.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>build_tag</code></td>
            <td>
                <code>string[50]</code>
            </td>
            <td> The identifier representing the specific build that the device
 is currently running. Read-only field, cannot be set by client.
</td>
        </tr></table>

### DisplaySettings {#DisplaySettings}


*Defined in [fuchsia.settings/display.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/display.fidl#24)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>auto_brightness</code></td>
            <td>
                <code>bool</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>brightness_value</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr></table>

### LightSensorData {#LightSensorData}


*Defined in [fuchsia.settings/display.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/display.fidl#29)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>illuminance_lux</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Brightness from the light sensor measured in lux
</td>
        </tr></table>

### DoNotDisturbSettings {#DoNotDisturbSettings}


*Defined in [fuchsia.settings/do_not_disturb.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/do_not_disturb.fidl#24)*

 Settings related to do-not-disturb (DND) mode.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>user_initiated_do_not_disturb</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the device is in do-not-disturb (DND) mode. Change this value
 if you're directly responding to a user-initiated event.

 Note that the device could still be in DND mode even if this is set to
 `false`, as <a class='link' href='#night_mode_initiated_do_not_disturb'>night_mode_initiated_do_not_disturb</a> might be `true`. To
 actually disable DND mode, set both fields to `false`.

 To know whether DND is enabled, you need to do a boolean OR of both
 fields.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>night_mode_initiated_do_not_disturb</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> If true, the device is in do-not-disturb (DND) mode. Change this value
 if you're trying to enable or disable DND based on a nightly schedule.

 Note that the device could still be in DND mode even if this is set to
 `false`, as <a class='link' href='#user_initiated_do_not_disturb'>user_initiated_do_not_disturb</a> might be `true`. Do not
 set that field to `false` unless you're directly responding to a
 user-initiated event.

 To know whether DND is enabled, you need to do a boolean OR of both
 fields.
</td>
        </tr></table>

### IntlSettings {#IntlSettings}


*Defined in [fuchsia.settings/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/intl.fidl#23)*

 Collection of internationalization-related settings.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>locales</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#LocaleId'>LocaleId</a>&gt;[10]</code>
            </td>
            <td> An ordered list of preferred locales.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td> The preferred temperature unit.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>time_zone_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/#TimeZoneId'>TimeZoneId</a></code>
            </td>
            <td> The currently set time zone.
</td>
        </tr></table>

### PrivacySettings {#PrivacySettings}


*Defined in [fuchsia.settings/privacy.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/privacy.fidl#22)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>user_data_sharing_consent</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> Reflects the user consent to have their user data shared with the product owner, e.g., for
 metrics collection and crash reporting.
</td>
        </tr></table>

### SetupSettings {#SetupSettings}


*Defined in [fuchsia.settings/setup.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/setup.fidl#21)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>enabled_configuration_interfaces</code></td>
            <td>
                <code><a class='link' href='#ConfigurationInterfaces'>ConfigurationInterfaces</a></code>
            </td>
            <td> Specifies the network interfaces that the device can be configured
 over during setup.
</td>
        </tr></table>

### SystemSettings {#SystemSettings}


*Defined in [fuchsia.settings/system.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/system.fidl#20)*

 Settings related to the general system.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='#LoginOverride'>LoginOverride</a></code>
            </td>
            <td> If set, indicates a login behavior specified at runtime.
</td>
        </tr></table>



## **UNIONS**

### Accessibility_Watch_Result {#Accessibility_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Accessibility_Watch_Response'>Accessibility_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Accessibility_Set_Result {#Accessibility_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Accessibility_Set_Response'>Accessibility_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Audio_Watch_Result {#Audio_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Audio_Watch_Response'>Audio_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Audio_Set_Result {#Audio_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Audio_Set_Response'>Audio_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Display_Watch_Result {#Display_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Display_Watch_Response'>Display_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Display_WatchLightSensor_Result {#Display_WatchLightSensor_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Display_WatchLightSensor_Response'>Display_WatchLightSensor_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Display_Set_Result {#Display_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Display_Set_Response'>Display_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### DoNotDisturb_Set_Result {#DoNotDisturb_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#DoNotDisturb_Set_Response'>DoNotDisturb_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Intl_Watch_Result {#Intl_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Intl_Watch_Response'>Intl_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Intl_Set_Result {#Intl_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Intl_Set_Response'>Intl_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Privacy_Watch_Result {#Privacy_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Privacy_Watch_Response'>Privacy_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Privacy_Set_Result {#Privacy_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Privacy_Set_Response'>Privacy_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Setup_Set_Result {#Setup_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#Setup_Set_Response'>Setup_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### System_Watch_Result {#System_Watch_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#System_Watch_Response'>System_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### System_Set_Result {#System_Set_Result}
*generated*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='#System_Set_Response'>System_Set_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>





## **BITS**

### ConfigurationInterfaces {#ConfigurationInterfaces}
Type: <code>uint32</code>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td>ETHERNET</td>
            <td>1</td>
            <td></td>
        </tr><tr>
            <td>WIFI</td>
            <td>2</td>
            <td></td>
        </tr></table>



