[TOC]

# fuchsia.accessibility


## **PROTOCOLS**

## ColorTransformHandler {#ColorTransformHandler}
*Defined in [fuchsia.accessibility/color_transform.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/color_transform.fidl#42)*

<p>Handler implemented by the owner of the presentation. Accessibility manager uses this protocol
to make changes to the screen's color transform.</p>

### SetColorTransformConfiguration {#SetColorTransformConfiguration}

<p>Called when the color transform configuration has changed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>configuration</code></td>
            <td>
                <code><a class='link' href='#ColorTransformConfiguration'>ColorTransformConfiguration</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## ColorTransform {#ColorTransform}
*Defined in [fuchsia.accessibility/color_transform.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/color_transform.fidl#50)*

<p>Allows a presentation owner to register a handler for color transforms. This API is implemented
by the Accessibility manager and called by Root Presenter.</p>

### RegisterColorTransformHandler {#RegisterColorTransformHandler}

<p>Registers a handler for changes in the color transform configuration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handler</code></td>
            <td>
                <code><a class='link' href='#ColorTransformHandler'>ColorTransformHandler</a></code>
            </td>
        </tr></table>



## MagnificationHandler {#MagnificationHandler}
*Defined in [fuchsia.accessibility/magnifier.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/magnifier.fidl#9)*

<p>Exposes a privileged magnifier API for camera control, typically on a
|fuchsia.ui.policy.Presentation|.</p>

### SetClipSpaceTransform {#SetClipSpaceTransform}

<p>Sets clip-space x-offset, y-offset, and scale for the presentation.
x and y are in Vulkan NDC and are applied after scaling, which occurs
about the center of the presentation. The callback indicates when the
update has been presented. The identity transform (0, 0, 1) is the
natural state.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>x</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>y</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr><tr>
            <td><code>scale</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>

## Magnifier {#Magnifier}
*Defined in [fuchsia.accessibility/magnifier.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/magnifier.fidl#19)*


### RegisterHandler {#RegisterHandler}

<p>Registers the camera control to be used for applying magnification. If
a previous handler had been registered, that handler is dropped.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handler</code></td>
            <td>
                <code><a class='link' href='#MagnificationHandler'>MagnificationHandler</a></code>
            </td>
        </tr></table>



## SettingsManager {#SettingsManager}
*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#75)*

<p>SettingsManager will be implemented by Accessibility Manager.
The accessibility settings manager is an interface that allows other services to:</p>
<ol>
<li>register as a settings provider. In return, SettingsManager will provide an interface
to modify individual settings.</li>
<li>register themselves to get notified whenever there is a change in Settings.
Ideally there should be just 1 Settings Provider and there can be multiple watchers.
&quot;Settings Service&quot; will be settings Provider for Accessibility. There could be multiple
settings watchers like Root Presenter, Flutter, Chrome, etc.</li>
</ol>

### RegisterSettingProvider {#RegisterSettingProvider}

<p>Register Accessibility settings provider to make modification to accessibility settings.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings_provider_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#SettingsProvider'>SettingsProvider</a>&gt;</code>
            </td>
        </tr></table>



### Watch {#Watch}

<p>Registers a watcher to observe changes in accessibility settings.
When a watcher is registered by calling Watch(), SettingsManager will send all the
Settings as part of registration.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#SettingsWatcher'>SettingsWatcher</a></code>
            </td>
        </tr></table>



## SettingsProvider {#SettingsProvider}
*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#87)*

<p>Interface to update Accessibility Settings. Various Accessibility Settings can be
modified individually.</p>

### SetMagnificationEnabled {#SetMagnificationEnabled}

<p>Enables or disables magnification depending on <code>magnification_enabled</code>.
When <code>magnification_enabled</code> is different from the existing setting,
the zoom factor is reset to 1.0.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>magnification_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#SettingsManagerStatus'>SettingsManagerStatus</a></code>
            </td>
        </tr></table>

### SetMagnificationZoomFactor {#SetMagnificationZoomFactor}

<p>Sets value of zoom factor, provided that magnification is enabled.
Zoom factor must be &gt; 1.0.
Returns ERROR if zoom is disabled or if magnification_zoom_factor &lt; 1.0.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>magnification_zoom_factor</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#SettingsManagerStatus'>SettingsManagerStatus</a></code>
            </td>
        </tr></table>

### SetScreenReaderEnabled {#SetScreenReaderEnabled}

<p>Sets value of screen_reader_enabled, and returns OK.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>screen_reader_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#SettingsManagerStatus'>SettingsManagerStatus</a></code>
            </td>
        </tr></table>

### SetColorInversionEnabled {#SetColorInversionEnabled}

<p>Sets value of color_inversion_enabled, and returns OK.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>color_inversion_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#SettingsManagerStatus'>SettingsManagerStatus</a></code>
            </td>
        </tr></table>

### SetColorCorrection {#SetColorCorrection}

<p>Sets value of color_correction, and returns OK.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>color_correction</code></td>
            <td>
                <code><a class='link' href='#ColorCorrection'>ColorCorrection</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code><a class='link' href='#SettingsManagerStatus'>SettingsManagerStatus</a></code>
            </td>
        </tr></table>

## SettingsWatcher {#SettingsWatcher}
*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#115)*

<p>SettingsWatcher is the client side interface that Settings Manager can
use to notify clients whenever Accessibility Settings change.</p>

### OnSettingsChange {#OnSettingsChange}

<p>Called when accessibility settings elections change.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>accessibility_settings</code></td>
            <td>
                <code><a class='link' href='#Settings'>Settings</a></code>
            </td>
        </tr></table>







## **ENUMS**

### ColorCorrectionMode {#ColorCorrectionMode}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility/color_transform.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/color_transform.fidl#8)*

<p>Specifies color correction mode.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DISABLED</code></td>
            <td><code>0</code></td>
            <td><p>No color correction.</p>
</td>
        </tr><tr>
            <td><code>CORRECT_PROTANOMALY</code></td>
            <td><code>1</code></td>
            <td><p>Color correction for protanomaly (red-green -- reduced sensitivity to red light).</p>
</td>
        </tr><tr>
            <td><code>CORRECT_DEUTERANOMALY</code></td>
            <td><code>2</code></td>
            <td><p>Color correction for deuteranomaly (red-green -- reduced sensitivity to green light).</p>
</td>
        </tr><tr>
            <td><code>CORRECT_TRITANOMALY</code></td>
            <td><code>3</code></td>
            <td><p>Color correction for tritanomaly (blue-yellow -- reduced sensitivity to blue light).</p>
</td>
        </tr></table>

### SettingsManagerStatus {#SettingsManagerStatus}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#7)*



<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>OK</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>ERROR</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr></table>

### ColorCorrection {#ColorCorrection}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#13)*

<p>Specifies color correction mode.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DISABLED</code></td>
            <td><code>0</code></td>
            <td><p>No color correction enabled.</p>
</td>
        </tr><tr>
            <td><code>CORRECT_PROTANOMALY</code></td>
            <td><code>1</code></td>
            <td><p>Color correction enabled for protanomaly (red-green -- reduced sensitivity to red light).</p>
</td>
        </tr><tr>
            <td><code>CORRECT_DEUTERANOMALY</code></td>
            <td><code>2</code></td>
            <td><p>Color correction enabled for deuteranomaly (red-green -- reduced sensitivity to green light).</p>
</td>
        </tr><tr>
            <td><code>CORRECT_TRITANOMALY</code></td>
            <td><code>3</code></td>
            <td><p>Color correction enabled for tritanomaly (blue-yellow -- reduced sensitivity to blue light).</p>
</td>
        </tr></table>



## **TABLES**

### ColorTransformConfiguration {#ColorTransformConfiguration}


*Defined in [fuchsia.accessibility/color_transform.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/color_transform.fidl#25)*

<p>The current configuration for accessibility color transforms, which includes color inversion and
color correction. This always includes the matrix required to apply the appropriate transforms.
Color correction and color inversion may be active simultaneously.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>color_inversion_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When color_inversion_enabled is true, certain colors are inverted across the entire screen.
If this field is omitted behavior should remain unchanged.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>color_correction</code></td>
            <td>
                <code><a class='link' href='#ColorCorrectionMode'>ColorCorrectionMode</a></code>
            </td>
            <td><p>When color_correction is set to DISABLED, colors are displayed normally. When
color_correction has different value, colors are modified to correct for the specified type
of color blindness. If this field is omitted behavior should remain unchanged.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>color_adjustment_matrix</code></td>
            <td>
                <code>float32[9]</code>
            </td>
            <td><p>3x3 Matrix in row-major form which will be used by root presenter to apply color correction
and color inversion, or a combination fo the two. This field should always be set.</p>
</td>
        </tr></table>

### Settings {#Settings}


*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#31)*

<p>Settings is used to represent all the Accessibility Settings along with Matrix
needed to apply Color Correction and Color Inversion.
This table will be used to transfer Settings information between different services to
either modify or get notified about Accessibility Settings.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>magnification_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When magnification_enabled == true, user can specify an area of the screen to be magnified.
Note that actually magnifying the region requires an addition input (gesture, button, etc.).</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>magnification_zoom_factor</code></td>
            <td>
                <code>float32</code>
            </td>
            <td><p>Degree of magnification for magnified area.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>screen_reader_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When screen_reader_enabled == true, user can specify elements of the UI to be described
audibly.
Note that reading a particular element requires an additional input.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>color_inversion_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td><p>When color_inversion_enabled == true, certain colors are inverted across the entire screen.
No additional user input is required for the inversion to take place once enabled.
Colors will continue to be inverted until color_inversion_enabled is set to false.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>color_correction</code></td>
            <td>
                <code><a class='link' href='#ColorCorrection'>ColorCorrection</a></code>
            </td>
            <td><p>When color_correction is set to DISABLED, colors are displayed normally.
When color_correction has different value, colors are modified to correct for the specified
type of color-blindness.
No additional user input is required for corrections to take place once enabled.
Correction will continue to occur until color_correction is set to DISABLED.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>color_adjustment_matrix</code></td>
            <td>
                <code>float32[9]</code>
            </td>
            <td><p>3x3 Matrix in row-major form which will be used by the SettingsManager
client for applying Color Correction and Color Inversion. Display
adapter expects a 3x3 row major matrix and A11y manager stores the
matrix in the same format.
Color Adjustment matrix is used to modify onscreen colors for either
of Deuteranomaly, Protanomaly and Tritanomaly or it can be used for
performing Color Inversion.</p>
</td>
        </tr></table>









