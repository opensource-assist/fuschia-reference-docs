[TOC]

# fuchsia.ui.brightness


## **PROTOCOLS**

## Control {#Control}
*Defined in [fuchsia.ui.brightness/brightness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/brightness.fidl#13)*

<p>Control provides an interface to manage the brightness component.</p>

### SetAutoBrightness {#SetAutoBrightness}

<p>Turns the auto-brightness mode on.
SetManualBrightness will turn it off.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>



### WatchAutoBrightness {#WatchAutoBrightness}

<p>Requests the current auto-brightness mode.
This call implements the Hanging Get protocol as detailed in
https://fuchsia.dev/fuchsia-src/development/api/fidl.md#delay-responses-using-hanging-gets</p>

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

<p>Turns auto-brightness mode off.
Used by e.g. Settings to set manual brightness using a slider
Value is in the range 0.0 to 1.0 representing min to max.</p>

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

<p>Gets the current brightness in the range 0.0 to 1.0.
This result is valid for both manual and auto-brightness modes and is typically used
to show the current brightness on a slider.
This call implements the Hanging Get protocol as detailed in
https://fuchsia.dev/fuchsia-src/development/api/fidl.md#delay-responses-using-hanging-gets</p>

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

### SetAutoBrightnessOffset {#SetAutoBrightnessOffset}

<p>Sets the brightness offset.
This will change the built-in brightness curve by the factor of the offset.
The offset is in the range of -1.0 to 1.0.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>offset</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>



### WatchAutoBrightnessOffset {#WatchAutoBrightnessOffset}

<p>Gets the current auto brightness offset.
This call implements the Hanging Get protocol as detailed in
https://fuchsia.dev/fuchsia-src/development/api/fidl.md#delay-responses-using-hanging-gets</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>offset</code></td>
            <td>
                <code>float32</code>
            </td>
        </tr></table>

### SetBrightnessTable {#SetBrightnessTable}

<p>Sets the brightness curve as a set of points.
This will override the built-in brightness curve.</p>

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

<p>Allows a presentation owner to register a handler for color adjustments.
This API is implemented by the Brightness Manager and
called by Root Presenter.</p>

### RegisterColorAdjustmentHandler {#RegisterColorAdjustmentHandler}

<p>Registers a handler for changes in the color adjustment configuration.</p>

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

<p>Handler implemented by the owner of the presentation.
The brightness manager uses this protocol to request changes to the
screen's color adjustment matrix.</p>

### SetColorAdjustment {#SetColorAdjustment}

<p>Called when the color adjustment  has changed.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>color_adjustment</code></td>
            <td>
                <code><a class='link' href='#ColorAdjustmentTable'>ColorAdjustmentTable</a></code>
            </td>
        </tr></table>



## ColorTint {#ColorTint}
*Defined in [fuchsia.ui.brightness/color_tint.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/color_tint.fidl#10)*


### CalculateColorTint {#CalculateColorTint}


#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>request</code></td>
            <td>
                <code><a class='link' href='#SensorInfo'>SensorInfo</a></code>
            </td>
        </tr></table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reply</code></td>
            <td>
                <code><a class='link' href='#TargetColorTint'>TargetColorTint</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### BrightnessPoint {#BrightnessPoint}
*Defined in [fuchsia.ui.brightness/brightness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/brightness.fidl#51)*



<p>A tuple representing a point on the auto-brightness curve</p>


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
*Defined in [fuchsia.ui.brightness/brightness.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/brightness.fidl#58)*



<p>A set of points defining the auto-brightness curve.
They should be ordered in increasing ambient_lux</p>


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

<p>The table for screen color tint adjustments.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>matrix</code></td>
            <td>
                <code>float32[9]</code>
            </td>
            <td><p>3x3 Matrix in row-major form which will be used by root presenter
to apply color adjustment.
This field may be omitted to disable color adjustment.</p>
</td>
        </tr></table>

### SensorInfo {#SensorInfo}


*Defined in [fuchsia.ui.brightness/color_tint.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/color_tint.fidl#17)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>red</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>green</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>blue</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>clear</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>color_temperature</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>lux</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr></table>

### TargetColorTint {#TargetColorTint}


*Defined in [fuchsia.ui.brightness/color_tint.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/color_tint.fidl#36)*



<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>red</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>2</td>
            <td><code>green</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>3</td>
            <td><code>blue</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>4</td>
            <td><code>lux</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>5</td>
            <td><code>color_temperature</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>6</td>
            <td><code>brightness_with_color_match</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr><tr>
            <td>7</td>
            <td><code>brightness_without_color_match</code></td>
            <td>
                <code>float32</code>
            </td>
            <td></td>
        </tr></table>











## **TYPE ALIASES**

<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/brightness.fidl#9">brightness</a></td>
            <td>
                <code>float32</code></td>
            <td><p>A normalized relative brightness adjustment in the range
0.0 (off/minimum) to 1.0 (maximum).</p>
</td>
        </tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.ui.brightness/color_tint.fidl#7">kelvin</a></td>
            <td>
                <code>float32</code></td>
            <td></td>
        </tr></table>

