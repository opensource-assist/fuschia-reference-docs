[TOC]

# fuchsia.input.report


## **PROTOCOLS**

## InputDevice {#InputDevice}
*Defined in [fuchsia.input.report/device.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/device.fidl#16)*

<p>An |InputDevice| driver represents a single physical input device.
The InputDevice maintains an internal FIFO of |MAX_DEVICE_REPORT_COUNT|
reports for each client that connects. Reports are removed from the FIFO
once they are read by the client. If the FIFO is full, it will drop the
oldest report to make room for an incoming report.</p>

### GetReportsEvent {#GetReportsEvent}

<p>Receive an event that will be signalled when there are reports in the
Device's report FIFO. When there are events in the FIFO, |event| will have
|DEV_STATE_READABLE| triggered. When the client has read all of the events,
|DEV_STATE_READABLE| will be  cleared.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>status</code></td>
            <td>
                <code>int32</code>
            </td>
        </tr><tr>
            <td><code>event</code></td>
            <td>
                <code>handle&lt;event&gt;</code>
            </td>
        </tr></table>

### GetReports {#GetReports}

<p>Get all of the reports that have been seen since the last time this method was called.
If this returns 0 reports, please wait on the report event.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>reports</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#InputReport'>InputReport</a>&gt;[50]</code>
            </td>
        </tr></table>

### GetDescriptor {#GetDescriptor}

<p>Gets the device descriptor for this device.</p>

#### Request
<table>
    <tr><th>Name</th><th>Type</th></tr>
    </table>


#### Response
<table>
    <tr><th>Name</th><th>Type</th></tr>
    <tr>
            <td><code>descriptor</code></td>
            <td>
                <code><a class='link' href='#DeviceDescriptor'>DeviceDescriptor</a></code>
            </td>
        </tr></table>



## **STRUCTS**

### DeviceInfo {#DeviceInfo}
*Defined in [fuchsia.input.report/descriptor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/descriptor.fidl#15)*



<p>DeviceInfo provides more information about the device and lets a client
distinguish between devices (e.g between two touchscreens that come from
different vendors). If the device is a HID device, then the id information
will come from the device itself. Other, non-HID devices may assign the
ids in the driver, so it will be the driver author's responsibility to
assign sensible ids.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>vendor_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>product_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>version</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>name</code></td>
            <td>
                <code>string[256]</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### SensorAxis {#SensorAxis}
*Defined in [fuchsia.input.report/sensor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/sensor.fidl#44)*



<p>A |SensorAxis| is a normal |Axis| with an additional |SensorType| to describe what the
axis is measuring.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>axis</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>type</code></td>
            <td>
                <code><a class='link' href='#SensorType'>SensorType</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Range {#Range}
*Defined in [fuchsia.input.report/units.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/units.fidl#50)*



<p>Describe a |Range| of values.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>min</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>max</code></td>
            <td>
                <code>int64</code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>

### Axis {#Axis}
*Defined in [fuchsia.input.report/units.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/units.fidl#56)*



<p>An |Axis| is defined as a |range| and a |unit|.</p>


<table>
    <tr><th>Name</th><th>Type</th><th>Description</th><th>Default</th></tr><tr>
            <td><code>range</code></td>
            <td>
                <code><a class='link' href='#Range'>Range</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr><tr>
            <td><code>unit</code></td>
            <td>
                <code><a class='link' href='#Unit'>Unit</a></code>
            </td>
            <td></td>
            <td>No default</td>
        </tr>
</table>



## **ENUMS**

### SensorType {#SensorType}
Type: <code>uint32</code>

*Defined in [fuchsia.input.report/sensor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/sensor.fidl#13)*

<p>Each sensor value has a corresponding SensorType, which explains what the
value is measuring in the world.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>ACCELEROMETER_X</code></td>
            <td><code>1</code></td>
            <td><p>Acceleration on the X axis.</p>
</td>
        </tr><tr>
            <td><code>ACCELEROMETER_Y</code></td>
            <td><code>2</code></td>
            <td><p>Acceleration on the Y axis.</p>
</td>
        </tr><tr>
            <td><code>ACCELEROMETER_Z</code></td>
            <td><code>3</code></td>
            <td><p>Acceleration on the Z axis.</p>
</td>
        </tr><tr>
            <td><code>MAGNETOMETER_X</code></td>
            <td><code>4</code></td>
            <td><p>Strength of the Magnetic Field in the X axis.</p>
</td>
        </tr><tr>
            <td><code>MAGNETOMETER_Y</code></td>
            <td><code>5</code></td>
            <td><p>Strength of the Magnetic Field in the Y axis.</p>
</td>
        </tr><tr>
            <td><code>MAGNETOMETER_Z</code></td>
            <td><code>6</code></td>
            <td><p>Strength of the Magnetic Field in the Z axis.</p>
</td>
        </tr><tr>
            <td><code>GYROSCOPE_X</code></td>
            <td><code>7</code></td>
            <td><p>Angular Velocity in the X direction moving counter-clockwise.</p>
</td>
        </tr><tr>
            <td><code>GYROSCOPE_Y</code></td>
            <td><code>8</code></td>
            <td><p>Angular Velocity in the Y direction moving counter-clockwise.</p>
</td>
        </tr><tr>
            <td><code>GYROSCOPE_Z</code></td>
            <td><code>9</code></td>
            <td><p>Angular Velocity in the Z direction moving counter-clockwise.</p>
</td>
        </tr><tr>
            <td><code>LIGHT_ILLUMINANCE</code></td>
            <td><code>10</code></td>
            <td><p>Ambient level of Light.</p>
</td>
        </tr><tr>
            <td><code>LIGHT_RED</code></td>
            <td><code>11</code></td>
            <td><p>Ambient level of Red Light.</p>
</td>
        </tr><tr>
            <td><code>LIGHT_GREEN</code></td>
            <td><code>12</code></td>
            <td><p>Ambient level of Green Light.</p>
</td>
        </tr><tr>
            <td><code>LIGHT_BLUE</code></td>
            <td><code>13</code></td>
            <td><p>Ambient level of Blue Light.</p>
</td>
        </tr></table>

### TouchType {#TouchType}
Type: <code>uint32</code>

*Defined in [fuchsia.input.report/touch.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/touch.fidl#12)*

<p>The device type from which the touch originated.</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>TOUCHSCREEN</code></td>
            <td><code>1</code></td>
            <td><p>A touch screen has direct finger input associated with a display.</p>
</td>
        </tr></table>

### Unit {#Unit}
Type: <code>uint32</code>

*Defined in [fuchsia.input.report/units.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/units.fidl#11)*

<p>This provides an easy, standardized way to specify units. New units can
be added as needed. There should not be ambiguity between units, so no
new units should be added that can be converted from the old units.
(e.g: Please don't add DISTANCE_METERS since there is already DISTANCE).</p>


<table>
    <tr><th>Name</th><th>Value</th><th>Description</th></tr><tr>
            <td><code>NONE</code></td>
            <td><code>0</code></td>
            <td><p>The device did not specify units.</p>
</td>
        </tr><tr>
            <td><code>OTHER</code></td>
            <td><code>1</code></td>
            <td><p>The device specified units that are not convertible to any of the other units.</p>
</td>
        </tr><tr>
            <td><code>DISTANCE</code></td>
            <td><code>2</code></td>
            <td><p>A measurement of distance in 10^-6 meter units.</p>
</td>
        </tr><tr>
            <td><code>WEIGHT</code></td>
            <td><code>3</code></td>
            <td><p>A measurement of weight in 10^-3 gram units.</p>
</td>
        </tr><tr>
            <td><code>ROTATION</code></td>
            <td><code>4</code></td>
            <td><p>A measurement of rotation is 10^-3 degrees.</p>
</td>
        </tr><tr>
            <td><code>ANGULAR_VELOCITY</code></td>
            <td><code>5</code></td>
            <td><p>A measurement of angular velocity is 10^-3 deg/s.</p>
</td>
        </tr><tr>
            <td><code>LINEAR_VELOCITY</code></td>
            <td><code>6</code></td>
            <td><p>A measurement of linear velocity is 10^-3 m/s</p>
</td>
        </tr><tr>
            <td><code>ACCELERATION</code></td>
            <td><code>7</code></td>
            <td><p>A measurement of acceleration is 10^-3 Gs</p>
</td>
        </tr><tr>
            <td><code>MAGNETIC_FLUX</code></td>
            <td><code>8</code></td>
            <td><p>A measurement of magnetic_flux is 10^-6 T</p>
</td>
        </tr><tr>
            <td><code>LUMINOUS_FLUX</code></td>
            <td><code>9</code></td>
            <td><p>A measurement of light is 1 Candela</p>
</td>
        </tr><tr>
            <td><code>PRESSURE</code></td>
            <td><code>10</code></td>
            <td><p>A measurement of pressure is 10^-3 Pascal</p>
</td>
        </tr><tr>
            <td><code>LUX</code></td>
            <td><code>11</code></td>
            <td></td>
        </tr></table>



## **TABLES**

### DeviceDescriptor {#DeviceDescriptor}


*Defined in [fuchsia.input.report/descriptor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/descriptor.fidl#25)*

<p>|DeviceDescriptor| describes a physical input device. Some physical devices may
send multiple types of reports (E.g: a physical touchscreen can send touch and
stylus reports, so it will have both a TouchDescriptor and a StylusDescriptor).</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>device_info</code></td>
            <td>
                <code><a class='link' href='#DeviceInfo'>DeviceInfo</a></code>
            </td>
            <td><p>|device_info| should always be present to help distinguish between physical devices.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>mouse</code></td>
            <td>
                <code><a class='link' href='#MouseDescriptor'>MouseDescriptor</a></code>
            </td>
            <td><p>When |mouse| is present the device has a mouse.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>sensor</code></td>
            <td>
                <code><a class='link' href='#SensorDescriptor'>SensorDescriptor</a></code>
            </td>
            <td><p>When |sensor| is present the device has a sensor.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>touch</code></td>
            <td>
                <code><a class='link' href='#TouchDescriptor'>TouchDescriptor</a></code>
            </td>
            <td><p>When |touch| is present the device has a touch device.
(E.g: Touchscreen, touchpad).</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>keyboard</code></td>
            <td>
                <code><a class='link' href='#KeyboardDescriptor'>KeyboardDescriptor</a></code>
            </td>
            <td><p>When |keyboard| is present the device has a keyboard.</p>
</td>
        </tr></table>

### KeyboardDescriptor {#KeyboardDescriptor}


*Defined in [fuchsia.input.report/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/keyboard.fidl#19)*

<p>The capabilities of a keyboard device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>keys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.ui.input2/'>fuchsia.ui.input2</a>/<a class='link' href='../fuchsia.ui.input2/#Key'>Key</a>&gt;[150]</code>
            </td>
            <td><p>The list of keys that this keyboard contains.</p>
</td>
        </tr></table>

### KeyboardReport {#KeyboardReport}


*Defined in [fuchsia.input.report/keyboard.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/keyboard.fidl#25)*

<p>A single report created by a keyboard device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>pressed_keys</code></td>
            <td>
                <code>vector&lt;<a class='link' href='../fuchsia.ui.input2/'>fuchsia.ui.input2</a>/<a class='link' href='../fuchsia.ui.input2/#Key'>Key</a>&gt;[15]</code>
            </td>
            <td><p>The list of keys that are currently pressed down.</p>
</td>
        </tr></table>

### MouseDescriptor {#MouseDescriptor}


*Defined in [fuchsia.input.report/mouse.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/mouse.fidl#12)*

<p>|MouseDescriptor| describes the capabilities of a mouse.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>movement_x</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>The range of relative X movement.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>movement_y</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>The range of relative Y movement.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>scroll_v</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>The range of relative vertical scroll.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>scroll_h</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>The range of relative horizontal scroll.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>buttons</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td><p>This is a vector of id's for the mouse buttons.</p>
</td>
        </tr></table>

### MouseReport {#MouseReport}


*Defined in [fuchsia.input.report/mouse.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/mouse.fidl#33)*

<p>|MouseReport| gives the relative movement of the mouse and currently
pressed buttons. Relative means the movement seen between the previous
report and this report. The client is responsble for tracking this and
converting it to absolute movement.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>movement_x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Relative X positional displacement.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>movement_y</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Relative Y positional displacement.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>scroll_v</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Relative vertical scrolling displacement.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>scroll_h</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Relative horizontal scrolling displacement.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>pressed_buttons</code></td>
            <td>
                <code>vector&lt;uint8&gt;[32]</code>
            </td>
            <td><p>A list of currently pressed buttons.</p>
</td>
        </tr></table>

### InputReport {#InputReport}


*Defined in [fuchsia.input.report/report.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/report.fidl#10)*

<p>|InputReport| is a single report that is created by an input device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>event_time</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>|event_time| is in nanoseconds when the event was recorded.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>mouse</code></td>
            <td>
                <code><a class='link' href='#MouseReport'>MouseReport</a></code>
            </td>
            <td><p>|mouse| is the report generated if the device contains a mouse.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>sensor</code></td>
            <td>
                <code><a class='link' href='#SensorReport'>SensorReport</a></code>
            </td>
            <td><p>|sensor| is the report generated if the device contains a sensor.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>touch</code></td>
            <td>
                <code><a class='link' href='#TouchReport'>TouchReport</a></code>
            </td>
            <td><p>|touch| is the report generated if the device contains a touch device.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>keyboard</code></td>
            <td>
                <code><a class='link' href='#KeyboardReport'>KeyboardReport</a></code>
            </td>
            <td><p>|keyboard| is the report generated if the device contains a keyboard.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>trace_id</code></td>
            <td>
                <code>uint64</code>
            </td>
            <td><p>Unique ID to connect trace async begin/end events.</p>
</td>
        </tr></table>

### SensorDescriptor {#SensorDescriptor}


*Defined in [fuchsia.input.report/sensor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/sensor.fidl#50)*

<p>|SensorDescriptor| describes the capabilities of a sensor.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#SensorAxis'>SensorAxis</a>&gt;[100]</code>
            </td>
            <td><p>Each |SensorAxis| in |values| describes what a sensor is measuring and its range.
These will directly correspond to the values in |SensorReport|.</p>
</td>
        </tr></table>

### SensorReport {#SensorReport}


*Defined in [fuchsia.input.report/sensor.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/sensor.fidl#57)*

<p>|SensorReport| gives the values measured by a sensor at a given point in time.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>values</code></td>
            <td>
                <code>vector&lt;int64&gt;[100]</code>
            </td>
            <td><p>The ordering of |values| will always directly correspond to the ordering of
the values in |SensorDescriptor|.</p>
</td>
        </tr></table>

### ContactDescriptor {#ContactDescriptor}


*Defined in [fuchsia.input.report/touch.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/touch.fidl#18)*

<p><code>ContactDescriptor</code> describes the fields associated with a touch on a touch device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>position_x</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>Describes the reporting of the x-axis.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>position_y</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>Describes the reporting of the y-axis.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>pressure</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>Pressure of the contact.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>contact_width</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>Width of the area of contact.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>contact_height</code></td>
            <td>
                <code><a class='link' href='#Axis'>Axis</a></code>
            </td>
            <td><p>Height of the area of contact.</p>
</td>
        </tr></table>

### TouchDescriptor {#TouchDescriptor}


*Defined in [fuchsia.input.report/touch.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/touch.fidl#36)*

<p><code>TouchDescriptor</code> describes the fields associated with an individual touch device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>contacts</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContactDescriptor'>ContactDescriptor</a>&gt;[10]</code>
            </td>
            <td><p>The contact descriptors associated with this touch descriptor.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>max_contacts</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>The max number of contacts that this touch device can report at once.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>touch_type</code></td>
            <td>
                <code><a class='link' href='#TouchType'>TouchType</a></code>
            </td>
            <td><p>The type of touch device being used.</p>
</td>
        </tr></table>

### ContactReport {#ContactReport}


*Defined in [fuchsia.input.report/touch.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/touch.fidl#48)*

<p><code>Contact</code> describes one touch on a touch device.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>contact_id</code></td>
            <td>
                <code>uint32</code>
            </td>
            <td><p>Identifier for this contact.</p>
</td>
        </tr><tr>
            <td>2</td>
            <td><code>position_x</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>A contact's position on the x axis.</p>
</td>
        </tr><tr>
            <td>3</td>
            <td><code>position_y</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>A contact's position on the y axis.</p>
</td>
        </tr><tr>
            <td>4</td>
            <td><code>pressure</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Pressure of the contact.</p>
</td>
        </tr><tr>
            <td>5</td>
            <td><code>contact_width</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Width of the bounding box around the touch contact. Combined with
<code>contact_height</code>, this describes the area of the touch contact.
<code>contact_width</code> and <code>contact_height</code> should both have units of distance,
and they should be in the same units as <code>position_x</code> and <code>position_y</code>.</p>
</td>
        </tr><tr>
            <td>6</td>
            <td><code>contact_height</code></td>
            <td>
                <code>int64</code>
            </td>
            <td><p>Height of the bounding box around the touch contact. Combined with
<code>contact_width</code>, this describes the area of the touch contact.
<code>contact_width</code> and <code>contact_height</code> should both have units of distance,
and they should be in the same units as <code>position_x</code> and <code>position_y</code>.</p>
</td>
        </tr></table>

### TouchReport {#TouchReport}


*Defined in [fuchsia.input.report/touch.fidl](https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/touch.fidl#75)*

<p><code>TouchscreenReport</code> describes the current contacts recorded by the touchscreen.</p>


<table>
    <tr><th>Ordinal</th><th>Name</th><th>Type</th><th>Description</th></tr>
    <tr>
            <td>1</td>
            <td><code>contacts</code></td>
            <td>
                <code>vector&lt;<a class='link' href='#ContactReport'>ContactReport</a>&gt;[10]</code>
            </td>
            <td><p>The contacts currently being reported by the device.</p>
</td>
        </tr></table>









## **CONSTANTS**

<table>
    <tr><th>Name</th><th>Value</th><th>Type</th><th>Description</th></tr><tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/descriptor.fidl#7">MAX_DEVICE_NAME_LENGTH</a></td>
            <td>
                    <code>256</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/device.fidl#9">MAX_DEVICE_REPORT_COUNT</a></td>
            <td>
                    <code>50</code>
                </td>
                <td><code>uint32</code></td>
            <td></td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/keyboard.fidl#11">KEYBOARD_MAX_NUM_KEYS</a></td>
            <td>
                    <code>150</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>A hardcoded number of max keys. This should be increased in the future
if we ever see keyboards with more keys.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/keyboard.fidl#16">KEYBOARD_MAX_PRESSED_KEYS</a></td>
            <td>
                    <code>15</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>A hardcoded number of the maximum keys that can be pressed at a time.
This should be increased in the future if we see keyboards that can
handle more pressed keys.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/mouse.fidl#9">MOUSE_MAX_NUM_BUTTONS</a></td>
            <td>
                    <code>32</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>A hardcoded number of max mouse buttons. This should be increased in the future
if we ever see mice with more buttons.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/sensor.fidl#9">SENSOR_MAX_VALUES</a></td>
            <td>
                    <code>100</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>A hardcoded number of max sensor values. This should be increased in the future
if we ever see a sensor with more values.</p>
</td>
        </tr>
    <tr>
            <td><a href="https://fuchsia.googlesource.com/fuchsia/+/master/sdk/fidl/fuchsia.input.report/touch.fidl#9">TOUCH_MAX_CONTACTS</a></td>
            <td>
                    <code>10</code>
                </td>
                <td><code>uint32</code></td>
            <td><p>A hardcoded number of max contacts per report. This should be increased in the future if
we see devices with more than the max amount.</p>
</td>
        </tr>
    
</table>

