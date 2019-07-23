Project: /_project.yaml
Book: /_book.yaml

# fuchsia.settings


## **PROTOCOLS**

## Accessibility {:#Accessibility}
*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#9)*

 Modify or watch accessibility settings that are persisted.

### Watch {:#Watch}

 Gets the current value of all accessibility settings. Returns
 immediately on first call; subsequent calls return when any of the
 values change.

 - `settings` all current values of the accessibility settings.
 * see <a class='link' href='../fuchsia.settings/index.html#AccessibilitySettings'>AccessibilitySettings</a> for their meaning.

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
                <code><a class='link' href='../fuchsia.settings/index.html#AccessibilitySettings'>AccessibilitySettings</a></code>
            </td>
        </tr></table>

### SetAudioDescription {:#SetAudioDescription}

 Enables or disables audio description.

 * see <a class='link' href='../fuchsia.settings/index.html#AccessibilitySettings.audio_description'>AccessibilitySettings.audio_description</a>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>audio_description</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetScreenReader {:#SetScreenReader}

 Enables or disables the screen reader.

 * see <a class='link' href='../fuchsia.settings/index.html#AccessibilitySettings.screen_reader'>AccessibilitySettings.screen_reader</a>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>screen_reader</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetColorInversion {:#SetColorInversion}

 Enables or disables color inversion.

 * see <a class='link' href='../fuchsia.settings/index.html#AccessibilitySettings.color_inversion'>AccessibilitySettings.color_inversion</a>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>color_inversion</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetEnableMagnification {:#SetEnableMagnification}

 Enables or disables magnification by triple-tapping the display.

 * see <a class='link' href='../fuchsia.settings/index.html#AccessibilitySettings.enable_magnification'>AccessibilitySettings.enable_magnification</a>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enable_magnification</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetColorCorrection {:#SetColorCorrection}

 Sets the specific color correction to use, or none.

 * see <a class='link' href='../fuchsia.settings/index.html#AccessibilitySettings.color_correction'>AccessibilitySettings.color_correction</a>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>color_correction</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#ColorBlindnessType'>ColorBlindnessType</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

### SetCaptionsSettings {:#SetCaptionsSettings}

 Updates closed captions settings.

 + `settings` fields to update. Only values explicitly set are changed.
 * see <a class='link' href='../fuchsia.settings/index.html#CaptionsSettings'>CaptionsSettings</a> for their meaning.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#CaptionsSettings'>CaptionsSettings</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Display {:#Display}
*Defined in [fuchsia.settings/display.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/display.fidl#9)*

 Settings related to display

### Watch {:#Watch}

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
                <code><a class='link' href='../fuchsia.settings/index.html#Display_Watch_Result'>Display_Watch_Result</a></code>
            </td>
        </tr></table>

### SetAutoBrightness {:#SetAutoBrightness}

 Enable or disable automatic adjustment of brightness.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>auto_brightness</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Display_SetAutoBrightness_Result'>Display_SetAutoBrightness_Result</a></code>
            </td>
        </tr></table>

### SetBrightness {:#SetBrightness}

 Changes the brightness to a value from 0-1.0, with 1.0 representing
 full brightness. Values greater than 1.0 may be added in future.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>brightness_value</code></td>
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
                <code><a class='link' href='../fuchsia.settings/index.html#Display_SetBrightness_Result'>Display_SetBrightness_Result</a></code>
            </td>
        </tr></table>

## Intl {:#Intl}
*Defined in [fuchsia.settings/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/intl.fidl#12)*

 Settings related to internationalization such as locale, time zone, and
 temperature units.

### Watch {:#Watch}

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
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_Watch_Result'>Intl_Watch_Result</a></code>
            </td>
        </tr></table>

### SetTimeZone {:#SetTimeZone}

 Sets the current time zone based on the [time_zone_id].

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>time_zone_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#TimeZoneId'>TimeZoneId</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_SetTimeZone_Result'>Intl_SetTimeZone_Result</a></code>
            </td>
        </tr></table>

### SetTemperatureUnit {:#SetTemperatureUnit}

 Changes the temperature unit to the specified unit.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_SetTemperatureUnit_Result'>Intl_SetTemperatureUnit_Result</a></code>
            </td>
        </tr></table>

### SetLocales {:#SetLocales}

 Sets the ordered list of preferred locales.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>locales</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#LocaleId'>LocaleId</a>&gt;[10]</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_SetLocales_Result'>Intl_SetLocales_Result</a></code>
            </td>
        </tr></table>

## System {:#System}
*Defined in [fuchsia.settings/system.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/system.fidl#9)*

 Settings related to the general system.

### Watch {:#Watch}

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
                <code><a class='link' href='../fuchsia.settings/index.html#System_Watch_Result'>System_Watch_Result</a></code>
            </td>
        </tr></table>

### SetLoginOverride {:#SetLoginOverride}

 Changes the login overide to the supplied value.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>login_override</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#LoginOverride'>LoginOverride</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>result</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#System_SetLoginOverride_Result'>System_SetLoginOverride_Result</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### Color {:#Color}
*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#134)*



 32-bit RGBA color. Color channels have not been premultiplied by `alpha`.


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>red</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>green</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>blue</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>alpha</code></td>
            <td>
                <code>uint8</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Display_Watch_Response {:#Display_Watch_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#16)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#DisplaySettings'>DisplaySettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Display_SetAutoBrightness_Response {:#Display_SetAutoBrightness_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#23)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Display_SetBrightness_Response {:#Display_SetBrightness_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#30)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Intl_Watch_Response {:#Intl_Watch_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#37)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#IntlSettings'>IntlSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Intl_SetTimeZone_Response {:#Intl_SetTimeZone_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#44)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Intl_SetTemperatureUnit_Response {:#Intl_SetTemperatureUnit_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#51)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### Intl_SetLocales_Response {:#Intl_SetLocales_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#58)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>

### System_Watch_Response {:#System_Watch_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#65)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#SystemSettings'>SystemSettings</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### System_SetLoginOverride_Response {:#System_SetLoginOverride_Response}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#72)*





<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr>
</table>



## **ENUMS**

### ColorBlindnessType {:#ColorBlindnessType}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#72)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>PROTANOMALY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEUTERANOMALY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>TRITANOMALY</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>

### CaptionFontFamily {:#CaptionFontFamily}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#119)*

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

### CaptionEdgeStyle {:#CaptionEdgeStyle}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#142)*

 Font edge style, for better visibility against the background.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>DROP_SHADOW</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>RAISED</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>DEPRESSED</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr><tr>
            <td><code>OUTLINE</code></td>
            <td><code>4</code></td>
            <td></td>
        </tr></table>

### Error {:#Error}
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

### LoginOverride {:#LoginOverride}
Type: <code>uint32</code>

*Defined in [fuchsia.settings/system.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/system.fidl#25)*

 What preferred login behavior has been set.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTOLOGIN_GUEST</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>AUTH_PROVIDER</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### AccessibilitySettings {:#AccessibilitySettings}


*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#51)*

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
                <code><a class='link' href='../fuchsia.settings/index.html#ColorBlindnessType'>ColorBlindnessType</a></code>
            </td>
            <td> What type of color-blindness, if any, to correct for.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>captions_settings</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#CaptionsSettings'>CaptionsSettings</a></code>
            </td>
            <td> What kind of sources get closed captions, and how they look.
</td>
        </tr></table>

### CaptionsSettings {:#CaptionsSettings}


*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#88)*

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
                <code><a class='link' href='../fuchsia.settings/index.html#CaptionFontStyle'>CaptionFontStyle</a></code>
            </td>
            <td> Font style and color used for the closed captions text.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>window_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Color'>Color</a></code>
            </td>
            <td> Border color used around the closed captions window.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>background_color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Color'>Color</a></code>
            </td>
            <td> Background color of the closed captions window.
</td>
        </tr></table>

### CaptionFontStyle {:#CaptionFontStyle}


*Defined in [fuchsia.settings/accessibility.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/accessibility.fidl#106)*

 Font, size, and color of closed captions text.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>family</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#CaptionFontFamily'>CaptionFontFamily</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>color</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Color'>Color</a></code>
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
                <code><a class='link' href='../fuchsia.settings/index.html#CaptionEdgeStyle'>CaptionEdgeStyle</a></code>
            </td>
            <td></td>
        </tr></table>

### DisplaySettings {:#DisplaySettings}


*Defined in [fuchsia.settings/display.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/display.fidl#22)*



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

### IntlSettings {:#IntlSettings}


*Defined in [fuchsia.settings/intl.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/intl.fidl#28)*

 Collection of internationalization-related settings.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>locales</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#LocaleId'>LocaleId</a>&gt;[10]</code>
            </td>
            <td> An ordered list of preferred locales.
</td>
        </tr><tr>
            <td>2</td>
            <td><code>temperature_unit</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#TemperatureUnit'>TemperatureUnit</a></code>
            </td>
            <td> The preferred temperature unit.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>time_zone_id</code></td>
            <td>
                <code><a class='link' href='../fuchsia.intl/index.html'>fuchsia.intl</a>/<a class='link' href='../fuchsia.intl/index.html#TimeZoneId'>TimeZoneId</a></code>
            </td>
            <td> The currently set time zone.
</td>
        </tr></table>

### SystemSettings {:#SystemSettings}


*Defined in [fuchsia.settings/system.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.settings/system.fidl#19)*

 Settings related to the general system.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>mode</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#LoginOverride'>LoginOverride</a></code>
            </td>
            <td> If set, indicates a login behavior specified at runtime.
</td>
        </tr></table>



## **UNIONS**

### Display_Watch_Result {:#Display_Watch_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#19)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Display_Watch_Response'>Display_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Display_SetAutoBrightness_Result {:#Display_SetAutoBrightness_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#26)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Display_SetAutoBrightness_Response'>Display_SetAutoBrightness_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Display_SetBrightness_Result {:#Display_SetBrightness_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#33)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Display_SetBrightness_Response'>Display_SetBrightness_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Intl_Watch_Result {:#Intl_Watch_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#40)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_Watch_Response'>Intl_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Intl_SetTimeZone_Result {:#Intl_SetTimeZone_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#47)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_SetTimeZone_Response'>Intl_SetTimeZone_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Intl_SetTemperatureUnit_Result {:#Intl_SetTemperatureUnit_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#54)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_SetTemperatureUnit_Response'>Intl_SetTemperatureUnit_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### Intl_SetLocales_Result {:#Intl_SetLocales_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#61)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Intl_SetLocales_Response'>Intl_SetLocales_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### System_Watch_Result {:#System_Watch_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#68)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#System_Watch_Response'>System_Watch_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>

### System_SetLoginOverride_Result {:#System_SetLoginOverride_Result}
*Defined in [fuchsia.settings/generated](https://fuchsia.googlesource.com/fuchsia/+/master/generated#75)*


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th></tr><tr>
            <td><code>response</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#System_SetLoginOverride_Response'>System_SetLoginOverride_Response</a></code>
            </td>
            <td></td>
        </tr><tr>
            <td><code>err</code></td>
            <td>
                <code><a class='link' href='../fuchsia.settings/index.html#Error'>Error</a></code>
            </td>
            <td></td>
        </tr></table>







