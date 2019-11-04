[TOC]

# fuchsia.ui.brightness


## **PROTOCOLS**

## Control {#Control}
*Defined in [fuchsia.ui.brightness/brightness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/brightness.fidl#13)*

 Control provides an interface to manage the brightness component.

### SetAutoBrightness {#SetAutoBrightness}

 Turns the auto-brightness mode on.
 SetManualBrightness will turn it off.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### WatchAutoBrightness {#WatchAutoBrightness}

 Requests the current auto-brightness mode.
 This call implements the Hanging Get protocol as detailed in
 https://fuchsia.googlesource.com/fuchsia/+/master/docs/development/api/fidl.md#delay-responses-using-hanging-gets

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>enabled</code></td>
            <td>
                <code>bool</code>
            </td>
        </tr></table>

### SetManualBrightness {#SetManualBrightness}

 Turns auto-brightness mode off.
 Used by e.g. Settings to set manual brightness using a slider
 Value is in the range 0.0 to 1.0 representing min to max.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### WatchCurrentBrightness {#WatchCurrentBrightness}

 Gets the current brightness in the range 0.0 to 1.0.
 This result is valid for both manual and auto-brightness modes and is typically used
 to show the current brightness on a slider.
 This call implements the Hanging Get protocol as detailed in
 https://fuchsia.googlesource.com/fuchsia/+/master/docs/development/api/fidl.md#delay-responses-using-hanging-gets

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>value</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### SetBrightnessTable {#SetBrightnessTable}

 Sets the brightness curve as a set of points.
 This will override the built-in brightness curve.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>table</code></td>
            <td>
                <code><a class='link' href='#BrightnessTable'>BrightnessTable</a></code>
            </td>
        </tr></table>



## ColorAdjustment {#ColorAdjustment}
*Defined in [fuchsia.ui.brightness/color_adjustment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/color_adjustment.fidl#11)*

 Allows a presentation owner to register a handler for color adjustments.
 This API is implemented by the Brightness Manager and
 called by Root Presenter.

### RegisterColorAdjustmentHandler {#RegisterColorAdjustmentHandler}

 Registers a handler for changes in the color adjustment configuration.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>handler</code></td>
            <td>
                <code><a class='link' href='#ColorAdjustmentHandler'>ColorAdjustmentHandler</a></code>
            </td>
        </tr></table>



## ColorAdjustmentHandler {#ColorAdjustmentHandler}
*Defined in [fuchsia.ui.brightness/color_adjustment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/color_adjustment.fidl#19)*

 Handler implemented by the owner of the presentation.
 The brightness manager uses this protocol to request changes to the
 screen's color adjustment matrix.

### SetColorAdjustment {#SetColorAdjustment}

 Called when the color adjustment  has changed.

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>color_adjustment</code></td>
            <td>
                <code><a class='link' href='#ColorAdjustmentTable'>ColorAdjustmentTable</a></code>
            </td>
        </tr></table>





## **STRUCTS**

### BrightnessPoint {#BrightnessPoint}
*Defined in [fuchsia.ui.brightness/brightness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/brightness.fidl#42)*



 A tuple representing a point on the auto-brightness curve


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>ambient_lux</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>display_nits</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### BrightnessTable {#BrightnessTable}
*Defined in [fuchsia.ui.brightness/brightness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/brightness.fidl#49)*



 A set of points defining the auto-brightness curve.
 They should be ordered in increasing ambient_lux


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>points</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#BrightnessPoint'>BrightnessPoint</a>&gt;[50]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>





## **TABLES**

### ColorAdjustmentTable {#ColorAdjustmentTable}


*Defined in [fuchsia.ui.brightness/color_adjustment.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/color_adjustment.fidl#25)*

 The table for screen color tint adjustments.


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>matrix</code></td>
            <td>
                <code>float32[9]</code>
            </td>
            <td> 3x3 Matrix in row-major form which will be used by root presenter
 to apply color adjustment.
 This field may be omitted to disable color adjustment.
</td>
        </tr></table>









