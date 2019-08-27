Project: /_project.yaml
Book: /_book.yaml

# fuchsia.accessibility


## **PROTOCOLS**

## SettingsManager {:#SettingsManager}
*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#75)*

 SettingsManager will be implemented by Accessibility Manager.
 The accessibility settings manager is an interface that allows other services to:
   1. register as a settings provider. In return, SettingsManager will provide an interface
      to modify individual settings.
   2. register themselves to get notified whenever there is a change in Settings.
 Ideally there should be just 1 Settings Provider and there can be multiple watchers.
 "Settings Service" will be settings Provider for Accessibility. There could be multiple
 settings watchers like Root Presenter, Flutter, Chrome, etc.

### RegisterSettingProvider {:#RegisterSettingProvider}

 Register Accessibility settings provider to make modification to accessibility settings.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>settings_provider_request</code></td>
            <td>
                <code>request&lt;<a class='link' href='#SettingsProvider'>SettingsProvider</a>&gt;</code>
            </td>
        </tr></table>



### Watch {:#Watch}

 Registers a watcher to observe changes in accessibility settings.
 When a watcher is registered by calling Watch(), SettingsManager will send all the
 Settings as part of registration.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>watcher</code></td>
            <td>
                <code><a class='link' href='#SettingsWatcher'>SettingsWatcher</a></code>
            </td>
        </tr></table>



## SettingsProvider {:#SettingsProvider}
*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#87)*

 Interface to update Accessibility Settings. Various Accessibility Settings can be
 modified individually.

### SetMagnificationEnabled {:#SetMagnificationEnabled}

 Enables or disables magnification depending on `magnification_enabled`.
 When `magnification_enabled` is different from the existing setting,
 the zoom factor is reset to 1.0.

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

### SetMagnificationZoomFactor {:#SetMagnificationZoomFactor}

 Sets value of zoom factor, provided that magnification is enabled.
 Zoom factor must be > 1.0.
 Returns ERROR if zoom is disabled or if magnification_zoom_factor < 1.0.

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

### SetScreenReaderEnabled {:#SetScreenReaderEnabled}

 Sets value of screen_reader_enabled, and returns OK.

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

### SetColorInversionEnabled {:#SetColorInversionEnabled}

 Sets value of color_inversion_enabled, and returns OK.

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

### SetColorCorrection {:#SetColorCorrection}

 Sets value of color_correction, and returns OK.

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

## SettingsWatcher {:#SettingsWatcher}
*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#115)*

 SettingsWatcher is the client side interface that Settings Manager can
 use to notify clients whenever Accessibility Settings change.

### OnSettingsChange {:#OnSettingsChange}

 Called when accessibility settings elections change.

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

### SettingsManagerStatus {:#SettingsManagerStatus}
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

### ColorCorrection {:#ColorCorrection}
Type: <code>uint32</code>

*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#13)*

 Specifies color correction mode.


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>DISABLED</code></td>
            <td><code>0</code></td>
            <td></td>
        </tr><tr>
            <td><code>CORRECT_PROTANOMALY</code></td>
            <td><code>1</code></td>
            <td></td>
        </tr><tr>
            <td><code>CORRECT_DEUTERANOMALY</code></td>
            <td><code>2</code></td>
            <td></td>
        </tr><tr>
            <td><code>CORRECT_TRITANOMALY</code></td>
            <td><code>3</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### Settings {:#Settings}


*Defined in [fuchsia.accessibility/settings.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.accessibility/settings.fidl#31)*

 Settings is used to represent all the Accessibility Settings along with Matrix
 needed to apply Color Correction and Color Inversion.
 This table will be used to transfer Settings information between different services to
 either modify or get notified about Accessibility Settings.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>magnification_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> When magnification_enabled == true, user can specify an area of the screen to be magnified.
 Note that actually magnifying the region requires an addition input (gesture, button, etc.).
</td>
        </tr><tr>
            <td>2</td>
            <td><code>magnification_zoom_factor</code></td>
            <td>
                <code>float32</code>
            </td>
            <td> Degree of magnification for magnified area.
</td>
        </tr><tr>
            <td>3</td>
            <td><code>screen_reader_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> When screen_reader_enabled == true, user can specify elements of the UI to be described
 audibly.
 Note that reading a particular element requires an additional input.
</td>
        </tr><tr>
            <td>4</td>
            <td><code>color_inversion_enabled</code></td>
            <td>
                <code>bool</code>
            </td>
            <td> When color_inversion_enabled == true, certain colors are inverted across the entire screen.
 No additional user input is required for the inversion to take place once enabled.
 Colors will continue to be inverted until color_inversion_enabled is set to false.
</td>
        </tr><tr>
            <td>5</td>
            <td><code>color_correction</code></td>
            <td>
                <code><a class='link' href='#ColorCorrection'>ColorCorrection</a></code>
            </td>
            <td> When color_correction is set to DISABLED, colors are displayed normally.
 When color_correction has different value, colors are modified to correct for the specified
 type of color-blindness.
 No additional user input is required for corrections to take place once enabled.
 Correction will continue to occur until color_correction is set to DISABLED.
</td>
        </tr><tr>
            <td>6</td>
            <td><code>color_adjustment_matrix</code></td>
            <td>
                <code>float32[9]</code>
            </td>
            <td> 3x3 Matrix in row-major form which will be used by the SettingsManager
 client for applying Color Correction and Color Inversion. Display
 adapter expects a 3x3 row major matrix and A11y manager stores the
 matrix in the same format.
 Color Adjustment matrix is used to modify onscreen colors for either
 of Deuteranomaly, Protanomaly and Tritanomaly or it can be used for
 performing Color Inversion.
</td>
        </tr></table>









